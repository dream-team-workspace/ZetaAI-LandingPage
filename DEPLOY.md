# Deployment

The ZetaAI landing page is deployed by GitHub Actions
(`.github/workflows/ci-cd.yml`) to <https://zeta.dream-team.works>.

- **Pull requests** — the `lint` job validates `index.html` with
  [html-validate](https://html-validate.org/).
- **Push to `master`** — the `deploy` job rsyncs the site (`index.html`,
  `assets/`) to the server and runs a smoke test against
  <https://zeta.dream-team.works/>.

## How it works

- The files are synced as the `deploy` user over key-only SSH (direct IPv4
  connection to `139.99.88.23`; no Cloudflare tunnel involved in the deploy
  step).
- Webroot: `/var/www/zeta.dream-team.works` (owned by `deploy:deploy`).
- nginx serves the webroot on port 80; the server's Cloudflare Tunnel
  (`ovh-server`) routes `zeta.dream-team.works` to `http://localhost:80`.
- Only `index.html` and `assets/` are deployed; repo docs, `RECON/` and the
  other markdown files stay out of the web root.

## Required repository secrets

Create in GitHub: **Settings → Secrets and variables → Actions → New repository secret**.

| Secret | Value |
| --- | --- |
| `DEPLOY_SSH_KEY` | Full contents of `~/.ssh/zeta_deploy_ed25519` (private key) |

### Deploy SSH key

- Local private key: `~/.ssh/zeta_deploy_ed25519` (comment `github-actions-zeta`)
- Its public half is in `/home/deploy/.ssh/authorized_keys` on the server.
- Server user `deploy` owns only the web roots and has no sudo.

**Rotation:** generate a new pair, append its public key to
`/home/deploy/.ssh/authorized_keys`, update the secret, then remove the old line.

## Manual deploy (fallback)

Same result as CI, run from the repo root:

```bash
mkdir -p _site
cp index.html _site/index.html
cp -r assets _site/assets

rsync -az --delete --chmod=D755,F644 \
  -e "ssh -i ~/.ssh/zeta_deploy_ed25519 -o User=deploy" \
  ./_site/ 139.99.88.23:/var/www/zeta.dream-team.works/
```

## Server layout

| What | Where |
| --- | --- |
| Web root | `/var/www/zeta.dream-team.works` (owned by `deploy:deploy`) |
| nginx vhost | `/etc/nginx/sites-available/zeta.dream-team.works.conf` |
| Tunnel ingress | `zeta.dream-team.works` → `http://localhost:80` (tunnel `ovh-server`) |
| DNS | CNAME `zeta` → `bd0efb4d-a596-4c6f-9997-7276f4980f0b.cfargotunnel.com` (proxied) |
| SSH (CI) | `deploy@139.99.88.23:22`, key-only |
| SSH (admin) | `ubuntu@139.99.88.23` (key-only, sudo) |

## Hardening notes

- `PasswordAuthentication no` is enforced via `/etc/ssh/sshd_config.d/00-hardening.conf`
  (required because `50-cloud-init.conf` sets `yes` and sshd uses the first value found).
  The `deploy` and `root` accounts are password-locked.
- Optional: install `fail2ban`; not strictly needed with key-only auth.
- Optional: pin the runner's SSH host key by storing a `known_hosts` secret and
  switching to `StrictHostKeyChecking yes` (currently TOFU via `accept-new`).
- If the server IP ever changes (`139.99.88.23`), update `DEPLOY_HOST` in the workflow.

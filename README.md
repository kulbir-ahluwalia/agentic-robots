# enterprises/agentic-robots

**Agentic Robots** — Kulbir + Chahit fleet for Physical AI, distributed compute, VLMs on real robots, and agentic infrastructure.

Live site: https://agentic-robots.ai (powered by this repo via GitHub Pages)

## What's here (all the features)
- `index.html` + `CNAME` — clean professional landing page (dark theme, fleet roster with short `ar-*` aliases, research, links)
- `fleet/` — inventory (devices.json), ssh/ (canonical config template)
- `docs/` — HOWTO for Squarespace domain linking, device inventory
- `landing/` — source of the homepage
- `README.md`, scripts, etc.

## Deploy / update the site
The site is static HTML served by GitHub Pages from the root of `main`.

After any change to `index.html`:
```bash
git add index.html
git commit -m "update: landing page"
git push
```

## Initial setup (one time)
1. Create the GitHub Organization named **enterprises** (if not done):
   - Go to https://github.com/account/organizations/new
   - Name: `enterprises`
   - Create (free plan ok for public repos)

2. Create the repo (or it was created):
   ```bash
   # This dir already has the remote set
   git push -u origin main
   ```

3. Enable GitHub Pages + custom domain:
   - In this repo on GitHub: Settings → Pages
   - Build and deployment: Source = "Deploy from a branch"
   - Branch: `main`, folder: `/ (root)`
   - Custom domain: `agentic-robots.ai`
   - Save. GitHub will check the DNS (see below).

4. Point the domain (critical to kill Squarespace "coming soon" crap):
   In Squarespace DNS Settings for `agentic-robots.ai`:
   - Delete the Squarespace Defaults A records (the 4x 198.49... and 198.185... for @)
   - Delete the `www` CNAME (ext-sq.squarespace.com)
   - Delete the HTTPS record
   - Keep Google Workspace (MX + TXT) if you want email
   - Add Custom records:
     - 4x A records:
       Name: `@`
       Data: 185.199.108.153
       (repeat for .109.153, .110.153, .111.153)
     - 1x CNAME:
       Name: `www`
       Data: `enterprises.github.io`

   Propagation: up to 4 hours (TTL), usually faster. Use `dig agentic-robots.ai` to check.

Once DNS is updated and Pages verifies the domain, https://agentic-robots.ai will serve this clean site (no more coming soon placeholder).

## Other domains
- agentic-robots.net / .org : repeat the A/CNAME or set URL redirects to .ai in Squarespace
- kulbir-singh-ahluwalia.com : already points correctly to GitHub Pages — leave it

## Fleet SSH
See `fleet/ssh/config` for the canonical SSH config with all the `ar-*` aliases and Tailscale hosts. Copy to `~/.ssh/config` on machines and distribute via your usual fleet syncs.

Full HOWTO for domains is in `docs/HOWTO_squarespace_agentic_robots_domains.md`

This repo + Tailscale + the fleet key = the control plane for the agentic robots enterprise.


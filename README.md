# enterprises/agentic-robots

Canonical home for **Agentic Robots** — Kulbir + Chahit (and collaborators) fleet of physical + digital agents, heavy compute (DGX Spark pair, RTX 5090, Jetson Thor, clusters), and the supporting infrastructure.

## Goals (use *all* features of this repo)
- Single source of truth for device inventory, SSH config, Tailscale reachability, and fleet orchestration scripts.
- Reproducible distributed training / inference / data pipelines across heterogeneous hardware.
- Professional public face (website + branding) for `agentic-robots.ai` / `.net` / `.org`.
- Memory, runbooks, and skills that survive across the entire fleet (MSI, DGX-X1/X2, Siebel, MacBook, Jetson, Delta/ICC/ICRN, future machines).

## Layout (grow this)
- `fleet/inventory/` — devices.json, tailscale-ips, hardware capabilities, last-known-state
- `fleet/ssh/` — the canonical `config` + fragments. See also historical scripts in the operators' home dirs.
- `fleet/scripts/` — bootstrap, health, sync, probe, update-ssh, etc. (many battle-tested versions live in `~/*.sh`)
- `website/` or `landing/` — source for the public site (or guidance linking Squarespace ↔ GitHub Pages / self-hosted)
- `docs/` — fleet-device-info snapshots, runbooks, CoRL/RA-L artifacts, memory
- `skills/` or `agent-hub/` — reusable agent patterns (v14+), prompt libraries, etc.

## SSH / fleet access
See `fleet/ssh/config` (and the version that ends up in each machine's `~/.ssh/config`).

Typical short aliases after this config is active:
- `ssh msi`, `ssh ar-x2`, `ssh siebel`, `ssh ar-mbp`, `ssh jetson-thor`
- UofI clusters: `ssh delta`, `ssh icc`, `ssh icrn`

All home devices use the `id_ed25519_fleet` key (never commit private keys).

## Domains we own (Squarespace)
- agentic-robots.ai (primary, exp 2028)
- agentic-robots.net (2029)
- agentic-robots.org (2029)
- kulbir-singh-ahluwalia.com (personal site, already pointed at GitHub Pages)
- prachit-puranik.com (2029)

See `HOWTO_squarespace_agentic_robots_domains.md` for exact DNS linking steps (GitHub Pages vs Squarespace builder).

## Contributing
Open PRs against this repo for:
- New device onboarding (add to inventory + SSH fragment + key copy instructions)
- Improved fleet scripts or distributed recipes
- Website / branding changes
- Memory updates

This repo + the Tailscale network + the dedicated fleet key = the "enterprises" control plane.


# How to link Squarespace domains (agentic-robots.* + others) to a real website

You just bought / transferred these via Squarespace (as of 2026-06):
- agentic-robots.ai   (Active, expires Jun 12 2028)  ← primary brand
- agentic-robots.net  (Active, expires Jun 12 2029)
- agentic-robots.org  (Active, expires Jun 12 2029)
- kulbir-singh-ahluwalia.com (already working, expires Feb 15 2028)
- prachit-puranik.com (expires Jun 12 2029)

Current reality (verified 2026-06-14):
- kulbir-singh-ahluwalia.com → GitHub Pages (185.199.108.153 etc.)
- agentic-robots.* → Squarespace default parking IPs (198.49.23.x / 198.185.159.x). Visiting them shows the "Create a memorable, professional website" prompt.

## Two main paths (pick one per domain or mix)

### Path A — Fastest beautiful professional site (recommended for the new "agentic-robots" brand)
1. Log into Squarespace → Domains.
2. For **agentic-robots.ai** click "Create Website" (or go to the domain and choose "Build a website").
3. Use the AI builder or a clean template. Suggested name / tagline:
   - "Agentic Robots"
   - "Physical AI • Distributed Fleet • Natural Language Robotics"
   - Kulbir Singh Ahluwalia + Chahit Jain + DASLAB + collaborators
4. Add:
   - Prominent GitHub org link (https://github.com/enterprises/agentic-robots)
   - Link to the detailed personal site (https://kulbir-singh-ahluwalia.com)
   - CoRL / RA-L paper links, WaypointGen, fleet photos, "Compute available for collaboration"
   - Contact / newsletter (you already have the Squarespace form pattern)
5. Once published, agentic-robots.ai (and www.) will just work — no extra DNS changes needed for the primary domain because Squarespace is both registrar + host.
6. For .net and .org:
   - In Squarespace, go to each domain → "Forwarding" or "URL Redirect".
   - Create a 301 permanent redirect to https://agentic-robots.ai
   - (Optional) Point them the same way as .ai and host three almost-identical sites if you want exact TLD match for legal/branding reasons.

Also: turn on the 2FA banner you screenshotted. It's free and good hygiene for the registrar.

### Path B — GitHub Pages / code-driven site (matches your existing personal site tech + full version control)
Use this if you want everything in the `enterprises/agentic-robots` repo (or a subdir/website repo) and versioned like the kulbir academic site.

Steps:

1. Decide repo + pages setup (in https://github.com/enterprises/agentic-robots):
   - Option: Put a `website/` or `landing/` folder in the main repo and use GitHub Pages "deploy from main /docs" or a GitHub Action.
   - Or create a dedicated repo `agentic-robots-site` under the org.
   - Or simply use the root + `/docs` for a simple static site (index.html + assets, or Hugo/Jekyll).

2. Build the site locally or with a template. You can start by copying/adapting the structure from your working kulbir-singh-ahluwalia.com (it's served from GitHub Pages).

3. In the GitHub repo:
   - Settings → Pages
   - Source: Deploy from a branch (main) or GitHub Actions
   - Custom domain: enter `agentic-robots.ai`
   - GitHub will tell you to add a `CNAME` file in the published folder containing exactly:
     ```
     agentic-robots.ai
     ```
   - Commit that file.

4. In Squarespace (the DNS part):
   - Domains → agentic-robots.ai → DNS
   - You will see Squarespace's default A records (the 198.49... ones). Delete or edit them.
   - Add these four A records (GitHub Pages apex requirement — use all four):
     ```
     agentic-robots.ai   A   185.199.108.153
     agentic-robots.ai   A   185.199.109.153
     agentic-robots.ai   A   185.199.110.153
     agentic-robots.ai   A   185.199.111.153
     ```
   - For the www subdomain (highly recommended):
     ```
     www   CNAME   <your-github-pages-target>
     ```
     The target is usually something like `enterprises.github.io` or `agentic-robots.github.io` (GitHub shows the exact value after you add the custom domain in step 3).
   - Save. Propagation usually 5–60 minutes. GitHub will show a green check when it verifies the CNAME/A records.

5. Repeat the A + CNAME records for agentic-robots.net and .org if you want them to resolve to the same Pages site (GitHub supports multiple custom domains on one Pages site). Or simply forward them (easier, see Path A).

6. (Optional but nice) Add CAA records if you ever want to be strict, and set up email forwarding in Squarespace for @agentic-robots.ai if you want professional email without running your own mailserver.

## For the existing kulbir-singh-ahluwalia.com
It is already correctly pointed (A records to GitHub's range). Nothing to change unless you want to add www. or subdomains (e.g. cs498gc.kulbir-singh-ahluwalia.com). Just keep the A records in Squarespace DNS for that domain.

## prachit-puranik.com
Treat exactly like the others. Options:
- Quick Squarespace site for Chahit (or joint landing)
- Point to an existing personal site of his via A/CNAME
- Forward to agentic-robots.ai or the main personal site

## Verification checklist after changes
- `dig +short agentic-robots.ai` should eventually show the 185.199.x.x GitHub IPs (or stay on Squarespace IPs if using Path A).
- Browser: https://agentic-robots.ai (no certificate warnings after a bit)
- GitHub repo Pages settings shows the custom domain as verified.
- Test on phone + different networks (DNS caching).

## Recommendation (June 2026)
- Use **Path A (Squarespace AI builder)** for agentic-robots.ai right now — you get a polished, on-brand marketing + hub site in < 1 hour, perfect for sharing with collaborators, advisors, internship teams, etc.
- Keep the deep technical content (papers, code, detailed CV, course) on the existing https://kulbir-singh-ahluwalia.com (already excellent).
- Link the two sites to each other.
- Later, if/when you want a fully code-owned version under the GitHub org, migrate or add a "View source / advanced" section that points at the repo (or run a static copy).

## 2FA reminder
Secure the Squarespace account with the two-factor authentication they prompted you about.


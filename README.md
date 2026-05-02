# MasCom Public POC — Deployment Folder

This folder is the **Quadrant 1** marketing front door per
`mcp_services/sops/2026.05.02_0100_ARCH_SOP_Public-MVP-Vision_v01.00.md` §3.1.
It contains **only public-safe artifacts**. No tenant data. No PII. No
business records. Generic copy and architecture only.

## What's here

- `index.html` — single-file marketing front door (dark-academia palette, self-contained)
- `README.md` — this file (deployment instructions)

## What's NOT here (and must NEVER be added)

The following lists are populated dynamically by the privacy review
in `mcp_services/handoffs/2026.05.02_0500_ARCH_SESSION-STATE_104-Phase-A-Triple-Yes-Executed_v01.00.md`
and the second subagent report. Confirm against the **current** repo
before any add:

- `tenants/{1hb_paul,kip,laura,patti,stephen,travis,detective}/` (any tenant data)
- `26_Cents_LLC/` (business records — closing docs, deeds, financials, etc.)
- `Main Street Manor/` (operations corpus, AI Instructions, audits)
- `mcp_services/data/credentials/registry.tsv` (node identity ledger)
- `mcp_services/sops/2026.04.27_Family_Matters_Forensic_SOT.md` (highest-sensitivity)
- `mascom_hq.html` and the two `mascom_hq__*.html` faces (these are RENDERED FOR `1hb_paul` tenant; not generic)
- Anything under `mcp_services/sops/` that names a real person, real address, real account number, real case file
- Family-Matters audio (`.m4a` files now in `tenants/1hb_paul/cases/CASE-Family-Matters/`)

## Deployment options

### Option B (RECOMMENDED): separate public mirror repo + GitHub Pages

Run from this folder:

```bash
# 1. Authenticate gh if you haven't already
gh auth login

# 2. Create a NEW PUBLIC repo (do NOT make the current private repo public)
gh repo create mascom-public-poc --public --description "MasCom public POC — universal AI governance, BYOK/BYOC/BYOAI"

# 3. Initialize a fresh git folder (this folder is currently inside the private repo's worktree;
# we want it OUTSIDE so it doesn't carry private history)
cp -r "C:/Repos/mc-ref-4tv9x2/public_poc/." "$HOME/mascom-public-poc/"
cd "$HOME/mascom-public-poc"
git init
git remote add origin https://github.com/xr7t9ops/mascom-public-poc.git
git add index.html README.md
git commit -m "Initial public POC — marketing front door"
git branch -M main
git push -u origin main

# 4. Enable Pages (settings → Pages → source: main / root)
gh repo edit xr7t9ops/mascom-public-poc --enable-pages || \
  echo "Open https://github.com/xr7t9ops/mascom-public-poc/settings/pages and enable Pages from main branch root"

# 5. Once enabled, site lives at: https://xr7t9ops.github.io/mascom-public-poc/
```

### Option C (quick alternative): Wix MCP push

If you'd rather use your existing Wix site as the marketing front
door — push the `index.html` content as a Wix page. Less control but
zero infra setup. The Wix MCP `mcp__f332843b-*` is already connected.

### Option D: Custom domain via Cloudflare Pages / Netlify

If you want `mascom.app` as the URL and don't want to wait on GitHub
Pages DNS propagation, Cloudflare Pages or Netlify can deploy this
folder directly from a fresh repo. Same content, different host. Both
are free for static sites.

### Option A (DO NOT): Make `mc-ref-4tv9x2` public

Would expose every tenant's data. Repeat: do not.

## What this front door does

- Hero: BYOK/BYOC/BYOAI positioning
- 5 sample MasComs (Detective lighthouse + Real Estate, Tax Prep, Illustrator, Nurse Practitioner) + a "Bring your own role" card
- 3-layer architecture explanation (Source/Graph/Interface)
- Email capture (DOES NOT actually send anywhere; placeholder UX only)
- Footer with PHD attestation

## What this front door does NOT do (yet)

- Connect to a real CRM or email list (Phase G.1 work — needs backend)
- Show the Detective POC playable demo (Phase G.2 — needs the sanitized POC HTML at a public URL; right now Detective POC is `design-references/PILOT_artifact-detail-reference.html` in private repo and needs sanitization before public push)
- Auth/sign-up flow (Phase G.2 — `app.mascom.app` is a separate quadrant)
- Solar-MasCom rendering (Phase G.3 — separate workstream)

## After deploying

Update `mcp_services/sops/2026.05.02_0100_ARCH_SOP_Public-MVP-Vision_v01.00.md`
§3.1 with the actual deployed URL (currently `mascom.app or similar`
— resolve at deploy time). Promote that SOP via mechanical-class
auto-accept.

Add a `published_at` row to `repo_graph.json` for this `index.html`
node so the deployment is tracked.

*Pure Heart Directive: 100% Legal, 100% Ethical, Zero Greed.*

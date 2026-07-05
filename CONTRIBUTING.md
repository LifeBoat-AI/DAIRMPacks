# Contributing a pack

Packs are how Helios operationalizes a governance framework or a business-case model without code
changes. Anyone can author one.

## Open-source pack (lives in this repo)

1. Copy `packs/_template/` → `packs/<your.pack.id>/`.
2. Fill `pack.json` and add any content files it references.
3. Validate: `helios pack validate packs/<your.pack.id>`
   - schema check · **every obligation must cite a resolvable source** (NFR-003) · dry-run conflict
     check against a reference tenant.
4. Sign: `helios pack sign packs/<your.pack.id> --key <your-key>` (BYOG uses a tenant-registered key).
5. Add your pack to `catalog.json`.
6. Open a PR. CI re-runs validation.

## Paid pack (listed here, delivered via the control plane)

Submit to Lifeboat (hello@lifeboat-ai.com). We register the entitlement (e.g.
`framework:your_framework`), sign with the Lifeboat key, and add a **metadata-only** entry to
`catalog.json`. The signed archive ships to entitled tenants via the control plane — it is not
committed here.

## Quality bar

- **Citations, always.** Obligations without a machine-resolvable citation are rejected at validation.
- **Least surprise.** Prefer `require`/`condition` over `prohibit`; a `prohibit` changes behavior and
  will land as `draft` for the CDAIO to confirm (HITL).
- **Composable.** Assume other packs are active. Declare a `priority` if your obligations may overlap.
- **In-tenant only.** No contribution may introduce an external network call (NFR-001 zero-egress).

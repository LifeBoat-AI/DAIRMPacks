# Pack template

Copy this directory to `packs/<your.pack.id>/` and edit `pack.json`.

- `id` — reverse-DNS unique (e.g. `acme.iso_42001`).
- `type` — `governance` or `business_case`.
- `license` — `open_source` (full contents live in this repo) or `paid` (metadata only; archive
  delivered via the control plane on entitlement). Set `entitlement` when `paid`.
- `contributions[]` — one entry per typed unit. See the full contribution model + all `kind`s in the
  Helios spec `docs/helios/PACK_SYSTEM.md`. Every `obligations` item **must** carry a `citation_ref`.
- `signature` — filled by `helios pack sign`; leave as `unsigned` while drafting.

Validate before submitting: `helios pack validate packs/<your.pack.id>` (schema + citation + conflict
dry-run). Then sign and open a PR (open-source) or submit to Lifeboat (paid).

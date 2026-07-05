# DAIRMPacks — Data & AI Risk Management Packs

The **Lifeboat registry** of installable governance packs for **[Helios](https://github.com/LifeBoat-AI/helios)** — the BYO‑Databricks data & AI governance platform.

A CDAIO starts a new job, opens Helios, picks **"EU AI Act"** from the catalog, and in minutes has a
*functioning* governance environment: the right controls, cited obligations, a risk agent that scores
against the framework, committees wired to the right queues, and agents tuned to it. No consultant,
no config project. Packs are **"mod packs" for governance** — install, activate, compose, remove.

> Think of this repo the way you'd think of an MCP‑server registry or a package index: a place to
> **discover and distribute** packs. It is *not* a runtime dependency — Helios never calls this
> registry while running. Packs are fetched **out‑of‑band**, **signature‑verified in‑tenant**, then
> activated. That's what keeps Helios's zero‑egress guarantee intact.

## What's in a pack

Two pack **types** today, one shared machinery:

| Type | What it operationalizes | Examples |
|---|---|---|
| `governance` | A governance/compliance framework, end‑to‑end | EU AI Act · NIST AI RMF · ISO 42001 · DCAM/DAMA · state regs |
| `business_case` | A standard business‑case value model (→ a generated Business Case form + backend) | Labor‑hours‑saved · Revenue uplift · Cost avoidance · Risk/rework |

A `governance` pack can contribute: a **regime**, **controls/policies**, machine‑checkable **cited
obligations**, **risk‑classification** schemes, **risk‑assessment** grounding, **committee routing**,
**revalidation** cadences, **decision‑rights** bindings, and endpoint assets — versioned **prompts**,
agent **skills**, and (later) **fine‑tuning/adapter** references. See the full contribution model in
the Helios spec: **`docs/helios/PACK_SYSTEM.md`**.

## Open‑source vs paid

- **Open‑source packs** live here in full (`packs/<id>/`), free to install.
- **Paid packs** are *listed* in [`catalog.json`](./catalog.json) with metadata only; their signed
  archives are delivered via the Lifeboat control plane once the tenant's license carries the matching
  entitlement (e.g. `framework:eu_ai_act`).

## Trust model

Every pack is an **Ed25519‑signed** archive (same crypto as the Helios offline license). The signature
binds the manifest + a content hash, verified **locally** in the tenant before activation. Tampering or
a swapped file fails verification. Lifeboat‑published packs are signed with the Lifeboat key; a tenant's
own **BYOG** packs are signed with a tenant key registered in Helios.

## Installing a pack into Helios

1. Download the pack archive (open‑source: from `packs/<id>/`; paid: delivered on entitlement).
2. Upload it into your Helios tenant (evidence Volume) — or let the installer stage it at deploy.
3. In Helios → **Settings → Packs**, verify the signature and **Activate**.
   Obligations with legal effect land as `draft` for you to confirm (HITL) before they bind.

## Authoring a pack

1. Copy [`packs/_template/`](./packs/_template/) → `packs/<your.pack.id>/`.
2. Fill `pack.json` (identity, `type`, `license`, contributions) and add content files.
3. `helios pack validate <dir>` — schema + **citation** checks + a dry‑run conflict check.
4. `helios pack sign <dir> --key …`.
5. Open a PR here (open‑source) or submit to Lifeboat (paid). See [CONTRIBUTING.md](./CONTRIBUTING.md).

## Layout

```
catalog.json                 # the registry index (open + paid, with metadata)
packs/
  _template/                 # copy this to start a new pack
    pack.json
    README.md
  lifeboat.eu_ai_act/        # lighthouse governance pack (in progress)
    pack.json
```

---
© 2026 Lifeboat AI, Inc. Repo + open‑source packs: Apache‑2.0 (see [LICENSE](./LICENSE)). Paid packs
are proprietary and licensed per entitlement.

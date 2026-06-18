# iartifact-registry

Public ledger of sealed iArtifact provenance records.

---

## Architecture

**The CSV in this repository is the canonical, append-only ledger.** Every registered iA-ID has exactly one row here. Rows are never modified or deleted — only appended.

The Cloudflare Worker at `iartifact-registry.iartifact.workers.dev` is a thin, read-only query layer over this CSV. It has no separate state. When you query the Worker, it reads from the data synced from this repo. The Worker is a convenience API for the iArtifact desktop app and the public verifier — it does not have its own database.

This means:
- The canonical source of truth is this repository and its commit history
- Every append is permanently timestamped by GitHub's commit infrastructure
- The CSV can be audited, forked, or independently served by anyone
- Deleting or altering a row requires rewriting git history — detectable by anyone watching the repo

---

## CSV schema

```
ia_id,artifact_type,creator,sealed_at,seal_hash,name
```

| Column | Description |
|---|---|
| `ia_id` | Unique iArtifact identifier — hex string, 12–64 characters, generated at seal time |
| `artifact_type` | Type of work (e.g., `literary`, `visual`, `audio`, `video`, `mixed`) |
| `creator` | Creator name as recorded in the iArtifact app at sealing time |
| `sealed_at` | ISO 8601 UTC timestamp of sealing |
| `seal_hash` | SHA-384 hex of the manifest at seal time (from the `sealed` chain event) |
| `name` | Human-readable name of the sealed artifact |

---

## First ledger entry

The first registered work in this ledger is the iArtifact literary work underlying U.S. Copyright Registration 1-15177775421, filed 2026-06-04 by Terry Whitaker / Ground Zero Studios. Once the iA-ID for that sealed artifact is confirmed, it will appear as the first data row.

**To add your artifact:** Seal it in the iArtifact desktop app, then submit the iA-ID via the in-app registry publish flow. Records are reviewed and appended manually to maintain ledger integrity.

---

## Verify any entry

Drop the artifact folder at the public verifier:
**https://terrywhitakergithub.github.io/iartifact-verify/**

The verifier runs entirely in your browser. Nothing is uploaded.

---

## Version history

| Date | Notes |
|---|---|
| 2026-06-17 | Initial ledger created. Header row added. Schema documented. Architecture clarified: CSV is canonical, Worker is read-only query layer. |

---

## License and provenance

Copyright © 2024–2026 Ground Zero Studios. All rights reserved.  
Author: Terry Whitaker, Hamilton, Ohio  
U.S. Copyright Registration 1-15177775421 (Literary Work, filed 2026-06-04)  
Built within the SDEA framework.

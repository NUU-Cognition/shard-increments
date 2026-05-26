---
id: 1073f709-0367-4917-947f-e6d7ee6fb98c
tags:
  - "#f/metadata"
  - "#f/type"
---

# Increment

A scoped piece of work, modeled as a loop. Opening an increment is a commitment — closing it means the work reached a coherent stopping point. Checkpoints consolidate closed increments and verify system-wide coherence.

## Properties

| Property | Value |
|----------|-------|
| Tag | `#inc/increment` |
| Location | `Mesh/Increments/` |
| Archive | `Mesh/Archive/Increments/` |
| Naming | `(Increment) X.N - [Name].md` |
| Numbering | Auto-increment from highest N under current checkpoint |

## Lifecycle

```
open → closed
         ↓
    (may continue in a future increment via continues field)

Any status → deprecated
```

## Version Format

- `X.0` — Checkpoint (major loop close)
- `X.N` — Increment (scoped work, N >= 1)
- `X.A` — Adhoc (small fixes)

## Templates

- [[tmp-inc-increment-v0.2]] — Standard increment
- [[tmp-inc-checkpoint-v0.2]] — Checkpoint with audit
- [[tmp-inc-adhoc-v0.2]] — Adhoc increment

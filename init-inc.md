# Increments Shard

Group work into loops. Open a loop when starting something, close it when the work lands. Checkpoints verify system-wide coherence.

## Core Concept: Loops

An increment is an open loop — a scoped piece of work that needs to be closed. Opening a loop is a commitment. Closing it means the work reached a coherent stopping point, even if the broader topic continues in a future increment.

- **Open loop** = increment with work in progress
- **Closed loop** = increment that reached its stopping point
- **Health metric** = number of open loops. Fewer is better. Too many open loops = project entropy.

Nothing is ever truly "finished" — a topic can continue in a new increment under a later checkpoint, linked via the `continues` field.

## Version Format

```
X.N = Checkpoint.Increment

5.2 = Checkpoint 5, Increment 2
```

| Type | Pattern | Purpose |
|------|---------|---------|
| Checkpoint | `X.0` | Major loop close. Verifies system coherence. Sets a new baseline. |
| Increment | `X.N` | A scoped piece of work. Opens a loop, closes when work lands. |
| Adhoc | `X.A` | Small fixes that don't warrant their own loop. Always exists alongside a checkpoint. |

## Status

All increments use the `status` frontmatter field:

| Value | Meaning |
|-------|---------|
| `open` | Loop is open, work is happening |
| `closed` | Loop is closed, work reached its stopping point |
| `deprecated` | Loop abandoned, work didn't land |

## Tags

Tags are for type classification only. State is tracked via the `status` field.

| Tag | Purpose |
|-----|---------|
| `#inc/increment` | All increments (including adhoc) |
| `#inc/checkpoint` | Checkpoint files |
| `#inc/adhoc` | Adhoc increments (used alongside `#inc/increment`) |
| `#inc/dashboard` | Dashboard file |

## Frontmatter

All increments use the `increment` field to store their version string:

```yaml
increment: "4.2"
checkpoint: "[[(Increment) 4.0 - Shard Ecosystem]]"
continues:
  - "[[(Increment) 2.1 - Prior Work]]"
opened: 2026-03-15
```

### Continuity Threading

When a topic spans multiple checkpoints, increments link back via `continues`:

```
4.1 Lattice System (closed)
  ↑ continues
6.2 Lattice Query Engine (closed)
  ↑ continues
9.1 Lattice 2.0 (open)
```

This gives you a thread — the full history of a topic across the project's lifetime. You can trace any capability back to its origin.

## Lifecycle

1. **Open** — Create an increment with scope and context
2. **Work** — Complete tasks, check off requirements
3. **Close** — Work landed, loop is closed. Add closing summary.
4. **Checkpoint** — When all loops are closed, create a checkpoint to verify coherence and set a new baseline

## File Structure

- Location: `Mesh/Increments/`
- Archive: `Mesh/Archive/Increments/`
- Format: `(Increment) X.N - Name.md`
- Dashboard: `(Dashboard) Increments.md`

## Checkpoint

A checkpoint is not a passive roll-up. It is an active verification:

1. **All loops closed** — every increment under this checkpoint is closed or deprecated
2. **State audit** — codebase, workspace, docs — everything is coherent
3. **Baseline set** — future increments build from this verified foundation
4. **Narrative** — what was accomplished, what the system looks like now

## Dashboard

`(Dashboard) Increments.md` — DataviewJS-powered live view showing loop health, open increments, recently closed increments, and checkpoint history.

## Skills

| Skill | File | Purpose |
|-------|------|---------|
| Create | `sk-inc-create.md` | Open a new loop with scope and context |
| Close | `sk-inc-close.md` | Close a loop, verify work landed |
| Checkpoint | `sk-inc-checkpoint.md` | Create checkpoint, audit coherence, set baseline |
| Sync | `sk-inc-sync.md` | Validate all increment files, dashboard, and loop health |

## Workflows

| Workflow | File | Purpose |
|----------|------|---------|
| Create with Notepad | `wkfl-inc-create_ntpd.md` | Open a loop + start brainstorming in a linked notepad |

## Templates

| Template | File | Purpose |
|----------|------|---------|
| Increment | `tmp-inc-increment-v0.2.md` | Standard increment artifact |
| Checkpoint | `tmp-inc-checkpoint-v0.2.md` | Checkpoint with audit checklist |
| Adhoc | `tmp-inc-adhoc-v0.2.md` | Adhoc increment for small fixes |
| Dashboard | `tmp-inc-dashboard-v0.2.md` | Loop health dashboard |

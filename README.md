# Increments

Group work into loops — open, close, checkpoint.

## Version Format

```
X.N = Checkpoint.Increment
5.2 = Checkpoint 5, Increment 2
```

| Type | Pattern | Purpose |
|------|---------|---------|
| Checkpoint | X.0 | Major loop close, verifies system coherence |
| Adhoc | X.A | Small fixes, always exists alongside a checkpoint |
| Increment | X.N | Scoped piece of work, opens a loop |

## Status Values

`open` | `closed` | `deprecated`

## Quick Reference

| Action | Command |
|--------|---------|
| Open a loop | Load [[init-inc]], run [[sk-inc-create]] |
| Open a loop + brainstorm | Load [[init-inc]], run [[wkfl-inc-create_ntpd]] |
| Close a loop | [[sk-inc-close]] |
| New checkpoint | [[sk-inc-checkpoint]] |
| Validate & health check | [[sk-inc-sync]] |

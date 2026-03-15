This skill belongs to the Increments shard. Ensure you have [[init-inc]] in context before continuing.

# Skill: Checkpoint

Create a new checkpoint — audit all loops, verify coherence, set a new baseline.

# Input

- (Optional) Checkpoint name

# Actions

1. Find the current checkpoint (highest `X.0`)
2. Find all increments under this checkpoint
3. Verify all increments are `closed` or `deprecated`:
   - If open increments exist, warn user and ask how to proceed (close them, deprecate them, or checkpoint anyway)
4. Determine the new checkpoint version: `(X+1).0`
5. Create checkpoint file using [[tmp-inc-checkpoint-v0.2]]:
   - Path: `Mesh/Increments/(Increment) (X+1).0 - [Name].md`
   - `consolidates`: list of wikilinks to all closed increments
   - Fill the Consolidated table summarizing each increment
   - Complete the Audit checklist
   - Write the State section describing current system capabilities
6. Create a new adhoc increment using [[tmp-inc-adhoc-v0.2]]:
   - Path: `Mesh/Increments/(Increment) (X+1).A - Adhoc.md`
   - `increment`: `"(X+1).A"`
   - `checkpoint`: wikilink to the new checkpoint
   - `opened`: today's date
7. Run [[sk-inc-sync]]

# Output

- New checkpoint file with audit and consolidation
- New adhoc increment for the next cycle

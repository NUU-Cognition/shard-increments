This skill belongs to the Increments shard. Ensure you have [[init-inc]] in context before continuing.

# Skill: Close Increment

Close a loop — verify work landed, add closing summary.

# Input

- Target increment (name or path; if omitted, ask user)

# Actions

1. Read the target increment file
2. Check linked tasks (via the Artifacts Dataview query or by searching for tasks with `increment` linking to this increment):
   - If all tasks are `done` or `deprecated`, proceed
   - If tasks remain open, ask user: close them now, move to another increment, or deprecate?
3. Update `status` in frontmatter from `open` to `closed`
4. Append a closing log entry: `| YYYY-MM-DD | X.N | Loop closed — [brief summary of what landed] |`
5. Run [[sk-inc-sync]]
6. Check if all increments under the current checkpoint are now `closed`. If so, suggest running [[sk-inc-checkpoint]]

# Output

- Increment file with `status: closed` and closing log entry

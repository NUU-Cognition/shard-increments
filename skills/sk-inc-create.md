This skill belongs to the Increments shard. Ensure you have [[init-inc]] in context before continuing.

# Skill: Create Increment

Open a new loop for the current checkpoint.

# Input

- Increment name
- Context for the increment (what it delivers and why)
- (Optional) `continues` links to prior increments on the same topic

# Actions

1. Find the current checkpoint — glob `Mesh/Increments/` for `#inc/checkpoint` files, pick the highest `X.0`
2. Find the next increment number — glob for `#inc/increment` files under the current checkpoint, find the highest `N`, use `N + 1`. Skip `A` (reserved for adhoc)
3. Create the increment file using [[tmp-inc-increment-v0.2]]:
   - Path: `Mesh/Increments/(Increment) X.N - [Name].md`
   - Status: `open`
   - `increment`: `"X.N"`
   - `checkpoint`: wikilink to current checkpoint
   - `continues`: wikilinks to prior increments if continuing a topic
   - `opened`: today's date
   - Fill Context, Scope from user input
4. Add initial log entry: `| YYYY-MM-DD | X.N | Increment created |`
5. Run [[sk-inc-sync]]

# Output

- New increment file in `Mesh/Increments/` with status `open`

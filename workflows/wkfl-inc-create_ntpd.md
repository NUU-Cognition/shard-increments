This workflow belongs to the Increments shard. Ensure you have [[init-inc]] in context before continuing.

# Workflow: Create Increment with Notepad

Open a new loop and immediately start a linked notepad for brainstorming its context and scope.

# Input

- (Optional) Increment name — defaults to a placeholder like "Exploration"
- (Optional) Initial brainstorming question

# Actions

## Stage 1: Create Increment

1. Find current checkpoint (highest `X.0`)
2. Find next increment number (highest `N + 1`, skipping `A`)
3. Create the increment using [[tmp-inc-increment-v0.2]] with:
   - `increment`: `"X.N"`
   - Name: user-provided or "Exploration"
   - Status: `open`
   - `opened`: today's date
   - Context: "See linked notepad for brainstorming"
   - Scope: minimal placeholder (to be filled after brainstorming)
4. Add log entry: `| YYYY-MM-DD | X.N | Created with linked notepad for brainstorming |`
5. Run [[sk-inc-sync]]

Present the created increment to the user. Once confirmed, proceed to Stage 2.

## Stage 2: Start Notepad

1. Get next notepad number: `flint helper type newnumber Notepad`
2. Start a notepad using [[wkfl-ntpd-start]]:
   - Topic: "Increment X.N - Brainstorming" (or user-provided topic)
   - Add `increment` field in notepad frontmatter linking to the new increment
   - Initial message: user-provided question, or "What should this increment focus on? What's the context and scope?"
3. Update the increment's Related Documents section to link to the notepad
4. The notepad workflow takes over — conversation continues there

# Output

- New increment in `open` state with placeholder content
- New notepad in `active` state linked to the increment
- Conversation started in notepad for brainstorming scope

# Guidelines

- The increment name can be refined later after brainstorming
- Keep the initial increment minimal — the notepad is where exploration happens
- Once brainstorming is complete, use [[wkfl-ntpd-finish]] to extract conclusions back into the increment

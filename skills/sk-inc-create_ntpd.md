# Skill: Create Stream with Notepad

Create a placeholder stream increment and immediately start a linked notepad for brainstorming its context and scope.

# Actions

1. Find current checkpoint (highest X.0.0)
2. Find next stream number (highest N + 1)
3. Get next notepad number using `flint helper type newnumber Notepad`
4. Create the stream using @tmp-inc-stream with:
   - Version: `X.N.0` (next available)
   - Name: "Exploration" or user-provided placeholder
   - Status: `active`
   - Context: "See linked notepad for brainstorming"
   - Scope: Leave minimal (to be filled after brainstorming)
5. Create linked notepad using @wkfl-ntpd-start:
   - Topic: "Increment X.N.0 - Brainstorming"
   - Add `increment` field in frontmatter linking to the new stream
   - Initial message: "What should this increment focus on? What's the context and scope?"
6. Update the stream's Related Documents section to link to the notepad
7. Add log entry: "Created with linked notepad for brainstorming"
8. Run @sk-inc-sync

# Output

- New stream increment in `active` state with placeholder content
- New notepad in `active` state linked to the increment
- Conversation started in notepad for brainstorming scope

# Guidelines

- The increment name can be refined later after brainstorming
- Keep the initial increment minimal — the notepad is where exploration happens
- Once brainstorming is complete, use @wkfl-ntpd-finish to extract conclusions back into the increment

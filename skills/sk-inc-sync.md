This skill belongs to the Increments shard. Ensure you have [[init-inc]] in context before continuing.

# Skill: Sync

Validate all increment files, dashboard, and loop health.

# Input

- None (operates on all increment files and the dashboard)

# Actions

1. The dashboard at `Mesh/(Dashboard) Increments.md` uses DataviewJS and is self-updating via queries against `#inc/increment` and `#inc/checkpoint` tags
2. Verify the dashboard file exists and its DataviewJS code is intact
3. If the dashboard has been manually edited or corrupted, restore it from [[inst-inc-dashboard.md]] in the shard's `install/` folder
4. Scan all increment files in `Mesh/Increments/` for inconsistencies:
   - Missing `increment` field
   - Missing or invalid `status` (must be `open`, `closed`, or `deprecated`)
   - Missing tags (`#inc/increment` or `#inc/checkpoint`)
   - Missing `checkpoint` link (for non-checkpoint increments)
   - Missing `opened` date
5. Report loop health:
   - Count of open loops
   - Any open loops older than 30 days (flag as potentially stale)
6. Report any data inconsistencies to user

# Output

- Dashboard verified or restored
- Increment files validated
- Loop health summary reported
- Any data inconsistencies reported to user

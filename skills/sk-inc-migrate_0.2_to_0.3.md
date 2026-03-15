This skill belongs to the Increments shard. One-time migration from v0.2.0 to v0.3.0.

# Skill: Migrate 0.2.0 → 0.3.0

Migrate all existing increment files and their references across the Mesh to the new format.

# Changes

| Before (0.2.0) | After (0.3.0) |
|-----------------|---------------|
| Version `X.N.0` | Version `X.N` |
| Tag `#inc/stream` | Tag `#inc/increment` |
| Status `active` | Status `open` |
| Status `completed` | Status `closed` |
| Template `tmp-inc-stream-v0.1` / `tmp-inc-stream` | Template `tmp-inc-increment-v0.2` |
| Template `tmp-inc-checkpoint-v0.1` | Template `tmp-inc-checkpoint-v0.2` |
| Template `tmp-inc-adhoc-v0.1` | Template `tmp-inc-adhoc-v0.2` |
| Location `Mesh/Types/Increments/` | Location `Mesh/Increments/` |
| Filename `(Increment) X.N.0 - Name.md` | Filename `(Increment) X.N - Name.md` |

# Actions

## Step 1: Content replacements in increment files

In all files under `Mesh/Types/Increments/`:

```bash
# Tags
sed -i '' 's/"#inc\/stream"/"#inc\/increment"/g' *.md

# Status
sed -i '' 's/^status: active$/status: open/' *.md
sed -i '' 's/^status: completed$/status: closed/' *.md

# Templates
sed -i '' 's/\[\[tmp-inc-stream-v0\.1\]\]/[[tmp-inc-increment-v0.2]]/g' *.md
sed -i '' 's/\[\[tmp-inc-stream\]\]/[[tmp-inc-increment-v0.2]]/g' *.md
sed -i '' 's/\[\[tmp-inc-checkpoint-v0\.1\]\]/[[tmp-inc-checkpoint-v0.2]]/g' *.md
sed -i '' 's/\[\[tmp-inc-adhoc-v0\.1\]\]/[[tmp-inc-adhoc-v0.2]]/g' *.md

# Version format in increment: field — drop trailing .0
sed -i '' -E 's/^increment: "([0-9]+\.[0-9A]+)\.0"$/increment: "\1"/' *.md

# Headings — drop trailing .0
sed -i '' -E 's/^# \(Increment\) ([0-9]+\.[0-9A]+)\.0/# (Increment) \1/' *.md
```

## Step 2: Update wikilinks across entire Mesh

Find all `(Increment) X.N.0` patterns in wikilinks and references across the Mesh and drop the trailing `.0`:

```bash
# For each increment file, replace old name pattern with new name pattern
# across all .md files in Mesh/
find Mesh/ -name "*.md" -exec sed -i '' -E \
  's/\(Increment\) ([0-9]+\.[0-9A]+)\.0/\(Increment\) \1/g' {} +
```

## Step 3: Rename increment files

```bash
# Rename each file to drop .0 from version
for f in Mesh/Types/Increments/\(Increment\)\ *.md; do
  newname=$(echo "$f" | sed -E 's/\(Increment\) ([0-9]+\.[0-9A]+)\.0/\(Increment\) \1/')
  mv "$f" "$newname"
done
```

## Step 4: Move to new location

```bash
mkdir -p Mesh/Increments/
mv Mesh/Types/Increments/*.md Mesh/Increments/
rmdir Mesh/Types/Increments/
```

## Step 5: Verify

- Grep for any remaining `.0` version patterns in Mesh
- Grep for any remaining `#inc/stream` tags
- Grep for any remaining `status: active` or `status: completed` in increment files
- Confirm all files are in `Mesh/Increments/`

# Output

- All increment files migrated to new format and location
- All wikilinks updated across the Mesh
- Zero stale references remaining

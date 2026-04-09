# memory-status

Memory health audit skill. Generates a staleness report for all Obsidian project memory files — shows last update dates, line counts, and flags stale or bloated files.

## Install

```bash
cp -r skills/dev/memory-status ~/.claude/skills/memory-status
```

## Invoke

```
/memory-status
```

## What it does

Scans all `.md` files in `Claude Memory/`, extracts frontmatter dates, and generates a report showing:

- File health status (OK / Stale / Very Stale / Bloated)
- Days since last update per project file
- Line counts to flag files approaching the 150-line compression threshold
- Active Context and Last Session from the Index
- Infrastructure status (which skills are installed, hooks configured)

## Example output

```
## Project Files Health

| File | Updated | Age | Lines | Status | Health |
|------|---------|-----|-------|--------|--------|
| ShipX.md | 2026-04-07 | 2d | 74 | Active | OK |
| Gloria.md | 2026-03-20 | 20d | 58 | Pending | Stale |
```

## Notes

- Read-only — does not modify any files
- Run periodically to catch stale memory before it causes drift

## Author

Darelle Gochuico · Dev

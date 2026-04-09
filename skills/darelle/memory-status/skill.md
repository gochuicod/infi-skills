---
name: memory-status
description: Show a staleness report for all project memory files. Displays last update dates, file sizes, line counts, and flags stale or bloated files. Use to audit the health of your Obsidian memory system.
disable-model-invocation: true
---

# Memory Status — System Health Report

Show the health of the entire Obsidian memory system at a glance.

## Step 1: Scan All Memory Files

Read the directory listing and metadata for every file in:
```
/Users/gochuicod/Documents/2nd Brain/gochuicod/Claude Memory/
```

For each `.md` file, extract:
- Filename
- `updated` date from YAML frontmatter
- `tags` from frontmatter
- Total line count (for bloat detection)
- Whether the project is marked active, pending, or on-hold in the Index

## Step 2: Load the Index

Read `Claude Memory Index.md` to get:
- The current Active Context
- The Last Session details
- The ecosystem table (to know which projects are active)

## Step 3: Build the Status Report

Generate a comprehensive table:

```
# Memory System Status Report
Generated: YYYY-MM-DD

## Active Context
[current active context from Index]

## Last Session
[last session summary from Index]

## Project Files Health

| File | Updated | Age | Lines | Status | Health |
|------|---------|-----|-------|--------|--------|
| ShipX.md | 2026-03-17 | 2d | 89 | Active | OK |
| Gloria.md | 2026-03-05 | 14d | 72 | Pending | Stale |

## Health Summary

- Total files: [N]
- Healthy: [N] files (updated within 14 days)
- Stale: [N] files (14-30 days old)
- Very Stale: [N] files (30+ days old)
- Bloated: [N] files (>150 lines, need consolidation)
- Overall health: [Good / Needs Attention / Action Required]

## Recommendations
- [List specific actions]
```

## Step 4: Check Skills & Hooks

Also report on the memory infrastructure — which skills are installed, whether hooks are configured, whether MEMORY.md is loaded.

## Rules
- This is a read-only command — it reports but does not modify anything
- Keep the output concise but complete

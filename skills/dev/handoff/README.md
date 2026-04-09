# handoff

Session memory handoff skill. Saves session progress to Obsidian vault at the end of every productive session so the next session starts with full context.

## Install

```bash
cp -r skills/dev/handoff ~/.claude/skills/handoff
```

## Invoke

```
/handoff [optional notes]
```

## What it does

1. Analyzes the current session — completed work, files created/updated, decisions made
2. Updates `Claude Memory Index.md` — Active Context + Last Session sections
3. Updates the relevant project memory file
4. Surfaces cacheable patterns to `Cache/Patterns/`
5. Commits and pushes the Obsidian vault to GitHub

## Example inputs

```
/handoff
→ Auto-generates full session handoff

/handoff finished CCP mock pipeline wiring, deferred real API phase
→ Incorporates custom notes into the handoff
```

## Notes

- Requires Obsidian vault at `/Users/gochuicod/Documents/2nd Brain/`
- Requires `mcp__obsidian__obsidian_update_note` and `mcp__smart-connections__lookup` tools
- Run before ending every productive Claude Code session

## Author

Darelle Gochuico · Dev

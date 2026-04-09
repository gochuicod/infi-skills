---
name: handoff
description: Update Obsidian memory at the end of a session. Auto-generates the Last Session handoff, updates Active Context, and refreshes the relevant project file(s). Use before ending any productive session.
argument-hint: "[optional notes]"
---

# Session Handoff Protocol

Save session progress to Obsidian memory so the next session starts exactly where this one left off.

## Step 1: Analyze the Session

Review the current conversation to identify:
- **Completed work** — features built, files created/modified, research done, proposals written
- **Files created** — new files added (with paths)
- **Files updated** — existing files modified (with paths)
- **Deferred items** — things discussed but not done (with reason: blocked, out of scope, waiting on X)
- **Next actions** — what should happen next session
- **Decisions made** — architectural choices, tool selections, approach decisions

If `$ARGUMENTS` is provided, incorporate those notes into the handoff.

Then run a semantic lookup to surface related vault notes that may need updating:
```
mcp__smart-connections__lookup(query: "<project or topic of this session>", limit: 5)
```
Use the results to catch any related project files, reference docs, or context notes beyond the primary project file. If the project isn't immediately clear from the conversation, use the lookup to identify it.

## Step 2: Update the Claude Memory Index

Read the current Index:
```
/Users/gochuicod/Documents/2nd Brain/gochuicod/Claude Memory/Claude Memory Index.md
```

Update TWO sections:

### Active Context (replace entirely)
Write 2-3 lines capturing:
- What's currently in focus / the immediate priority
- What's next after that
- Any blockers or waiting items

Include today's date: `## Active Context (updated YYYY-MM-DD)`

### Last Session (replace entirely)
Write a structured handoff:
```markdown
## Last Session (YYYY-MM-DD)
- Completed: [bullet list of what was done]
- Created: [new files with relative paths]
- Updated: [modified files with relative paths]
- Deferred: [what wasn't done and why]
- Decisions: [any notable decisions made]
- Next action: [what the next session should start with]
```

## Step 3: Update the Project File

If work was done on a specific project, update that project's Obsidian memory file:
```
/Users/gochuicod/Documents/2nd Brain/gochuicod/Claude Memory/<ProjectName>.md
```

**Before writing, run a staleness check:**
1. Read the file's `updated` frontmatter date
2. Count the file's total lines
3. Apply these rules:
   - If `updated` date is >30 days ago OR file is >80 lines: consolidate entries older than 60 days into a `## History (compressed)` section **before** appending new content
   - History entry format: `- YYYY-MM-DD: [1-sentence summary of what was done that session]`
   - Keep the last 2 sessions' entries in full detail; compress everything older into one-liners
   - Remove any known issues/bugs that were fixed this session
4. Record any stale files in the Step 6 report (see format below)

Follow the save rules:
- Save WHAT and WHY, skip HOW (unless surprising)
- One line per feature/change
- **Always** set the `updated` date in frontmatter to today's date (YYYY-MM-DD). This is critical for the tiered staleness system — without it, the project file will be flagged as stale on every handoff.
- If wiring changed, update the Wiring (compact) section

## Step 4: Update Claude Code Memory (if needed)

If any feedback, user preferences, or reference info was learned this session, update the relevant file in:
```
~/.claude/projects/-Users-gochuicod-Documents-InfiGroup/memory/
```

Only update if something genuinely new was learned — don't duplicate what's already there.

## Step 4b: Surface Cacheable Patterns

Scan the session for non-obvious solutions worth caching. Promote to `Claude Memory/Cache/Patterns/` if ANY of:
- Solution took multiple attempts or was counterintuitive
- Pattern is a library/tool/API quirk (bot detection, version gotcha, obscure flag, workaround for a known bug)
- Reusable across projects (not tied to one codebase's specifics)

**Format:** `Cache/Patterns/YYYY-MM-DD_short-kebab-slug.md` with frontmatter `tags: [cache, pattern, <lib>]`, `created:`, `topic:`, `projects: [...]`, `libs: [...]`. Body: **Problem**, **Solution**, **Why it works**, minimal code shape, **Applies when**.

## Step 5: Backup to GitHub

After all Obsidian files are updated, commit and push the vault to GitHub:

```bash
cd "/Users/gochuicod/Documents/2nd Brain"
git add -A
git commit -m "chore: session handoff $(date +%Y-%m-%d)"
git push
```

## Rules
- Keep the handoff concise — future Claude reads this at session start
- Use absolute dates (2026-03-19), never relative ("today", "yesterday")
- Don't save low-level details (CSS tweaks, line-by-line fixes)
- Don't save things already captured in git history
- If no meaningful work was done, say so — don't fabricate a handoff
- Token budget: project files should stay under ~80 lines (~1000 tokens). If a handoff would push the file over, consolidate before writing.

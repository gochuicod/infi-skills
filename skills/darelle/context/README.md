# context

Project context loader. Reads the Obsidian memory file for a named project mid-session — gotchas, current state, active tickets, key decisions, and codebase slices.

## Install

```bash
cp -r skills/dev/context ~/.claude/skills/context
```

## Invoke

```
/context [project-name]
/context [project-name] [slice]
```

Valid slices: `components`, `wiring`, `api`, `schema`, `env`, `all`

## What it does

- Reads the project's Obsidian memory file and surfaces gotchas, current state, and decisions
- Detects project from CWD if no args given
- With a slice arg, reads the targeted `Codebase/<Project>/<slice>.md` file for structural context

## Example inputs

```
/context CCP
→ Loads Content Calendar Platform memory file

/context Arka wiring
→ Loads Codebase/Arka/wiring.md for pipeline wiring context

/context
→ Auto-detects project from current working directory
```

## Author

Darelle Gochuico · Dev

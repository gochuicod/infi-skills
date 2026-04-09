# obsidian-markdown

Obsidian Flavored Markdown reference skill. Covers wikilinks, embeds, callouts, frontmatter properties, comments, and other Obsidian-specific syntax extensions.

## Install

```bash
cp -r skills/dev/obsidian-markdown ~/.claude/skills/obsidian-markdown
```

## Invoke

```
/obsidian-markdown
```

## What it does

Activates a reference mode for creating and editing `.md` files in Obsidian. Ensures Claude uses:

- `[[wikilinks]]` for internal vault links (not standard Markdown links)
- `> [!callout-type]` syntax for callouts
- Correct YAML frontmatter format with `tags`, `aliases`, `cssclasses`
- `%%hidden%%` comment syntax
- `==highlighted text==` for highlights
- `![[embed]]` for embedding other notes, images, or PDFs

## When to use

- Writing or editing Obsidian vault notes
- Creating project memory files for the Claude Memory system
- Any `.md` file that will be opened in Obsidian

## Author

Darelle Gochuico · Dev

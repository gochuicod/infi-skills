# defuddle

Web page content extractor. Uses the Defuddle CLI to strip navigation, ads, and clutter from web pages and return clean markdown — saving significant tokens compared to raw WebFetch.

## Install skill

```bash
cp -r skills/dev/defuddle ~/.claude/skills/defuddle
```

## Install Defuddle CLI (required)

```bash
npm install -g defuddle
```

## Invoke

This skill activates Claude's behavior when given a URL to read. Instead of using WebFetch (which returns full HTML), Claude will use:

```bash
defuddle parse <url> --md
```

## What it does

- Extracts main article/doc content from any standard web page
- Outputs clean markdown (no nav, ads, footers, sidebars)
- Reduces token usage by 60-80% vs raw HTML fetching
- Works on documentation sites, blog posts, articles, GitHub pages

## Example inputs

```
Read this docs page: https://drizzle.team/docs/...
→ Runs defuddle parse <url> --md and returns clean content

/defuddle
→ Reminds Claude to use defuddle for URL analysis
```

## Author

Darelle Gochuico · Dev

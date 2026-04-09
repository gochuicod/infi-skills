# fullstack-expertise

InfiGroup full-stack reference skill for Darelle. Covers Figma-to-code translation, base_system architecture, design tokens, animation patterns, responsive design, and backend patterns.

## Install

```bash
cp -r skills/dev/fullstack-expertise ~/.claude/skills/fullstack-expertise
```

## Invoke

```
/fullstack-expertise [frontend | backend | figma | all]
```

## What it does

Activates a senior full-stack developer persona tuned to InfiGroup's stack (Next.js 16, Tailwind, Shadcn UI, Drizzle, Supabase). Covers:

- **frontend** — design tokens, Tailwind layout patterns, component conventions, animation
- **backend** — withApi pipeline, Drizzle patterns, caching, auth, email, observability
- **figma** — Auto-layout → CSS mapping, reading designs accurately, token extraction
- **all** — full reference (default)

## Example inputs

```
/fullstack-expertise figma
→ Translating a Figma card component to pixel-perfect React

/fullstack-expertise backend
→ Adding a new API route with rate limiting and Zod validation

/fullstack-expertise
→ Full reference for any InfiGroup Next.js work
```

## Author

Darelle Gochuico · Dev

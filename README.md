# infi-skills

Shared AI skills and agents for the InfiGroup team. Single source of truth for reusable AI workflows across marketing, content, strategy, and development.

## Who This Is For

| Team | What's here for you |
|------|---------------------|
| **Marketing** | Content briefs, caption writers, hashtag generators, campaign analysis |
| **Strategy** | Competitive research, audience segmentation, insight summarizers |
| **Dev** | Code review, architecture review, debugging workflows |
| **Design** | Moodboards, visual direction briefs, brand consistency checks, Figma prompt helpers |
| **All teams** | Any validated Claude Code skill or AI agent prompt ready to share |

## Structure

```
infi-skills/
├── skills/
│   ├── marketing/    # Marketing-specific skills
│   ├── content/      # Content creation and editing skills
│   ├── strategy/     # Strategy and research skills
│   ├── design/       # Design workflow skills
│   └── dev/          # Development workflow skills
└── agents/
    ├── marketing/    # Marketing agents (social, email, calendar)
    ├── content/      # Content generation agents
    └── design/       # Design direction and visual brief agents
```

## How to Use a Skill in Claude Code

1. Copy the skill folder into `~/.claude/skills/<skill-name>/`
2. Invoke it in any Claude Code session with `/<skill-name>`

```bash
cp -r skills/marketing/content-brief ~/.claude/skills/content-brief
```

## How to Use a Standalone Agent

Skills in `agents/` are self-contained prompts. Copy the prompt directly into Claude, ChatGPT, or any AI tool.

## Contributing a Skill

1. Create your skill folder: `skills/<category>/<skill-name>/`
2. Add a `skill.md` with your prompt (see template below)
3. Add a `README.md` describing what it does and example inputs/outputs
4. Open a pull request

### Skill File Template

```markdown
---
name: your-skill-name
description: One sentence — what does this skill do?
author: Your Name
team: marketing | content | strategy | design | dev
version: 1.0.0
---

# Your Skill Name

[Skill prompt here]
```

## Naming Convention

- Lowercase, hyphen-separated: `content-brief`, `hashtag-generator`
- Prefix with team if ambiguous: `mkt-campaign-planner`, `dev-code-review`

## Guidelines

- **Test before submitting** — run at least 3 times on real inputs
- **One skill per folder** — keep skills focused and single-purpose
- **Include examples** — add sample inputs/outputs in the README
- **No secrets** — never include API keys, passwords, or client data

## Team Contacts

| Team | Contact |
|------|---------|
| Design | Josh |
| Marketing | Kim Montejo |
| Dev | Darelle Gochuico |

---

> Built for InfiGroup · [infi-brain.vercel.app](https://infi-brain.vercel.app)

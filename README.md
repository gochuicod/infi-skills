# infi-skills

Shared AI skills and agents for the InfiGroup team. Single source of truth for reusable AI workflows across marketing, content, strategy, and development.

## Who This Is For

| Person | Role | What's here |
|--------|------|-------------|
| **Darelle** | Dev | Full-stack skills, session memory, project context, web extraction |
| **Kim** | Marketing | Content briefs, caption writers, hashtag generators, campaign analysis, strategy |
| **Josh** | Design | Moodboards, visual direction briefs, brand consistency checks, Figma prompt helpers |
| **All** | Any role | Any validated Claude Code skill or AI agent prompt ready to share |

## Structure

```
infi-skills/
├── skills/
│   ├── darelle/          # Darelle's Claude Code skills
│   ├── kim/              # Kim's skills
│   │   ├── content/      # Content creation skills
│   │   └── strategy/     # Strategy and research skills
│   └── josh/             # Josh's design skills
└── agents/
    ├── kim/              # Kim's agents
    │   └── content/      # Content generation agents
    └── josh/             # Josh's design agents
```

## How to Use a Skill in Claude Code

1. Copy the skill folder into `~/.claude/skills/<skill-name>/`
2. Invoke it in any Claude Code session with `/<skill-name>`

```bash
cp -r skills/darelle/fullstack-expertise ~/.claude/skills/fullstack-expertise
```

## How to Use a Standalone Agent

Skills in `agents/` are self-contained prompts. Copy the prompt directly into Claude, ChatGPT, or any AI tool.

## Contributing a Skill

1. Create your skill folder: `skills/<your-name>/<skill-name>/`
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

## Contributors

| Person | Role |
|--------|------|
| Darelle Gochuico | Dev |
| Kim Montejo | Marketing |
| Josh | Design |

---

> Built for InfiGroup · [infi-brain.vercel.app](https://infi-brain.vercel.app)

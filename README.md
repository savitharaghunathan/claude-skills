# Claude Code Skills

Custom skills (slash commands) for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Skills

| Skill | Command | Description |
|-------|---------|-------------|
| **Managing ADRs** | `/managing-adrs` | Create and update Architecture Decision Records — format, numbering, status lifecycle, and when a decision is worth recording |

## Installation

Clone this repo into your Claude Code skills directory:

```sh
git clone https://github.com/savitharaghunathan/claude-skills.git ~/.claude/skills
```

Skills are automatically picked up by Claude Code from `~/.claude/skills/*/SKILL.md`.

## Usage

In a Claude Code session, invoke any skill with its slash command:

```
/managing-adrs
```

Each skill is a directory containing a `SKILL.md` file with YAML frontmatter (name, description) and markdown instructions.

## License

Apache-2.0

---

Assisted by [Claude Code](https://claude.com/claude-code)

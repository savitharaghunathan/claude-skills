# Claude Code Skills

Custom skills (slash commands) for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Skills

| Skill | Command | Description |
|-------|---------|-------------|
| **Commit & Push** | `/commit-push` | Selectively stage files, commit with sign-off, and push to the current branch |
| **Detailed Plan** | `/detailed-plan` | Create a comprehensive technical design document with background, current state, proposal, design, implementation plan, testing plan, and security implications |
| **Explain Code** | `/explain-code` | Explain code with visual diagrams and analogies |
| **Explain Project** | `/explain-project` | Get a structured overview of a project's purpose, tech stack, and architecture |
| **New Branch** | `/new-branch` | Create a new branch after syncing upstream/main to origin/main via rebase |
| **Review Output** | `/review-output` | Critically review AI-generated output by surfacing hidden risks, rejected alternatives, and areas of low confidence |

## Installation

Clone this repo into your Claude Code skills directory:

```sh
git clone https://github.com/savitharaghunathan/claude-skills.git ~/.claude/skills
```

Skills are automatically picked up by Claude Code from `~/.claude/skills/*/SKILL.md`.

## Usage

In a Claude Code session, invoke any skill with its slash command:

```
/commit-push
/detailed-plan <describe what to plan>
/explain-code
/explain-project
/new-branch feature/my-feature
/review-output
```

## Structure

```
skills/
  commit-push/SKILL.md
  detailed-plan/SKILL.md
  explain-code/SKILL.md
  explain-project/SKILL.md
  new-branch/SKILL.md
  review-output/SKILL.md
```

Each skill is a directory containing a `SKILL.md` file with YAML frontmatter (name, description) and markdown instructions.

## License

Apache-2.0

---

Assisted by [Claude Code](https://claude.com/claude-code)

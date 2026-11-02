---
name: explain-project
description: Gives a comprehensive overview of the current project — its purpose, structure, tech stack, and how the pieces fit together. Use when opening a new codebase or when the user asks "what is this project?" or "explain this repo."
---

Analyze the current project and produce a clear, structured overview. Use the tools available to explore the codebase before answering — do not guess.

## Steps

1. **Identify the project root** — look for package.json, Cargo.toml, go.mod, pyproject.toml, Makefile, or similar manifest files to determine the language and framework.
2. **Read the README** if one exists, but do not just parrot it back. Synthesize your own understanding.
3. **Scan the directory structure** to understand how the code is organized.
4. **Identify key entry points** — main files, app bootstrapping, route definitions, CLI entry points.
5. **Spot the core patterns** — MVC, microservices, monorepo, event-driven, etc.

## Output Format

### What this project does
One paragraph. Plain language. What problem does it solve and for whom?

### Tech stack
A short table or bullet list: language, framework, database, key libraries, build tools.

### Project structure
An ASCII tree of the top-level directories with one-line descriptions of what each contains.

### Architecture overview
An ASCII diagram showing how the major components connect — services, data flow, APIs, external dependencies.

### Key entry points
List the 3-5 most important files a new developer should read first, with a one-line explanation of each.

### Development workflow
How to install dependencies, run the project locally, and run tests — pulled from actual config files, not guessed.

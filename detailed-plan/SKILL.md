---
name: detailed-plan
description: Creates a comprehensive technical design document with background, current state, proposal, design, implementation plan, testing plan, and security implications. Use when planning non-trivial features, system changes, or architectural decisions that need thorough analysis before implementation.
---

Create a detailed technical design document by systematically researching and writing each section. Do not skip sections or produce shallow content — every section must be grounded in actual codebase analysis.

## Input

This skill accepts an optional topic argument describing what to plan. Examples:

- `/detailed-plan add OAuth2 support to the API`
- `/detailed-plan migrate from PostgreSQL to CockroachDB`
- `/detailed-plan` (no argument — will ask what to plan)

The argument text, if provided, is available as `$ARGUMENTS`.

## Process

### Phase 1: Gather Context

Before writing anything, research the codebase and problem space:

1. **Clarify scope** — If `$ARGUMENTS` was provided, use it as the topic and skip asking "what are we planning?" Instead, ask only narrowing questions:
   - Are there constraints or requirements already decided?
   - Who are the stakeholders or consumers of this change?

   If no argument was provided, also ask what problem we are solving.

   Ask one round of focused questions. Do not over-interrogate.

2. **Research the codebase** — Use the Task tool with `subagent_type=Explore` to understand:
   - The relevant modules, services, and data flows
   - Existing patterns that the proposal should follow
   - Any prior attempts or related code

3. **Research externally if needed** — Use WebSearch or Context7 to look up:
   - Best practices for the approach being considered
   - Known pitfalls or security advisories
   - Framework-specific guidance

### Phase 2: Write the Document

Produce a markdown document with all seven sections below. Write to a file at the path `docs/plans/YYYY-MM-DD-detailed-<topic>.md` (create the `docs/plans/` directory if it does not exist). Use today's date.

Add YAML frontmatter:

```yaml
---
title: <Descriptive Title>
type: detailed-plan
date: YYYY-MM-DD
status: draft
---
```

#### Section 1: Background

Explain **why** this work is being considered. Cover:
- The business or technical motivation
- Relevant history — what led to this point
- Links to related issues, RFCs, or prior discussions if known

This section answers: *Why are we talking about this?*

#### Section 2: Current State

Describe **what exists today**. Be specific:
- Relevant architecture, components, and data flows (use ASCII diagrams)
- Key files and entry points with paths and line references
- Current limitations, pain points, or failure modes
- Metrics or evidence of the problem if available

This section answers: *What do we have right now, and what's wrong with it?*

#### Section 3: Proposal

State **what you propose to do** in clear, direct terms:
- A concise summary of the change (2-3 sentences)
- Goals: what success looks like
- Non-goals: what is explicitly out of scope
- Key decisions and their rationale

This section answers: *What are we going to do about it?*

#### Section 4: Design

Describe **how** the proposal will work at a technical level:
- Architecture and component diagrams (ASCII)
- Data models, schemas, or API contracts that change
- Interaction flows for key scenarios
- How this integrates with existing systems
- Trade-offs considered and why this design was chosen over alternatives

List at least two alternative approaches that were considered and explain why they were rejected.

This section answers: *How will it work?*

#### Section 5: Implementation Plan

Break the work into **ordered, concrete steps**:
- Group steps into logical phases (e.g., Phase 1: Data layer, Phase 2: API, Phase 3: UI)
- For each step, list the specific files to create or modify
- Call out dependencies between steps
- Identify what can be done in parallel
- Flag any migrations, feature flags, or rollout considerations

Each step should be small enough that a developer can pick it up and execute without further planning.

This section answers: *What do we do first, second, third?*

#### Section 6: Testing Plan

Define **how the change will be verified**:
- Unit tests: what functions/modules need test coverage and key cases
- Integration tests: what workflows or cross-component interactions to test
- Edge cases and error scenarios to cover
- Performance or load testing if relevant
- Manual verification steps or QA checklist
- Rollback verification: how to confirm a rollback is clean

This section answers: *How do we know it works?*

#### Section 7: Security Implications

Analyze **security impact** honestly. Cover:
- Authentication and authorization changes
- Data exposure: does this change what data is accessible and to whom?
- Input validation and sanitization requirements
- Secrets, credentials, or API key handling
- OWASP Top 10 relevance (SQLi, XSS, CSRF, SSRF, etc.)
- Dependency risks from new libraries
- If there are no material security implications, say so explicitly and explain why

This section answers: *What could go wrong from a security perspective?*

### Phase 3: Review

After writing the document:

1. Re-read each section and verify claims against actual code — do not leave unverified statements.
2. Run the `/review-output` skill mentally: identify the hardest decision, rejected alternatives, and lowest-confidence areas. Add a brief **Open Questions** section at the end listing unresolved items.
3. Present the completed document path to the user and summarize the key proposal and any open questions that need their input.

## Principles

- **Grounded in code**: Every architectural claim should reference actual files and line numbers.
- **Honest about unknowns**: Flag uncertainty rather than papering over it.
- **Concrete over abstract**: Prefer specific file paths, function names, and data shapes over vague descriptions.
- **Minimal viable scope**: The proposal should solve the stated problem without gold-plating.
- **Diagrams over prose**: When a diagram can replace a paragraph, use the diagram.

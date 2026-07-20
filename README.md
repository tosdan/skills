# Software Development Agent Skills

Personal, reusable workflows for AI coding agents working on software projects.
The catalog follows the open [Agent Skills specification](https://agentskills.io/specification)
and is installable with the [`skills` CLI](https://github.com/vercel-labs/skills).

## Catalog

### `plan-software-decisions`

Use for complex or uncertain work that needs a durable decision record before
implementation. The skill inspects the repository, creates or resumes a
canonical work plan, discusses one decision at a time, and derives acceptance
scenarios before code changes begin.

```text
Use $plan-software-decisions to analyze this migration, create a persistent
plan, and guide me through one decision at a time.
```

### `pair-program-in-checkpoints`

Use for incremental implementation when the work should proceed through small,
reviewable checkpoints. The skill proposes one checkpoint, waits for approval,
implements only that scope, verifies it, and then proposes the next one.

```text
Use $pair-program-in-checkpoints to translate this plan into code one approved
checkpoint at a time.
```

### Using both

The skills cover consecutive phases without depending on each other:

1. Use `plan-software-decisions` while important behavior or architecture is
   still unresolved.
2. Use `pair-program-in-checkpoints` after the relevant decisions and acceptance
   scenarios are stable enough to implement.

Install either skill independently when only one phase is needed.

## Repository layout

```text
skills/
  <skill-name>/
    SKILL.md
    agents/        # optional agent-facing metadata
    scripts/       # optional executable helpers
    references/    # optional documentation loaded on demand
    assets/        # optional templates and static resources
```

Each skill is self-contained. Its directory name and the `name` field in
`SKILL.md` must match and use lowercase kebab-case.

## Use this catalog

List the available skills from a local checkout:

```sh
npx skills@latest add . --list
```

After publishing the repository on GitHub, list or install skills with:

```sh
npx skills@latest add <owner>/<repository> --list
npx skills@latest add <owner>/<repository> --skill <skill-name>
npx skills@latest add <owner>/<repository> --skill '*'
```

Use `-g` for a user-level installation and `-a <agent>` to target a specific
agent, such as `codex` or `claude-code`.

## Add a skill

Create or move each skill into `skills/<skill-name>/`. At minimum it needs:

```markdown
---
name: skill-name
description: Describe what the skill does and the situations in which an agent should use it.
---

# Skill Name

Instructions for the agent.
```

Keep detailed material outside `SKILL.md` and link to it with paths relative to
the skill directory. Do not add a README to every skill: repository-level usage
and installation guidance belongs here, while agent instructions belong in
`SKILL.md`.

Before committing, confirm discovery with:

```sh
npx skills@latest add . --list
```
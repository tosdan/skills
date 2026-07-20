# Agent Skills

Personal, reusable skills for AI coding agents, organized as an installable
catalog for the open [Agent Skills specification](https://agentskills.io/specification)
and the [`skills` CLI](https://github.com/vercel-labs/skills).

## Repository layout

```text
skills/
  <skill-name>/
    SKILL.md
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
the skill directory. Before committing, confirm discovery with:

```sh
npx skills@latest add . --list
```


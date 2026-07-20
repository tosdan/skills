# Repository Guidelines

This repository is a catalog of portable Agent Skills.

## Structure

- Put every publishable skill in `skills/<skill-name>/`.
- Keep each skill self-contained; do not depend on files from another skill.
- Require `SKILL.md`. Add `scripts/`, `references/`, and `assets/` only when the
  skill needs them.
- Do not place templates or incomplete skills under `skills/`, because the CLI
  may discover and publish them.

## SKILL.md

- Follow the Agent Skills specification at https://agentskills.io/specification.
- Use lowercase kebab-case for the directory and `name`; they must match.
- Make `description` state both what the skill does and when it should trigger.
- Keep instructions portable across agents. Isolate agent-specific behavior and
  document it explicitly when it cannot be avoided.
- Keep `SKILL.md` concise. Put detailed documentation in `references/` and link
  to it directly with relative paths.
- Avoid experimental frontmatter fields unless the skill genuinely requires
  them and their reduced portability is intentional.

## Verification

- Run or otherwise exercise scripts added to a skill.
- From the repository root, run `npx skills@latest add . --list` and confirm all
  intended skills are discovered with no duplicates.
- Review skill scripts and instructions for unsafe commands, hidden network
  access, secrets, and machine-specific absolute paths before committing.


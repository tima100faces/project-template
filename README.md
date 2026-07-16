# project-template

Skeleton for a new project. The working process lives in `CLAUDE.md`.

## Starting a project

1. Copy the contents of this repo into the new project (without `.git` and `global/`).
2. Fill in the header of `CLAUDE.md`: name, level, stack, start command, checks.
3. Pick the **complexity level** — it decides what to keep:
   - **Lightweight** — keep `CLAUDE.md` + `docs/STATUS.md`, delete the rest of `docs/`.
   - **Project** — keep everything.
   - **Critical** — keep everything, plus a separate plan for each risky change.
4. `git init`, first commit.

## Global rules

`global/CLAUDE.md` holds the rules that apply to every project. It lives here so it
does not drift between machines. Install it on each machine:

```bash
cp global/CLAUDE.md ~/.claude/CLAUDE.md
```

Claude Code loads it automatically at the start of every session, in every project.
Do not copy it into individual projects.

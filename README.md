# project-template

Skeleton for a new project. The working process lives in [`AGENTS.md`](AGENTS.md); the operational
part — in `docs/`.

## Starting a project

1. Copy the contents of this repo into the new project, without `.git` and `global/`.
2. Fill in the header of `AGENTS.md`: name, level, stack, where it runs, start command, checks,
   what must not be touched without asking, licence.
3. Pick the **complexity level** — it decides what to keep:
   - **Lightweight** — `AGENTS.md` + `docs/STATUS.md` + `docs/PITFALLS.md`, delete the rest of `docs/`.
   - **Project** — keep everything.
   - **Critical** — keep everything, plus a separate plan for each risky change.
4. `git init`, first commit.

## What is where

| File | Purpose |
|---|---|
| `AGENTS.md` | working agreement: roles, levels, task format, git rules, verification, session start and end |
| `CLAUDE.md` | one-line pointer to `AGENTS.md`, for tools that still look for that name |
| `docs/STATUS.md` | mandatory: what works, what is in progress, what is broken, next action |
| `docs/PRODUCT.md` | goal, who the user is, MVP boundaries, main scenarios |
| `docs/PLAN.md` | current stage, next tasks, done, parked, risks |
| `docs/DECISIONS.md` | decisions that are expensive to reverse |
| `docs/PITFALLS.md` | what broke, why, how not to step on it again |
| `.gitignore` | secrets, virtualenvs, dependencies, databases |

**Everything about the project lives in the project folder.** An external wiki keeps the map and the
story; it never keeps a second copy of these files.

## Global rules

`global/CLAUDE.md` holds the rules that apply to every project. It lives here so it does not drift
between machines. Install it on each machine under the name the agent there actually reads:

```bash
cp global/CLAUDE.md ~/.claude/CLAUDE.md
```

Do not copy it into individual projects.

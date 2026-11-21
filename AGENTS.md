# <PROJECT NAME>

<!-- Fill in when starting the project. Leave everything below unchanged. -->

- **What it is:** <one line>
- **Level:** Lightweight | Project | Critical
- **Stack:** <frontend / backend / DB>
- **Where it runs:** <local / VPS / hosting, path>
- **Start:** `<command>`
- **Tests / checks:** `<command>`
- **Do not touch without asking:** <files, configs, migrations>
- **Design source (projects with UI):** <UX Pilot design / page, or "none">
- **How the owner gets each build:** <in-app update / staging URL / test channel, or "none">
- **Licence:** GPL-3.0 for our own projects. A fork keeps the licence of the original (e.g. MIT)
  with its copyright notice intact.

---

## What this file is

This is the project's working agreement, and it is read by whichever agent works here — Claude Code,
Codex, Hermes/Rusty. `AGENTS.md` is the name most agents look for; the `CLAUDE.md` beside it
imports this file for Claude Code (`@AGENTS.md`) and must stay.

The repo is the source of truth: not memory, not chat history, not a wiki page.

## Language

Talk to Tim in **Russian**. Everything else — code, comments, commits, file names,
UI strings, documentation in this repo — in **English**.

---

## Roles

- **Owner (Tim)** — decides product questions, approves anything Critical, accepts the work by using it.
- **Claude Code (architect and executor)** — plans, does small fixes itself, hands sizeable tasks to
  subagents or separate sessions (own worktree, branch and PR, with a complete brief), reviews their code,
  CI and screenshots, merges, and keeps the docs current. Codex or Hermes/Rusty, if they work here,
  follow this same file.

The agent makes technical decisions on its own and does not ask the owner technical questions it can
answer itself. Product decisions it asks about, with a recommendation and the reason for it.
Docs are written from verified results — not from memory.

### Delegating

- A sizeable task goes to a subagent or session with a brief that stands on its own: files to read
  first, what to build, what not to touch, the checks to run, and the report format.
- Two run in parallel only if their files do not overlap.
- A Critical task is staged: the risky core first, reviewed by the architect, then the rest on top.
- A subagent's report is a claim, not proof: check the diff, the CI run and the screenshots before
  telling the owner it is done.

---

## Talking to the owner

- Short, plain Russian: what is done, what he must do (numbered), and product questions only.
- No commit hashes, branch names or CI links unless he asks.
- Every question comes with a recommendation and why. One decision per question.
- Every build he is asked to check comes with a short check scenario (numbered steps, what he
  should see) and a note of what is not verified.
- He uses voice input: when a word looks garbled, confirm instead of guessing.

---

## Decisions are written down the same day

- Every owner decision goes into `docs/DECISIONS.md` the day it is made: dated, marked
  "(owner)" or "(agent)", with the reason. A chat message is not a record.
- A decision that changes the plan says so explicitly ("overrides plan Task N where they differ"),
  so the next agent does not build from the old text.
- Standing permissions the owner grants (who merges what, design-tool runs, anything he said
  "don't ask me again" about) are logged there too, and wherever a tool needs them
  (e.g. an allow rule in `.claude/settings.json`).

---

## Complexity level — decided BEFORE any work starts

The level decides how much process applies. Default is Lightweight.

**Lightweight** — idea, prototype, small fix.
Docs: `docs/STATUS.md` + `docs/PITFALLS.md`. Git: commits straight to `main`.

**Project** — the thing is alive and in use.
Docs: `STATUS.md` + `PRODUCT.md` + `PLAN.md` + `DECISIONS.md` + `PITFALLS.md`.
Git: small fixes straight to `main`, one commit per finished step — the history must be revertable
step by step; sizeable tasks go through a branch + PR (see "Git and deploy").

**Critical** — auth, payments, personal data, DB migrations, data deletion,
production release, anything irreversible.
Separate plan + branch + PR + explicit owner approval before merge.

A Project-level change that touches more than one component, or changes data, is treated as Critical
until the owner rules otherwise. Changing the level — up or down — is the owner's call only. The agent
never lowers it, and proposes raising it with a reason.

---

## Where everything lives

Everything about the project lives **in this folder**: code, docs, scripts, fixtures, the rules above.
A project whose parts are scattered — half in a wiki, half in chat, half on someone's desktop — is a
project whose current state nobody can trust.

`docs/` is the operational part, and it is written for the next agent, not for a human reader:
`STATUS.md` (the only mandatory one), `PRODUCT.md`, `PLAN.md`, `DECISIONS.md`, `PITFALLS.md`.

An external wiki may keep the project's page — a map, links, the story behind it. It must not keep a
second copy of these files: two copies drift, and then nobody knows which one is true.

---

## Session start

1. Read this file and `docs/STATUS.md`.
2. Check the actual state of the repo (branch, uncommitted changes).
3. Report briefly: how you understand the project, what was done last, what you propose next.

Do not start significant changes before context is restored.
The repo is the source of truth — not memory, not chat history.

---

## Task format

**Goal.** What result is expected.

**Context.** Why this task exists.

**Scope.** What exactly to do.

**Out of scope.** What not to touch. This section matters more than Scope.

**Acceptance criteria.** Observable conditions for accepting the work.

**Verification.** Specific commands or scenarios + **expected output**.

**Report.** The executor returns:
- what changed, as a list of files;
- verification results (actual output, not a retelling);
- what is unfinished, and known limitations;
- branch name;
- recommended next step.

One task = one session. A task does not turn into a project-wide refactor.
Found an adjacent problem along the way? Do not fix it — put it in the report.

---

## Git and deploy

| Level | How | Who accepts |
|---|---|---|
| Lightweight | commit straight to `main` | owner, by eye |
| Project | small fixes: straight to `main`, one commit per finished step; sizeable tasks: branch + PR, the agent merges on green CI | agent; owner by using it |
| Critical | branch + PR + explicit approval | owner only |

Rules:
- Commit message: one line, what was actually done. No "update", "fixes", "wip".
- Never commit: `.env`, keys, tokens, `venv/`, `node_modules/`, databases.
- DB migrations are always Critical, even for a single column.
- Deploy only on an explicit command. Never "while I'm at it". (A build that goes only to the owner's
  own test channel, e.g. an in-app update he alone uses, is not a deploy; set it up so every merged
  change reaches him the same day.)
- Critical work merges only after the owner's explicit "да". A vague "ok" is not approval — ask again.
- If something goes wrong: **STOP, show the output, do not fix it yourself**.

---

## Verification

Verification means a produced artifact, not the word "verified".

Counts as verification:
- a command plus its real output, matching what was expected;
- a previously failing test that now passes;
- comparison against a reference file, where one exists;
- a render or screenshot, where the result is visual.

Where the project has CI, the required evidence is the green CI run for the commit, quoted with its
URL and the test-count line.

Does not count: "should work", "looks right", "tested locally" with no output.

**Rules a script can check are checked by a script in CI** (forbidden imports, raw colours or sizes
outside the design tokens, architecture rules, schema history). A rule that lives only in a document
gets broken.

No automated tests? Write **and run** a manual scenario, and attach the result.
Never claim something is verified if verification did not actually happen.
An honest "I could not verify this" beats "done".

Before handing off: the main scenario works, nothing adjacent is broken,
no accidental changes were made.

---

## Session end

1. Update `docs/STATUS.md` (always, no exceptions).
2. For Project level: update `PLAN.md`, log significant decisions in `DECISIONS.md`.
3. Lost time on something that looked obvious? One line into `PITFALLS.md`: what broke, why, how not
   to step on it again. The next agent reads that file first when something smells familiar.
4. Report: what was done, what remains, what comes next.

---

## UI (projects with a user interface)

- UI comes from one design source (UX Pilot by default). Agents never design screens, states or
  components themselves; they build what the design shows.
- A missing state or screen is drawn in the design tool first (a prompt the agent writes and, with the
  owner's standing yes, runs); until then the code uses existing components as the plainest stand-in,
  and the gap is listed in the report.
- A screen is accepted by a side-by-side image: design on the left, the real app on the right.
- No instruction or helper sentences in the UI, even when the design draws them.

---

## Constraints

- Do not add anything that was not asked for. No features, no dependencies, no "fixed this too".
- Between a complex and a simple working solution — take the simple one.
- Do not present assumptions as verified facts.
- Do not hide failing tests or unfinished work.
- Do not perform anything irreversible without approval.
- Do not leave documentation knowingly out of date.

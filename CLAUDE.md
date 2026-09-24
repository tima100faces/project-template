# Rules moved to AGENTS.md

This project's working rules live in [`AGENTS.md`](AGENTS.md). Tools from Anthropic now read
`AGENTS.md` first, so the rules are kept in exactly one file — two copies drift and then nobody
knows which one is true.

If your tool only looks for `CLAUDE.md`: read `AGENTS.md` at the start of the session and treat it as
this file.

---
name: docs
description: "Project docs system: sync codebase to docs, research what to build next, or retro on past work."
argument-hint: <sync|research|retro> [topic or doc path]
---

# Docs

Project memory system. Pick an action:

- **`/docs sync`** — Map codebase to references, update roadmap statuses. Use `/docs sync structure` to only rebuild the folder layout.
- **`/docs research`** — Discover and formalize what to build next into a roadmap doc
- **`/docs retro`** — Analyze logs and decisions over a time period for patterns, wins, and recurring issues

## Core Model

- `.docs/reference/` = **what exists in the codebase**. Sync writes here.
- `.docs/roadmap/` = **what should exist but doesn't yet**. Research writes here. Organized by status.
- `.docs/decisions/` = decision records. Any command can create these.
- `.docs/logs/` = chronological record of all agent work and decisions. Any command writes here after completing substantial work. Exists so every dev in a shared repo can see what agents did and why.
- `.docs/retros/` = retrospective analyses. Retro writes here. Separate from logs so analytical summaries don't get buried in work history.

## Rule Levels

- **Required** — Must be followed.
- **Recommended** — Strong default guidance.

## Global Rules (required)

1. **Command contract** — only `sync`, `research`, `retro`.
2. **Docs root + folder contract** — this skill manages `.docs/` with only these top-level folders:
   - `.docs/reference/`
   - `.docs/roadmap/`
   - `.docs/decisions/`
   - `.docs/logs/`
   - `.docs/retros/`
   - Inside `.docs/reference/`, use:
     - `features/`
     - `architecture/`
     - `conventions/`
     - `runbooks/`
     - `pitfalls/`
   - Inside `.docs/roadmap/`, use status folders:
     - `proposed/` — ideas formalized, not started
     - `in-progress/` — actively being worked on
     - `completed/` — fully shipped
     - `archived/` — superseded, rejected, or deprioritized
3. **Naming + date rules**
   - `reference/*` → `kebab-case.md`
   - `roadmap/**`, `decisions/` → `YYYY-MM-DD-kebab-case.md`
   - `logs/` → `YYYY-MM-DD-kebab-task-name.md` — one log per day per scope of work. Same-day iterations on the same work append as sections; a new day always starts a new file.
   - Dates must be zero-padded ISO 8601: `YYYY-MM-DD`.
4. **Append-only history** — for `decisions/` and `retros/`, add new files instead of rewriting history. For `logs/`, same-day iterations on the same work append sections to the existing file (see rule 5).
5. **Log after every complete piece of work** — whenever an agent finishes substantial work (pushing a PR, completing a sync, finalizing a research recommendation, shipping a feature), log what was done. **One log file per day per scope of work:**
   - Search today's files in `.docs/logs/` (matching today's `YYYY-MM-DD` prefix) for an existing log matching this work.
   - If a same-day log exists, **append a new `---` divider and section** to it.
   - If no same-day log exists, create `.docs/logs/YYYY-MM-DD-kebab-task-name.md`.
   - Never append to a log from a previous day — always create a new file.
   - Each section captures what was done, decisions made, and rationale — so every developer can reconstruct what agents did and why.
6. **Roadmap status lifecycle** — track status by moving docs between roadmap folders:
   - `proposed/` → `in-progress/` → `completed/`
   - Items that won't be built go to `archived/` with a note explaining why (superseded, rejected, deprioritized)
   - Every roadmap doc must still have a `## Status` line for quick context (e.g., `Proposed`, `In Progress`, `Completed (YYYY-MM-DD)`, `Archived — superseded by [link]`)
7. **Policy files** — if `AGENTS.md` and/or `CLAUDE.md` exist, keep their docs-memory guidance aligned.
8. **Path containment** — all file operations must target paths within the project root. Reject any path containing `..` segments or symlinks that resolve outside the project. All `.docs/` operations must stay within `.docs/`.
9. **No secrets in docs** — never write credentials, API keys, tokens, connection strings, or other secrets into any `.docs/` file. If sensitive values are encountered during scanning, reference them generically (e.g., "uses environment variable for DB auth") without including the actual value.
10. **Conflict behavior** — if repository conventions conflict with these defaults, do not rewrite conventions silently. Report the mismatch and ask the user before changing direction.

## Global Rules (recommended)

- Prefer focused, single-purpose docs.
- Prefer updating existing docs before creating new ones.
- Keep docs concrete and scannable.
- Treat code as ground truth; avoid full schema dumps in docs.

---

## Command References

Each command's full specification lives in its own file under `references/`:

- **`sync`** — [references/sync.md](references/sync.md)
- **`research`** — [references/research.md](references/research.md)
- **`retro`** — [references/retro.md](references/retro.md)

Match the first argument to the corresponding reference file and follow its instructions.

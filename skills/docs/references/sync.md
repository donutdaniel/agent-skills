## sync

Fully map the codebase into `.docs/reference/`. Also update roadmap statuses for shipped work.

**Completeness requirement:** Sync must resolve ALL findings before completing. Do not defer undocumented systems, stale docs, or partial docs to "a future sync." Every implemented system must have a corresponding reference doc when sync finishes. If the scope is large, batch the work — but finish it in this run.

### 1. Ensure structure

Runs every sync to keep the folder structure intact. Idempotent — creates what's missing, leaves everything else alone. Never overwrites or removes existing files or folders.

1. Ensure all folders exist (create any that are missing):

```
.docs/
├── README.md
├── reference/
│   ├── features/
│   ├── architecture/
│   ├── conventions/
│   ├── runbooks/
│   └── pitfalls/
├── roadmap/
│   ├── proposed/
│   ├── in-progress/
│   ├── completed/
│   └── archived/
├── decisions/
├── logs/
└── retros/
```

2. If `.docs/README.md` is missing, create it with this exact content:

````
# .docs/

Project memory system. Code is ground truth — these docs capture context that code alone doesn't convey.

## Structure

```
.docs/
├── README.md              # This file
├── reference/             # What exists in the codebase
│   ├── features/          # Feature-level docs
│   ├── architecture/      # System architecture
│   ├── conventions/       # Code patterns and required practices
│   ├── runbooks/          # Operational how-tos
│   └── pitfalls/          # Known gotchas and their fixes
├── roadmap/               # What should exist but doesn't yet
│   ├── proposed/          # Ideas formalized, not started
│   ├── in-progress/       # Actively being worked on
│   ├── completed/         # Fully shipped
│   └── archived/          # Superseded, rejected, or deprioritized
├── decisions/             # Decision records (append-only)
├── logs/                  # Chronological work history (append-only, per-task)
└── retros/                # Retrospective analyses (append-only)
```

## Conventions

- **`reference/*`** uses `kebab-case.md`
- **`roadmap/**`**, **`decisions/`** use `YYYY-MM-DD-kebab-case.md`
- **`logs/`** uses `YYYY-MM-DD-kebab-task-name.md` per-task files
- Dates are zero-padded ISO 8601: `YYYY-MM-DD`
- `logs/`, `retros/`, and `decisions/` are **append-only** — add new files, don't rewrite history
- Roadmap status lifecycle: `proposed/` → `in-progress/` → `completed/` (or → `archived/`)
- Code is ground truth — docs point to code, not the other way around

## Commands

Managed via `/docs` skill:
- `/docs sync` — Map codebase to references, update roadmap statuses
- `/docs research` — Discover what to build next, formalize into roadmap
- `/docs work` — Execute a roadmap item, then update references
- `/docs retro` — Look back over a time period for patterns and insights
````

3. If `AGENTS.md` and/or `CLAUDE.md` exist but lack docs guidance, add this exact section:

```
## Project Memory

`.docs/` is the project memory system — see `.docs/README.md` for conventions. Use the `/docs` skill to manage it (`sync`, `research`, `work`, `retro`). After substantial work (PR, feature, refactor), log what you did and why to `.docs/logs/YYYY-MM-DD-task-name.md`.
```

### 2. Audit docs vs code

1. Read `.docs/README.md`, then review all files under `.docs/reference/`, `.docs/roadmap/`, `.docs/decisions/`, and `.docs/logs/`.
2. Use repository search to check what exists in code (schema, services, routes, UI, jobs, APIs).
3. Compare every reference doc against current code for accuracy.
4. Identify implemented systems that have no reference doc.
5. Check roadmap items — have any been shipped? Should any move between status folders?

### 3. Classify findings

Use this taxonomy:

- **Stale** — reference doc is materially incorrect vs current code
- **Partial** — reference doc exists but is missing significant implemented behavior
- **Undocumented** — important implemented system has no reference doc
- **Roadmap shipped** — roadmap item has been implemented and should move to `completed/`
- **Obsolete** — reference doc describes something that no longer exists in the codebase (removed feature, resolved runbook, fixed pitfall); delete it

### 4. Sync (required — must resolve ALL findings, no deferral)

Resolve every finding discovered in steps 2-3. Do not skip, defer, or deprioritize any item:

- **Stale docs** — update to match current code.
- **Partial docs** — fill in the missing sections from code evidence.
- **Undocumented systems** — create new reference docs (`features/`, `architecture/`, `conventions/`, `runbooks/`, or `pitfalls/` as appropriate).
- **Shipped roadmap items** — move the roadmap doc to `completed/` and update its `## Status` line.
- **Obsolete docs** — delete reference docs for things that no longer exist in the codebase.
- Add or update `conventions/`, `runbooks/`, and `pitfalls/` entries when repository evidence exists.

If a change would alter repository conventions or policy direction, report the mismatch and ask before making that change.

### Output Contract (required)

When `/docs sync` completes, return all of:

1. **Bootstrap status** — `created` or `already present`
2. **Coverage table** with this exact header:

```
| System | Doc | Status | Action taken |
|--------|-----|--------|--------------|
```

3. **Summary** — counts by status (stale fixed, partial filled, undocumented created, roadmap updated)
4. **Docs changes made** — list updated/created/moved paths, or `none`
5. **Log entry** — create `.docs/logs/YYYY-MM-DD-sync.md` capturing what was synced, key findings, and decisions

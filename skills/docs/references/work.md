## work

Execute a roadmap item. Build it, then close the loop in docs.

### 1. Understand task

- If user gives a roadmap doc path, read it first
- If user gives a description, find the related roadmap doc in `.docs/roadmap/`
- If no roadmap doc exists, ask: should we create one first (`/docs research`) or proceed directly?
- If ambiguous, clarify scope briefly
- Move the roadmap doc to `in-progress/` if it's still in `proposed/`

### 2. Gather implementation context

- Read the roadmap doc and any related reference docs
- Inspect existing code patterns in touched areas
- Check project rules and conventions

### 3. Build

- Plan first if scope is large (using your environment's planning workflow)
- Implement the change
- Run verification commands

### 4. Close the loop

After implementation is complete:

- **Update reference docs** — create or update `.docs/reference/` docs to reflect the new code (features, architecture, conventions, runbooks, pitfalls as appropriate)
- **Update roadmap doc** — move to `completed/` and update `## Status` to `Completed (YYYY-MM-DD)`, or move to `completed/` with `Partially Completed (YYYY-MM-DD)` and notes on what remains
- **Log entry** — append to an existing log for the same scope of work (see Global Rule 5), or create `.docs/logs/YYYY-MM-DD-kebab-task-name.md` if none exists. Captures what was done, key decisions made, and why

### Output Contract (required)

When `/docs work` completes, return all of:

1. **Scope delivered**
2. **Code files changed**
3. **Verification** — commands + pass/fail
4. **Docs updated** — list reference/roadmap/log paths, or `none`
5. **Follow-ups** — remaining work or `none`

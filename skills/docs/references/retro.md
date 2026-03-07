## retro

Look back at logs, decisions, and roadmap history over a period of time to surface patterns and insights.

### 1. Determine period

A retro always covers a specific time window. Determine the period:

- If user specifies a range (e.g., "last 2 weeks", "March", "since 2024-01-01"), use that
- If user specifies a topic but no range, use the full history for that topic. Topic filtering searches only within `.docs/` — scan filenames first for quick hits, then search file content within `.docs/logs/`, `.docs/retros/`, `.docs/decisions/`, and `.docs/roadmap/` for keyword matches
- If neither is specified, default to **since the last retro** — find the most recent `.docs/retros/YYYY-MM-DD.md` (or `.docs/retros/YYYY-MM-DD-<topic>.md` if scoped to a specific topic) and cover everything after that date
- If no previous retro exists, **ask the user** what period to cover

When filtering by period, use the date prefixes on filenames (`YYYY-MM-DD-*`) to include only docs within the window.

### 2. Gather history

Read docs within the period from:

- `.docs/logs/` — work logs
- `.docs/decisions/` — decision records
- `.docs/roadmap/completed/` — items shipped during the period
- `.docs/roadmap/archived/` — items abandoned during the period
- `.docs/retros/` — read the most recent retro (if one exists) for context on prior concerns and actions

### 3. Analyze and write retro

Look at the gathered history and surface what's interesting. Organize findings into these sections:

- **Wins** — What went well, approaches worth repeating.
- **Concerns** — What didn't go well, what's fragile or being worked around.
- **Observations** — Trends, shifts, or patterns that aren't good or bad yet but worth tracking.
- **Actions** — Concrete next steps, what to do differently.

Use these exact words as section headers in the retro doc for consistency. Skip any section that has no signal. Follow the data — if the history points somewhere unexpected, follow that instead. Reference specific logs or decisions when it adds clarity, but keep it readable — don't turn every bullet into a citation dump.

Write the retro to `.docs/retros/YYYY-MM-DD.md` (or `.docs/retros/YYYY-MM-DD-<topic>.md` if scoped to a topic).

### Output Contract (required)

When `/docs retro` completes, return:

1. **Period covered** — date range and count of docs reviewed
2. **Summary** — key findings from each section
3. **Retro doc path**

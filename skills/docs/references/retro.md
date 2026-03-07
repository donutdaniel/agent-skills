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

### 3. Analyze through lenses

When the period contains **more than 15 logs**, spawn parallel subagents — one per lens — to analyze concurrently. Otherwise, work through them sequentially.

Skip any lens that has no signal:

**Work patterns** — What kind of work dominates?
- Categorize logs: feature, bugfix, refactor, debt paydown, docs, infrastructure
- Is the team building or firefighting? What's the ratio?

**Hotspots** — What areas keep getting touched?
- Identify files, systems, or domains that appear across multiple logs
- Repeated work in the same area signals something unresolved — a missing abstraction, unclear ownership, or chronic instability

**Decision drift** — Are decisions holding?
- Look for decisions that got revisited, reversed, or contradicted by later work
- Patterns here suggest missing context at decision time or changing constraints that weren't tracked

**Roadmap health** — How well do plans turn into shipped work?
- Ratio of completed vs archived items
- Items that sat in `proposed/` or `in-progress/` for a long time — what blocked them?
- Patterns in what gets abandoned (too ambitious, wrong timing, dependencies)

**Recurring pitfalls** — What keeps going wrong?
- Cross-reference logs for repeated issues, workarounds, or similar mistakes
- Check if existing pitfall docs cover these, or if new ones are needed

**Wins** — What worked well?
- Patterns that led to smooth, successful work
- Approaches worth promoting to conventions or repeating

### 4. Synthesize

Findings can be insights, observations, or recommendations — not everything needs an action item. An interesting pattern or a shift in what the team is working on is worth surfacing even if there's nothing to "do" about it.

When a finding does warrant a recommendation, cite the specific logs, decisions, or roadmap items that support it. Don't force recommendations where the evidence isn't there.

### Output Contract (required)

When `/docs retro` completes, return all of:

1. **Period covered** — date range of logs analyzed, total count of logs/decisions reviewed
2. **Findings table** with this exact header:

```
| Lens | Finding | Evidence | Takeaway |
|------|---------|----------|----------|
```

3. **Key takeaways** — the most interesting or impactful findings, whether insights or action items
4. **Retro doc** — create `.docs/retros/YYYY-MM-DD.md` (or `.docs/retros/YYYY-MM-DD-<topic>.md` if scoped to a specific topic) capturing the full analysis
5. **Follow-ups** — suggested next commands (e.g., `/docs research` for a surfaced issue, `/docs sync` if reference docs need updating)

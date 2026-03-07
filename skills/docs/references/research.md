## research

Discover what to build next and formalize it into a roadmap doc.

### 1. Scan for candidates

Work through these lenses. Not all will apply to every product — use what's relevant:

**Usage and behavior** — What are users actually doing?
- If analytics tools are available, check usage patterns, funnels, retention, and drop-off points
- Identify features that are heavily used (double down) vs unused (cut or rethink)

**Demand** — What are users asking for?
- Check issue trackers, feature request backlogs, and support channels for patterns
- Look for frequently requested capabilities or common complaints

**Pain** — What's broken or frustrating?
- Check `.docs/reference/pitfalls/` and `.docs/reference/runbooks/` for recurring operational pain
- Look at bug reports, incident history, and support escalations

**Strategy** — What's the current direction?
- Read `.docs/roadmap/` for existing plans and their statuses
- Read `.docs/reference/features/` for gaps, limitations, and natural next steps
- Consider business goals and priorities the user has communicated

**Landscape** — What's happening externally?
- Research competitors, adjacent tools, and market shifts if relevant
- Identify opportunities others are capitalizing on

**Technical opportunity** — What does the codebase reveal?
- Scan code for `TODO`, `FIXME`, `HACK`, stubs, and dead paths
- Identify tech debt that's actively slowing down development

**Vision** — What's possible that doesn't exist yet?
- What adjacent problems could we solve with what we've already built?
- What emerging capabilities or trends could we leverage?
- What would the product look like if we removed current constraints?
- What would make users say "I didn't know I needed this"?

Narrow to user-specified domain if provided.

### 2. Rank candidates

Rank by:

- impact (user value, pain reduction)
- readiness (how much groundwork already exists)
- size (`small`, `medium`, `large`)

### 3. Propose shortlist

Use this exact header:

```
| # | What | Why now | Size | Readiness | Exists | Missing |
|---|------|---------|------|-----------|--------|---------|
```

### 4. Formalize the chosen item

Once the user picks an item (or accepts the recommendation):

1. Create a roadmap doc at `.docs/roadmap/proposed/YYYY-MM-DD-slug.md`
2. Required sections:
   - Opening line (plain-language summary of the problem)
   - Status (`Proposed`)
   - Why (problem statement, evidence, user impact)
   - What (concrete scope, deliverables)
   - How It Fits In (relation to existing systems, dependencies)
   - Non-Goals (explicit scope boundaries)
   - Open Questions (unresolved decisions)
3. Add cross-links from related reference docs if useful

### Output Contract (required)

When `/docs research` completes, return all of:

1. **Shortlist table** (3-5 rows)
2. **Recommended item** (`#<n>` + one-sentence reason)
3. If formalized: **roadmap doc path**, **open questions**
4. **Next command** suggestion (`/docs work <path>` or another `/docs research` for a different domain)
5. **Log entry** — create `.docs/logs/YYYY-MM-DD-research-<topic>.md` capturing what was investigated, candidates considered, and the recommendation rationale

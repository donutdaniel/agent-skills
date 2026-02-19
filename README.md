# docs

Project memory system for AI coding agents. Keeps a `docs/` folder in sync with your codebase as a persistent knowledge base — capturing what exists (reference), what to build next (roadmap), decisions made, and work history.

## Install

```bash
npx skills add donutdaniel/agent-skills --skill docs
```

## Commands

| Command | What it does |
|---|---|
| `/docs sync` | Maps your codebase to `docs/reference/`, updates stale docs, creates missing ones, moves shipped roadmap items to completed |
| `/docs research` | Scans code, issues, and strategy to discover what to build next, then formalizes the chosen item into a roadmap doc |
| `/docs work <item>` | Builds a roadmap item, then closes the loop — updates reference docs, completes the roadmap entry, and logs the work |

## How it works

The skill manages a `docs/` folder in your project:

```
docs/
├── README.md
├── reference/        # What exists in the codebase
│   ├── features/
│   ├── architecture/
│   ├── conventions/
│   ├── runbooks/
│   └── pitfalls/
├── roadmap/          # What should exist but doesn't yet
│   ├── proposed/
│   ├── in-progress/
│   ├── completed/
│   └── archived/
├── decisions/        # Decision records
└── logs/             # Chronological work history
```

- **`sync`** audits every reference doc against current code, fixes stale/partial docs, creates docs for undocumented systems, and moves shipped roadmap items to `completed/`. It resolves everything in one run.
- **`research`** looks across usage patterns, user demand, pain points, strategy, competitive landscape, technical debt, and vision to propose a ranked shortlist of what to build. You pick one and it writes the roadmap doc.
- **`work`** reads a roadmap doc, builds the feature, then updates reference docs, moves the roadmap to completed, and appends a log entry.

## Compatibility

Works with any agent that supports the [Agent Skills standard](https://github.com/vercel-labs/skills) — Claude Code, Cursor, Copilot, Windsurf, OpenCode, and others.

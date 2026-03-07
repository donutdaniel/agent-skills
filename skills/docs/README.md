# docs

Project memory system for AI coding agents. Keeps a `.docs/` folder in sync with your codebase as a persistent knowledge base — capturing what exists (reference), what to build next (roadmap), decisions made, and work history.

## Install

```bash
npx skills add donutdaniel/agent-skills --skill docs
```

## Commands

| Command | What it does |
|---|---|
| `/docs sync` | Maps your codebase to `.docs/reference/`, updates stale docs, creates missing ones, moves shipped roadmap items to completed |
| `/docs research` | Scans code, issues, and strategy to discover what to build next, then formalizes the chosen item into a roadmap doc |
| `/docs work <item>` | Builds a roadmap item, then closes the loop — updates reference docs, completes the roadmap entry, and logs the work |
| `/docs retro` | Looks back over a time period to surface patterns, insights, and lessons from logs, decisions, and roadmap history |

## How it works

The skill manages a `.docs/` folder in your project:

```
.docs/
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
- **`retro`** looks back over a time period (defaulting to since the last retro) at logs, decisions, and completed/archived roadmap items. Surfaces patterns — what kind of work dominates, what areas keep getting touched, what decisions held or drifted, and what keeps going wrong. Findings can be insights or action items.

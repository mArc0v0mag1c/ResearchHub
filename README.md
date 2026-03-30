# ResearchHub

Cross-project researcher identity, shared skills, and knowledge hub. Works with [ResearchProjectTemplate](https://github.com/mArc0v0mag1c/ResearchProjectTemplate) and [ReadingProjectTemplate](https://github.com/mArc0v0mag1c/ReadingProjectTemplate).

## What This Is

A personal repo that bridges all your research and reading projects. ResearchHub owns:
1. **Your identity** --- profile, interests, lessons learned
2. **Shared skills** --- canonical copies that all projects symlink to
3. **Cross-project knowledge** --- methods inventory, digests, connections

```
ResearchHub/
├── profile.md                 Your researcher identity (user-curated)
├── interests.md               Evolving interests, cross-project themes
├── lessons.md                 Cross-project lessons learned
├── skills/                    *** CANONICAL shared skills ***
│   ├── paper-reader/          Read & discuss papers, generate notes
│   ├── method-tracker/        Track methods learned across projects
│   ├── research-junshi/       Research advisor — arXiv scans, idea digests
│   ├── zotero-paper-reader/   Fetch papers from Zotero, convert, analyze
│   └── mistral-pdf-to-markdown/ PDF-to-markdown OCR conversion
├── agents/                    *** CANONICAL shared agents ***
│   └── note-checker.md        Verify reading notes against source material
├── method-tracker/
│   └── methods.md             Structured inventory of methods learned
├── research-junshi/
│   ├── config.md              Venue search patterns, arXiv categories
│   └── digests/               Historical digest archive (append-only)
├── Brainstorm/
│   └── cross-project/         Cross-project connection digests
└── .claude/
    └── CLAUDE.md              Instructions for Claude in this repo
```

## Architecture

### Three Layers

| Layer | Role | Runs at | Owns |
|-------|------|---------|------|
| **ResearchHub** | Runtime hub | Always | Shared skills, profile, methods, lessons, digests |
| **Templates** | Creation-time scaffolding | Project setup | CLAUDE.md, folder structure, git hooks, type-specific skills |
| **Projects** | Data + symlinks | Always | Code, data, output, progress. Symlinks to Hub for shared skills |

### What lives where

**ResearchHub** (shared across all projects):
- `skills/paper-reader` --- reading & note-taking conventions
- `skills/method-tracker` --- method inventory management
- `skills/research-junshi` --- arXiv scanning, idea generation
- `skills/zotero-paper-reader` --- Zotero integration
- `skills/mistral-pdf-to-markdown` --- PDF OCR conversion
- `agents/note-checker.md` --- verify notes against sources

**ResearchProjectTemplate** (research-only):
- `progress-tracker` --- PROGRESS.md workflow
- `work-summary` --- working journal entries
- `pdf` --- local PDF manipulation
- Research-specific agents: code-reviewer, report-checker, results-summarizer, unit-tester, review-doc-commit

**ReadingProjectTemplate** (reading-only):
- No type-specific skills currently (all shared)

### Skill symlink structure

Every project's `.claude/skills/` contains symlinks:

```
SocialFin/.claude/skills/
├── paper-reader/       -> ~/vscodeproject/ResearchHub/skills/paper-reader/
├── method-tracker/     -> ~/vscodeproject/ResearchHub/skills/method-tracker/
├── research-junshi/    -> ~/vscodeproject/ResearchHub/skills/research-junshi/
├── zotero-paper-reader/ -> ~/vscodeproject/ResearchHub/skills/zotero-paper-reader/
├── mistral-pdf-to-markdown/ -> ~/vscodeproject/ResearchHub/skills/mistral-pdf-to-markdown/
├── progress-tracker/   (local, research-only)
├── work-summary/       (local, research-only)
└── pdf/                (local, research-only)
```

Update a skill in ResearchHub -> every project sees the change instantly.

## Setup

```bash
git clone https://github.com/mArc0v0mag1c/ResearchHub.git ~/vscodeproject/ResearchHub
```

Then edit `profile.md` and `interests.md` to describe your research identity.

Both templates' `create_project.sh` will check for ResearchHub and print setup instructions if it's missing.

## How It Connects

```
┌─────────────────────┐     ┌─────────────────────┐
│ Research Project A   │     │ Reading Project X    │
│  skills/ ───────────┼──┐  │  skills/ ───────────┼──┐
│  agents/ ───────────┼──┤  │  agents/ ───────────┼──┤
└─────────────────────┘  │  └─────────────────────┘  │
                         │                            │
┌─────────────────────┐  │  ┌─────────────────────┐  │
│ Research Project B   │  │  │ Reading Project Y    │  │
│  skills/ ───────────┼──┤  │  skills/ ───────────┼──┤
│  agents/ ───────────┼──┤  │  agents/ ───────────┼──┤
└─────────────────────┘  │  └─────────────────────┘  │
                         ▼                            ▼
                    ┌──────────────────────────────────┐
                    │          ResearchHub              │
                    │                                   │
                    │  skills/    agents/                │
                    │  profile.md    interests.md        │
                    │  methods.md   lessons.md           │
                    │  digests/     cross-project/       │
                    └──────────────────────────────────┘
```

- **Skills**: All projects symlink shared skills from `ResearchHub/skills/`
- **Agents**: Shared agents (note-checker) symlinked from `ResearchHub/agents/`
- **Per-project**: Each project saves digests to `Notes/Brainstorm/` and archives to `ResearchHub/research-junshi/digests/`
- **Cross-project**: When research-junshi detects connections between projects, it saves to `ResearchHub/Brainstorm/cross-project/`
- **Methods**: method-tracker appends to `ResearchHub/method-tracker/methods.md` from any project
- **Lessons**: Cross-project lessons go to `ResearchHub/lessons.md`

## Project Type Detection

Shared skills auto-detect the project type:

| Check | Project type | Status file | Extracted papers location |
|-------|-------------|-------------|--------------------------|
| `PROGRESS.md` exists | Research | `PROGRESS.md` | `Literature/Extracted/` |
| `READING-LOG.md` exists | Reading | `READING-LOG.md` | `Extracted/` |

## Global CLAUDE.md

Both templates install `~/.claude/CLAUDE.md` on first run --- a user-level config loaded in every Claude Code session with shared writing standards, workflow orchestration, and cross-project conventions.

## Rules

1. **Never modify `profile.md` or `interests.md` without user confirmation** --- these are user-curated
2. **Digests are append-only** --- never delete or overwrite past digests
3. **`methods.md` is append-only for new entries** --- proficiency and "Used in" fields can be updated
4. **`lessons.md` is append-only**
5. **Skills in ResearchHub are canonical** --- edit here, not in project copies

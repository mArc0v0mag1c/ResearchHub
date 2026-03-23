# ResearchHub

Cross-project researcher identity and skill-state hub. Works with [ResearchProjectTemplate](https://github.com/mArc0v0mag1c/ResearchProjectTemplate) and [ReadingProjectTemplate](https://github.com/mArc0v0mag1c/ReadingProjectTemplate).

## What This Is

A personal repo that bridges all your research and reading projects. Skills (research-junshi, method-tracker) running in any project read from and write to ResearchHub.

```
ResearchHub/
├── profile.md                 Your researcher identity (user-curated)
├── interests.md               Evolving interests, cross-project themes
├── lessons.md                 Cross-project lessons learned
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

## Setup

### Automatic (recommended)

ResearchHub is auto-created the first time you run `create_project.sh` in either template:

```bash
# From ResearchProjectTemplate
./create_project.sh MyProject

# Or from ReadingProjectTemplate
./create_project.sh MacroTheory
```

If `~/vscodeproject/ResearchHub/` doesn't exist, the script creates it with the full scaffold. If it already exists, it's left untouched.

### Manual

```bash
git clone https://github.com/mArc0v0mag1c/ResearchHub.git ~/vscodeproject/ResearchHub
```

Then edit `profile.md` and `interests.md` to describe your research identity.

## How It Connects

```
┌─────────────────────┐     ┌─────────────────────┐
│ Research Project A   │     │ Reading Project X    │
│  research-junshi ────┼──┐  │  research-junshi ────┼──┐
│  method-tracker  ────┼──┤  │  method-tracker  ────┼──┤
└─────────────────────┘  │  └─────────────────────┘  │
                         │                            │
┌─────────────────────┐  │  ┌─────────────────────┐  │
│ Research Project B   │  │  │ Reading Project Y    │  │
│  research-junshi ────┼──┤  │  research-junshi ────┼──┤
│  method-tracker  ────┼──┤  │  method-tracker  ────┼──┤
└─────────────────────┘  │  └─────────────────────┘  │
                         ▼                            ▼
                    ┌──────────────────────────────────┐
                    │          ResearchHub              │
                    │  profile.md    interests.md       │
                    │  methods.md   lessons.md          │
                    │  digests/     cross-project/      │
                    └──────────────────────────────────┘
```

- **Per-project**: Each project saves digests to `Notes/Brainstorm/` and archives to `ResearchHub/research-junshi/digests/`
- **Cross-project**: When research-junshi detects connections between projects, it saves to `ResearchHub/Brainstorm/cross-project/`
- **Methods**: method-tracker appends to `ResearchHub/method-tracker/methods.md` from any project
- **Lessons**: Cross-project lessons go to `ResearchHub/lessons.md`

## Global CLAUDE.md

Both templates install `~/.claude/CLAUDE.md` on first run — a user-level config loaded in every Claude Code session with shared writing standards, workflow orchestration, and cross-project conventions. Edit the "Who I Am" section to personalize it.

## Rules

1. **Never modify `profile.md` or `interests.md` without user confirmation** — these are user-curated
2. **Digests are append-only** — never delete or overwrite past digests
3. **`methods.md` is append-only for new entries** — proficiency and "Used in" fields can be updated
4. **`lessons.md` is append-only**

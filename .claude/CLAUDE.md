# ResearchHub

Cross-project researcher identity and skill-state hub.

## Purpose

This repo is the bridge between all your research and reading projects. Skills running in any project can read from and write to ResearchHub.

## Directory Guide

- `profile.md` — Your researcher identity: areas, projects, strengths, learning goals, preliminary results. Read by research-junshi across all projects. **Do not modify without user confirmation.**
- `interests.md` — Evolving research interests, cross-project themes, paper wish list. **Do not modify without user confirmation.**
- `Brainstorm/cross-project/` — Cross-project connection digests written by research-junshi when it detects links between projects.
- `research-junshi/config.md` — Global configuration: arXiv categories, target venues, deep scan venues.
- `research-junshi/digests/` — Historical archive of all research-junshi digests across projects. Append-only.
- `method-tracker/methods.md` — Structured inventory of methods and techniques learned. Append new entries; proficiency levels can be updated.
- `lessons.md` — Cross-project lessons learned. Append-only. When the self-improvement loop fires, ask the user whether the lesson is project-specific or global.

## Rules

1. **Never modify `profile.md` or `interests.md` without user confirmation** — these are user-curated.
2. **Digests are append-only** — never delete or overwrite past digests.
3. **`methods.md` is append-only for new entries** — existing entries' proficiency and "Used in" fields can be updated.
4. **New skills** that need cross-project state should create their own subfolder (following the `research-junshi/` and `method-tracker/` pattern).

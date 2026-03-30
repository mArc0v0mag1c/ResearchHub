---
name: method-tracker
description: Track methods and techniques learned from projects and readings. Scans Notes for method discussions, maintains structured inventory in ResearchHub. Trigger on "track method", "add method", "what methods do I know", "methods I know", "method inventory", "update methods", "learned methods", "method list".
---

# Method Tracker

Scans your Notes and papers for discussions of methods, techniques, and approaches. Builds and maintains a structured inventory at `~/vscodeproject/ResearchHub/method-tracker/methods.md`.

Designed to match your scholarly note-taking style --- extracts methods from comparative tables, theoretical grounding, logic chains, and code implementations.

---

## Configuration

- **Methods inventory**: `~/vscodeproject/ResearchHub/method-tracker/methods.md`
- **Scan locations**: determined by project type (see below)

---

## Project Type Detection

Detect the project type by checking what exists in the project root:

| Check | Project type | Scan locations |
|-------|-------------|----------------|
| `PROGRESS.md` exists | Research project | `Notes/*.md`, `Notes/**/*.md`, `Code/`, `Literature/Extracted/` |
| `READING-LOG.md` exists | Reading project | `Notes/*.md`, `Notes/**/*.md`, `Extracted/*.md` |

---

## When to Run

- User says "track method", "add method", "update methods", "what methods do I know", "method inventory"
- After completing a reading or analysis session --- suggest: "Want me to check for new methods to track?"
- User says "run method-tracker"

---

## What to Look For

1. **Explicit method names**: regression techniques (OLS, IV, GMM, DiD, RDD, synthetic control), estimators, algorithms, statistical tests
2. **Comparative tables**: tables contrasting multiple frameworks, approaches, or models
3. **Logic chains**: numbered steps describing how a technique works or why it produces certain results
4. **Theoretical grounding**: references to established frameworks ("following [Author]'s framework...")
5. **Testable predictions / Limitations**: sections discussing what a method can and cannot do
6. **Code implementations** (research projects): Python/R code blocks showing usage of specific packages or techniques
7. **Formulas and equations**: mathematical descriptions of estimators or models

---

## Workflow

### Step 1: Read current inventory
Read `~/vscodeproject/ResearchHub/method-tracker/methods.md` to know what's already tracked.

### Step 2: Scan Notes
Use Grep and Read to search `Notes/*.md` and `Notes/**/*.md` for method-related content. For each match, read surrounding context to understand:
- What method is being discussed?
- Where did the user learn it? (paper citations, project references)
- How deeply do they understand it? (reading about it, or applying it?)

### Step 3: Scan project-specific sources

**Research projects**: Scan `Code/` for import statements, applied statistical methods, models, algorithms. Also scan `Literature/Extracted/` for methods in papers. Code usage = "Applied" level evidence.

**Reading projects**: Scan `Extracted/*.md` for methods discussed in papers. Focus on method sections, theoretical frameworks, estimators, mathematical formulations. Cross-reference with `READING-LOG.md` to associate methods with their source papers. Methods from readings default to "Learning" level unless evidence of application exists.

### Step 4: Cross-reference against inventory
- Skip methods already tracked (unless new usage to report)
- For existing methods used in a new project: update "Used in" field
- For existing methods with new evidence of deeper understanding: consider upgrading proficiency

### Step 5: Present to user
Show findings with suggested entries:

```markdown
**Found: [Method Name]**
- Source: [where found --- file path and context]
- Suggested entry:
  - What: [description]
  - Source: [paper/project]
  - Proficiency: [Learning / Applied once / Comfortable / Fluent]
  - Category: [field]
```

**Always confirm with the user before appending.** Never silently modify methods.md.

### Step 6: Update inventory
After user confirmation, append new entries to `~/vscodeproject/ResearchHub/method-tracker/methods.md`:

```markdown
### [Method Name]
- **What**: [1-2 sentence description]
- **Source**: [Where learned --- project name, paper citation, or course]
- **Key reference**: [Paper/textbook with page numbers if applicable]
- **When added**: [Date]
- **Proficiency**: [Learning / Applied once / Comfortable / Fluent]
- **Used in**: [List of projects where applied]
- **Notes**: [Key insight, gotcha, or connection to other methods]
```

Place the entry under the appropriate category heading. If no matching category exists, create a new one.

### Step 7: Report upgrades
If a method was already tracked but evidence shows increased proficiency or new usage:
- Show the user the current entry and the new evidence
- Suggest the update (e.g., "Upgrade from 'Learning' to 'Applied once'?")
- Update after confirmation

---

## Proficiency Levels

- **Learning**: Read about it, understand the concept, haven't applied it yet
- **Applied once**: Used it in one project or exercise
- **Comfortable**: Used it across multiple projects, can implement without reference
- **Fluent**: Deep understanding, can teach it, know edge cases and limitations

---

## Integration with Research-Junshi

Research-junshi reads `methods.md` to generate better ideas:
- When it finds a paper using a method you know --- highlights the connection
- When it finds a method you don't know --- suggests adding it to learning goals
- Leverages your method strengths for cross-pollination ideas

---

## Tone

Be precise and factual when identifying methods. Match the user's scholarly style --- reference specific papers, page numbers, and project names. Don't inflate proficiency levels --- be honest about the difference between reading about a method and actually implementing it.

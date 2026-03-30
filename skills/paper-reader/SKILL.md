# Paper Reader & Note-Taking Skill

Read and discuss academic papers with the user, and produce structured reading notes.

## When to Use

Trigger on: "read paper", "let's read", "discuss paper", "paper notes", "reading notes", "take notes on", or when the user starts asking questions about a paper in `Literature/Extracted/`.

## Reference Routing

Load additional modules **on demand** based on the task:

| If the user asks for... | Load |
|---|---|
| LaTeX reading notes, `.tex` output | `latex-notes.md` |

Do NOT load reference files unless the task requires them.

## How to Discuss Papers

### Grounding

1. **Always read the extracted markdown first** (`Literature/Extracted/`) to ground yourself in the paper's actual content before answering.
2. **Cite precisely**: refer to the specific paragraph, page, figure, table, or equation. Use formats like "(para. 2, p. 12)", "(Table 3, p. 8)", "(Figure 2, p. 15)". Look both above and below the referenced content for context.
3. **Answer directly** --- lead with the substance, grounded in what the paper actually says.

### Separating Sources

4. **If the paper doesn't answer the question directly**, say so explicitly before providing your answer. Clearly separate what comes from the paper vs. what doesn't.
5. **External sources**: when the user asks for material beyond the paper, use only reliable sources --- top-university lecture slides, top-journal papers, or their companion slides. Always provide:
   - A direct web link to the source
   - A precise reference within that source (e.g., "Slide 14", "Section 3, para. 2, p. 8")

### Interaction Style

- Lead with the answer, not the reasoning
- Do not restate the user's question
- Do not speculate or use hedging language ("suggests", "likely", "appears to")
- If asked to compare across papers, ground each side in its own extracted text

## Companion Notes (Markdown)

When the user wants notes captured during discussion, create or update `Notes/<paper-name>.md`.

### File Structure

```markdown
# Author (Year) --- Title: Companion Notes

## 1. Short descriptive title

**Reference:** where in the paper (e.g., Abstract (p. 1); Section I (pp. 2--5))

Key quote or claim, then the unpacked logic chain or analysis with precise citations (page, paragraph).

## 2. Next topic

Same pattern. Each numbered section is one self-contained insight, argument, or brainstorm.
```

### Guidelines

- One file per paper, append new sections as discussion continues
- Each section needs a **Reference** line pointing to the paper
- Logic chains should be numbered steps with citations
- Brainstorms and cross-paper connections are welcome --- label them clearly
- Do not invent content beyond what the paper says; mark external commentary explicitly

## Reading Log

If the project has a `READING-LOG.md` or equivalent tracker (e.g., `PROGRESS.md`), update it when:
- Starting a new reading (add to Currently Reading)
- Finishing a reading (move to Completed with a one-liner takeaway)
- Discovering related papers to read later (add to Up Next)

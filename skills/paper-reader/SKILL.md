# Paper Reader & Note-Taking Skill

Read and discuss academic papers with the user, and produce structured reading notes.

## When to Use

Trigger on: "read paper", "let's read", "discuss paper", "paper notes", "reading notes", "take notes on", or when the user starts asking questions about a paper in `Literature/Extracted/`.

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

## LaTeX Reading Notes

When the user wants formal LaTeX notes, follow the draft-first workflow.

### Workflow

```
1. User specifies which paper/section
2. User provides: extracted markdown + annotations + key points to capture
3. Claude replies with a PLAIN TEXT DRAFT (not LaTeX) --- outlining content,
   flow, and key equations in readable form
4. User reviews the draft -> requests revisions
5. User approves: "yes, do latex" -> Claude writes the .tex code
6. User inspects live in VS Code (LaTeX Workshop auto-rebuilds on save)
7. User says "move on" -> next section
```

**Critical**: Do NOT generate LaTeX code until the user explicitly approves the draft.

### Content Structure

| Step | Purpose | Example |
|------|---------|---------|
| **Overview** | What is this paper about? Setting, contribution | "This paper studies optimal consumption under uncertainty..." |
| **Key Arguments** | Main theoretical/empirical arguments | "The authors show via Bellman equation that..." |
| **Technical Details** | Derivations, proofs, methods worth recording | "Starting from the FOC, substitute envelope condition..." |
| **Takeaways** | Key results, connections to other readings | "This generalizes the result from [other paper]..." |

### LaTeX Conventions

- Use `\usepackage{marcoreport}` for structure
- Direct quotes:
  ```latex
  \begin{quote}
  ``Exact text from the source'' \hfill (Author, Year, p.~12)
  \end{quote}
  ```
- Paraphrased content: inline reference (Author, Year, p.~15--17)
- Equations from source:
  ```latex
  \begin{equation}
  V(a) = \max_{c} u(c) + \beta V(a')  \tag{Source: eq.~3, p.~8}
  \end{equation}
  ```
- Use `remarkbox` for key insights and cross-paper connections
- Use `itemize` for cases, `enumerate` for sequential steps
- Time-subscripts preferred: $a_t, a_{t+1}, c_t^*$
- Starred variables for optima: $c_t^*$

### What NOT to Do

- Don't invent content beyond what was provided
- Don't add unnecessary caveats or hedging
- Don't create separate boxes when items can be nested
- Don't switch notation mid-section
- Don't generate the next section until explicitly told

## Reading Log

If the project has a `READING-LOG.md` or equivalent tracker (e.g., `PROGRESS.md`), update it when:
- Starting a new reading (add to Currently Reading)
- Finishing a reading (move to Completed with a one-liner takeaway)
- Discovering related papers to read later (add to Up Next)

## Available Environments from `marcoreport.sty`

| Command | Purpose |
|---------|---------|
| `\vct{x}` | Bold vector |
| `\mat{A}` | Bold matrix |
| `\RR` | Real numbers |
| `\EE` | Expectation |
| `\var` | Variance |
| `\argmin`, `\argmax` | Arg operators |

| Environment | Purpose |
|-------------|---------|
| `theorem`, `lemma` | Numbered theorems |
| `definition` | Numbered definitions |
| `remark` | Unnumbered remarks |
| `remarkbox[Title]` | Blue box for key insights |
| `mynote` (tcolorbox) | Gray note box |

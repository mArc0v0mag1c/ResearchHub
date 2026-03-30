# LaTeX Reading Notes — Reference Module

When the user wants formal LaTeX notes, follow the draft-first workflow.

## Workflow

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

## Content Structure

| Step | Purpose | Example |
|------|---------|---------|
| **Overview** | What is this paper about? Setting, contribution | "This paper studies optimal consumption under uncertainty..." |
| **Key Arguments** | Main theoretical/empirical arguments | "The authors show via Bellman equation that..." |
| **Technical Details** | Derivations, proofs, methods worth recording | "Starting from the FOC, substitute envelope condition..." |
| **Takeaways** | Key results, connections to other readings | "This generalizes the result from [other paper]..." |

## LaTeX Conventions

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

## What NOT to Do

- Don't invent content beyond what was provided
- Don't add unnecessary caveats or hedging
- Don't create separate boxes when items can be nested
- Don't switch notation mid-section
- Don't generate the next section until explicitly told

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

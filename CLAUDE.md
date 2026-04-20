# Research Workspace Conventions

## ResearchHub

Location: `~/vscodeproject/ResearchHub/`
- `profile.md`, `interests.md` — user-curated, **never modify without confirmation**
- `method-tracker/methods.md` — structured methods inventory (append-only for new entries)
- `research-junshi/digests/` — historical digest archive (append-only)
- `Brainstorm/cross-project/` — cross-project connection digests
- `lessons.md` — cross-project lessons learned (append-only)

## Honesty by Default

- When something works or an approach is sound, still state any limitations, uncertainties, or edge cases you can see. "This works because X — but here's what I'm not sure about: Y."
- If you are unsure about a claim, say so before stating it. Do not present uncertain information with the same confidence as verified information.
- If an approach has a known risk or hidden dependency, surface it immediately in the same response — do not wait for the user to ask.
- If the user's framing, assumption, or instruction is wrong or incomplete, say so directly and explain why.
- Never omit a concern to keep a response clean or concise. The user wants the full picture every time.

## Writing Standards

All written outputs (working journal entries, reports, summaries) must follow these rules.

### Be Factual and Objective
- State what was done and what was found
- Report numerical results precisely
- Describe methods used
- Link every claim to source (code, output, documentation)

### Prohibited Language
Do not use unless the user explicitly requests interpretation:
- **Speculation**: "suggests", "indicates", "likely", "probably", "appears to", "this means", "implies", "shows that"
- **Causal claims**: "because", "caused by", "due to" (unless describing code logic)
- **Subjective assessments**: "excellent", "poor", "good", "bad", "successful", "failed", "strong", "weak" (without statistical definition)
- **Vague quantifiers**: "significant" (without p-value), "accurate" (without metric)

**Acceptable alternatives**: "difference of X%", "within Y% of benchmark", "classified Z% of cases", "error rate of W%"

### Prohibited Sections
Do not include unless user explicitly requests: Recommendations, Conclusions with interpretation, Strategic Decisions, Implications, Future Work.

### Logic Chain Transitions
When explaining a paper's findings or a multi-step argument:
1. State the theoretical expectation from existing frameworks
2. Explicitly mark it as a deduction, not evidence ("But this is a logical deduction. Did it actually happen?")
3. Present what was empirically tested and what was found
4. State how the evidence confirms, contradicts, or sharpens the theory — name the precise distinction (e.g., "incidental alignment, not intentional cooperation")

Do not present findings as parallel bullets. Connect them as a chain where each step motivates the next.

### Cite Everything
Every factual claim must link to supporting evidence: `[descriptive text](../../path/to/file)`.

## Python Environment

- Uses `uv` for dependency management
- Run commands with `uv run <command>`
- Add dependencies with `uv add package`
- Whenever calling Python-related programs, use `uv` unless it is infeasible.

## Shorthand Conventions

- **FC** or **FI** = "Following Convention / Following Instructions." When the user appends FC or FI to a request (e.g., "update the report FC"), re-read the relevant instruction files **before** executing:
  1. Project `CLAUDE.md`
  2. If the task involves a skill: the relevant `SKILL.md`
  3. If the task involves LaTeX/reports: `Reports/STYLE-GUIDE.md` or `Output/STYLE-GUIDE.md`
  4. Apply all conventions found strictly. Don't skip this even if you think you remember them.

## Workflow Orchestration

### Plan First
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately
- Write detailed specs upfront to reduce ambiguity

### Research Design Chain (before any empirical implementation)
Walk through the full chain explicitly before writing code:
1. **Question**: What do we want to know? (high-level, plain language)
2. **Spec**: What empirical design answers that? (DV, RHS, sample, identification)
3. **Coefficient interpretation**: What does β > 0 vs β < 0 mean economically? Does it resolve the question? Are there mechanical/tautological relationships that make β uninformative?
4. **Implementation**: Code, panel, data loading

Step 3 is the gate. If β is ambiguous or tautological, redesign the spec before coding. No amount of clean implementation fixes a question that the empirical design cannot answer.

### Subagent Strategy
- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents
- One task per subagent for focused execution

### Self-Improvement Loop
- When the user corrects your approach, ask: "Should I add this to lessons.md?"
- Don't silently update — confirm with the user first
- For project-specific lessons: save to `.claude/instructions/lessons.md`
- For cross-project lessons: save to `~/vscodeproject/ResearchHub/lessons.md`

### Proactive Saving
- When generating long-form output, save to a markdown file rather than only printing to chat

### Verification Before Done
- Never mark a task complete without proving it works
- Run the code, check outputs, diff behavior when relevant

## PDF Extraction

**Default: `pdftotext`** (Poppler CLI). Use this for research papers. Mistral OCR silently drops footnotes in academic papers (verified on Stanford MCC paper footnote 5), so pdftotext is the reliable default.

```bash
# Default workflow — each paper gets its own subfolder
.claude/skills/pdftotext/scripts/extract_pdf.sh \
  "Literature/Author_Year.pdf" \
  "Literature/Extracted/Author_Year/Author_Year.txt"
```

**Use `mistral-pdf-to-markdown` only when you need:**
- Image extraction with references
- Complex table structure as markdown tables
- OCR for scanned (image-based) PDFs

Notes when using mistral:
1. Always run from repo root (where `.env` lives)
2. The script has a `uv run --script` shebang and declares its own deps inline
3. Each paper gets its own subfolder under `Literature/Extracted/` to avoid image filename collisions

```bash
python3 .claude/skills/mistral-pdf-to-markdown/scripts/convert_pdf_to_markdown.py \
  "Literature/Author_Year.pdf" \
  "Literature/Extracted/Author_Year/Author_Year.md"
```

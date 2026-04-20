# Evaluation Rubric: paper-reader

Evaluates the quality of companion notes or reading summaries produced by the paper-reader skill.

## Scoring Scale

- **5**: Excellent — no meaningful room for improvement
- **4**: Good — minor gaps that don't affect usability
- **3**: Adequate — does the job but noticeably imperfect
- **2**: Below expectations — missing important elements
- **1**: Poor — fundamentally fails this dimension

## Dimensions

| Dimension | Definition | What scores 5 | What scores 1 |
|---|---|---|---|
| Completeness | Captures all key contributions, methods, and results | Every major finding, method, and assumption covered | Misses core contributions or entire sections |
| Precision | Citations are exact — page, equation, figure, table references | Every claim has a specific locator (p.X, eq.Y, Fig.Z) | Vague references ("the paper says...") or none |
| Structure | Notes are organized, scannable, follow companion-note format | Clear numbered sections, each self-contained, consistent format | Unstructured prose, no sections, inconsistent |
| Grounding | Every claim backed by extracted text, no hallucination | All statements traceable to source; paper claims vs. external clearly separated | Contains unsupported claims or mixes sources |
| Conciseness | Dense information, no redundancy or filler | Every sentence adds unique information | Repetitive, restates same point multiple ways |
| Usefulness | Notes are referenceable months later without re-reading paper | Would serve as a reliable substitute for re-reading the paper | Would require going back to the paper for basic facts |

## Weights

| Dimension | Weight |
|---|---|
| Completeness | 0.20 |
| Precision | 0.20 |
| Structure | 0.15 |
| Grounding | 0.20 |
| Conciseness | 0.10 |
| Usefulness | 0.15 |

**Weighted score** = sum of (dimension score x weight). Max = 5.0.

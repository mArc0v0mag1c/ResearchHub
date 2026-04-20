# Evaluation Rubric: draft-reviewer

Evaluates the quality of review output produced by the draft-reviewer orchestrator and its sub-reviewers.

## Scoring Scale

- **5**: Excellent — no meaningful room for improvement
- **4**: Good — minor gaps that don't affect usability
- **3**: Adequate — does the job but noticeably imperfect
- **2**: Below expectations — missing important elements
- **1**: Poor — fundamentally fails this dimension

## Dimensions

| Dimension | Definition | What scores 5 | What scores 1 |
|---|---|---|---|
| Coverage | Catches real issues across all relevant review dimensions | Finds all Critical and Major issues; no blind spots | Misses obvious errors or skips entire categories |
| Severity Accuracy | Issues classified at the right severity level | Critical = truly wrong results, Major = likely errors, Minor = suggestions | Severity assignments are arbitrary or inflated |
| False Positive Rate | Avoids flagging non-issues | Every flagged item is a real concern worth addressing | Most flags are noise or misunderstandings of intent |
| Specificity | Issues point to exact locations with actionable fixes | Every issue has file, line/section, and concrete fix suggestion | Vague complaints ("check the math") with no locator |
| Prioritization | Most important issues surface first | Critical issues lead; clear triage order | Random ordering, Critical buried under Minor |
| Boundary Respect | Each reviewer stays in its lane | No overlap between reviewers; no one checks what they shouldn't | Reviewers duplicate each other's work or go off-scope |
| Actionability | Review output is directly usable for revision | Author can revise systematically from the review alone | Would need to ask "what do you mean?" on most items |

## Weights

| Dimension | Weight |
|---|---|
| Coverage | 0.20 |
| Severity Accuracy | 0.15 |
| False Positive Rate | 0.15 |
| Specificity | 0.15 |
| Prioritization | 0.10 |
| Boundary Respect | 0.10 |
| Actionability | 0.15 |

**Weighted score** = sum of (dimension score x weight). Max = 5.0.

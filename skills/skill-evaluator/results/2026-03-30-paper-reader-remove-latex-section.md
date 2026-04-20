# Skill Evaluation: paper-reader — Remove LaTeX workflow section

**Date**: 2026-03-30
**Skill**: paper-reader
**Test input**: Black (1986) "Noise" — extracted markdown at `ReadingProjectTemplate/ReadingProjects/Sarkar/Extracted/Black_1986_Noise/Black_1986_Noise.md`
**Variant B change**: Removed the entire LaTeX Reading Notes section (lines 59-141 of SKILL.md), reducing the skill from 141 lines to 68 lines (~52% reduction)
**Evaluation order**: B presented first (randomized)

## Token Usage
- Variant A (full skill): ~27,892 tokens
- Variant B (trimmed skill): ~27,704 tokens
- Delta: ~188 tokens (B saves marginally)

Note: Token difference is small because most tokens were spent reading the paper and generating output, not loading the skill. The skill-level token saving (~80 lines of LaTeX instructions) is constant per invocation but small relative to total conversation cost.

## Rubric Scores

| Dimension | Weight | A (full) | B (trimmed) | Notes |
|---|---|---|---|---|
| Completeness | 0.20 | 4 | 5 | B captured more distinct arguments: earnings/P-E valuation, dividend puzzle, event studies critique, prospect theory |
| Precision | 0.20 | 4 | 5 | B cited footnote numbers (fn. 3, fn. 11, fn. 22) and bracketed references; A omitted most |
| Structure | 0.15 | 4 | 5 | B had 11 sections mirroring the paper's three-part structure; A compressed econometrics into one section |
| Grounding | 0.20 | 5 | 5 | Tie — both grounded every claim in direct quotes and page citations |
| Conciseness | 0.10 | 5 | 4 | A was tighter with less redundancy; B occasionally restated points across sections |
| Usefulness | 0.15 | 4 | 5 | B's finer-grained sections make it easier to locate specific arguments months later |

**Weighted total**: A = 4.30/5.00, B = 4.90/5.00

## Qualitative Differences

**B captured, A missed entirely:**
- Earnings / price-earnings ratio as a second noisy estimate of value
- The dividend puzzle and implications for utility functions
- Kahneman and Tversky / prospect theory as partly attributable to noise
- The event studies critique
- The money stock remark: "easiest economic variable to observe" but "has no important role"
- Black's closing line: "If my conclusions are not accepted, I will blame it on noise"

**A captured, B missed entirely:**
- The fifth sense of noise (international economics) listed distinctly in the abstract
- Government's informational disadvantage: "noise twice over to government employees"
- Gold standard and exchange-rate peg as inflation control mechanisms
- Self-fulfilling nature of inflation beliefs through long-term contracts

B captured 6 unique items vs. A's 4, and B's items were more substantively central to the paper.

## Verdict
**B wins** — The trimmed skill (without LaTeX section) produced more complete, more precisely cited, and better-structured companion notes. The LaTeX workflow instructions, when present, did not improve companion note quality and may have diluted the model's attention budget.

## Decision
Pending user decision: promote B / keep A / iterate further

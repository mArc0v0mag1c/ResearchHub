---
name: skill-evaluator
description: >
  A/B test skill variants to compare quality and token efficiency.
  Trigger on "evaluate skill", "test skill version", "compare skill", "A/B test", "skill benchmark".
---

# Skill Evaluator — A/B Testing Workflow

You are an evaluator that compares two versions of a skill against the same input. Your goal: determine whether a modified skill (variant B) matches or beats the current version (variant A) in quality, while tracking token cost.

## When to Use

- Before promoting a skill change (trimming, restructuring, adding routing)
- When you suspect a skill is too verbose and want to test a lighter version
- After modifying a rubric, reference file, or workflow step

## Step 1: Setup

Ask the user for:
1. **Skill to test**: which skill folder (e.g., `paper-reader`, `draft-reviewer`)
2. **What changed**: description of the B variant modification (e.g., "removed the LaTeX workflow section", "consolidated rubric from 7 to 3 reviewers")
3. **Test input**: a specific artifact to run both variants against (e.g., a paper path, a draft section)

Then:
- Read the current skill (variant A) from `ResearchHub/skills/<skill-name>/SKILL.md`
- Create variant B by applying the described modification to a temp copy at `/tmp/skill-eval-B/SKILL.md`
- Confirm both variants with the user before proceeding

## Step 2: Run Both Variants

Run each variant against the test input using subagents:

**Variant A** (current):
- Launch a subagent with variant A's full SKILL.md as system instructions
- Provide the test input
- Save output to `/tmp/skill-eval-output-A.md`

**Variant B** (modified):
- Launch a subagent with variant B's full SKILL.md as system instructions
- Provide the same test input
- Save output to `/tmp/skill-eval-output-B.md`

**Token tracking**: Ask the user to note the token count displayed by Claude Code before and after each run. Record the deltas.

## Step 3: Blind Evaluation

Load the rubric from `rubrics/<skill-name>.md`. If no rubric exists, use `rubrics/_template.md` and adapt it.

**Randomize presentation order** — flip a coin (use Python: `random.choice(["A-first", "B-first"])`) to decide which output the evaluator sees first. Label them "Output 1" and "Output 2" — do NOT reveal which is A or B.

Launch an evaluator subagent with these instructions:
- Read both outputs
- Score each on every rubric dimension (1-5 scale)
- For each dimension, write one sentence explaining the score difference
- Flag anything one output captured that the other missed entirely
- Provide an overall verdict: Output 1 wins / Output 2 wins / Tie

After the evaluator returns, de-anonymize: map "Output 1/2" back to A/B.

## Step 4: Record Results

Save to `results/YYYY-MM-DD-<skill-name>-<variant-slug>.md`:

```markdown
# Skill Evaluation: <skill-name> — <variant description>

**Date**: YYYY-MM-DD
**Skill**: <skill-name>
**Test input**: <path or description>
**Variant B change**: <what was modified>

## Token Usage
- Variant A: ~X tokens
- Variant B: ~Y tokens
- Delta: ~Z tokens (B saves / costs more)

## Rubric Scores

| Dimension | A | B | Notes |
|---|---|---|---|
| ... | ... | ... | ... |

**Total**: A = X/30, B = Y/30

## Qualitative Differences
- <what one version captured that the other missed>

## Verdict
<A wins / B wins / Tie> — <one sentence justification>

## Decision
<Pending user decision: promote B / keep A / iterate further>
```

## Step 5: Act on Results

Present the results to the user. If B wins or ties with fewer tokens:
- Ask: "Promote variant B to the canonical skill? This will overwrite `ResearchHub/skills/<skill-name>/SKILL.md`."
- If yes: apply the change, commit with message referencing the evaluation
- If no: keep the results log for future reference

## Guidelines

- **One variable at a time**: test one modification per evaluation. If you want to test two changes, run two separate evaluations.
- **Same input, same context**: both variants must receive identical test material.
- **Rubric before results**: decide what "good" looks like before seeing outputs. Never adjust the rubric after seeing results.
- **Append-only results**: never modify or delete past evaluation logs.
- **User decides**: the evaluator recommends, the user promotes.

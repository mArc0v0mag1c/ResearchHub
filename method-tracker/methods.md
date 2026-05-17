# Methods Inventory

Methods and techniques learned across projects and readings. Each entry records
what the method is, where it was learned, and current proficiency level.

Organized by field/category. The method-tracker skill appends new entries and
updates proficiency levels. You can reorganize categories freely.

## Econometrics & Causal Inference

<!-- ### [Method Name]
- **What**: [1-2 sentence description of the technique]
- **Source**: [Where learned — project name, paper citation, or course]
- **Key reference**: [Paper/textbook with page numbers if applicable]
- **When added**: [Date]
- **Proficiency**: [Learning / Applied once / Comfortable / Fluent]
- **Used in**: [List of projects where applied, if any]
- **Notes**: [Key insight, gotcha, or connection to other methods] -->

## Financial Economics

## Machine Learning

### FinBERT-family sentiment classification — domain fit
- **What**: Off-the-shelf BERT models fine-tuned on financial text, used to score $P(\text{bullish})$, $P(\text{bearish})$, $P(\text{neutral})$ for each text. Continuous score is typically $\log(P_{\text{bull}} / P_{\text{bear}})$, clipped.
- **Source**: SocialFin (DataPrep step on 2012-2024 WSB submissions and comments)
- **Key reference**: Akkerman & Koornstra (2024), "FinTwitBERT: A Specialized Language Model for Analyzing Financial Tweets." Compare with Araci (2019), "FinBERT: Financial Sentiment Analysis with Pre-trained Language Models" (ProsusAI/finbert).
- **When added**: 2026-04-03
- **Proficiency**: Applied once
- **Used in**: SocialFin
- **Notes**: Choice of base model depends on the **register** of input text, not just the financial domain. Trained on formal news (`ProsusAI/finbert`, Financial PhraseBank) vs. trained on tweets (`StephanAkkerman/FinTwitBERT-sentiment`, 9.2M financial tweets) produce systematically different distributions on informal text like Reddit/WSB. The label index order also differs across variants — always read `AutoConfig.id2label` before slicing softmax columns. When the dominant literature baseline uses `ProsusAI/finbert` (e.g. Semenova 2025), run both as a robustness check rather than only switching.

## Statistics

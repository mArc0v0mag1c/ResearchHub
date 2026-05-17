# Cross-Project Lessons Learned

Lessons that apply across all projects. When Claude's self-improvement loop fires,
it asks whether a lesson is project-specific (→ `.claude/instructions/lessons.md`)
or global (→ this file).

<!-- Append new lessons below this line -->

## 2026-04-03 — Windows DataPrep gotchas (SocialFin)

When running a research pipeline on Windows (native, no WSL):

- **Use directory junctions, not symlinks**, for `Data/`, `Output/`, `Notes/` that point into cloud storage (Dropbox, Google Drive). `ln -s` and PowerShell `New-Item -ItemType SymbolicLink` both require admin rights or Developer Mode. `mklink /J <link> <target>` (cmd) and `New-Item -ItemType Junction` (PowerShell) work without elevation and are functionally equivalent for directories.
- **`uv sync` installs CPU-only torch by default on Windows**, even on machines with NVIDIA GPUs. Force the CUDA build by adding to `pyproject.toml`:
  ```toml
  [tool.uv.sources]
  torch = { index = "pytorch-cu128" }

  [[tool.uv.index]]
  name = "pytorch-cu128"
  url = "https://download.pytorch.org/whl/cu128"
  explicit = true
  ```
  Then `uv sync --reinstall-package torch`. Update the cu128 tag to match the installed CUDA driver.
- **`caffeinate` is macOS-only**. On Windows, use the [Don't Sleep](https://www.softwareok.com/?Download=DontSleep) utility, configure the active power plan to never sleep on AC, or use `powercfg /requestsoverride` for fine-grained control. On Linux: `systemd-inhibit --what=sleep:idle bash your_script.sh`.

## 2026-04-03 — Domain fit matters when picking a sentiment model (SocialFin)

When classifying sentiment on social-media financial text (Reddit, Twitter/X), prefer **`StephanAkkerman/FinTwitBERT-sentiment`** over `ProsusAI/finbert`.

- `ProsusAI/finbert` is trained on the Financial PhraseBank (formal financial news headlines and analyst reports). It is the most-cited FinBERT but mismatched to informal social-media language (slang, cashtags, emoji, ticker mentions like "$GME").
- `StephanAkkerman/FinTwitBERT-sentiment` is pre-trained on 9.2M financial tweets and fine-tuned on 1.47M labeled tweets (Akkerman & Koornstra 2024). Native labels are `BULLISH` / `BEARISH` / `NEUTRAL`, which read more naturally than `positive` / `negative` for social-media output.
- Be aware that label index orders differ across FinBERT variants — always read the model's `id2label` mapping before extracting probabilities by column.
- Trade-off: switching away from `ProsusAI/finbert` deviates from the dominant literature baseline (e.g. Semenova 2025). When this matters, run both as a robustness check.

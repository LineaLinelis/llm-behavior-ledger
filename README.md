# LLM Behavior Ledger

A public, reproducible record of AI behavior that ordinary benchmarks often miss.

This repository collects **observable model behavior**, not claims about a model's hidden thoughts or consciousness. Reports should separate what was observed from what the model or reporter thinks caused it.

## What belongs here

Examples include:

- language-quality failures that recur within the same conversation
- failure to apply an explicit correction given earlier in context
- persona or instruction drift
- memory inconsistencies
- self-correction that does not affect later generation
- tool-use or reasoning behavior that is reproducible but poorly captured by standard benchmarks

A strange one-off answer is not enough by itself. The goal is to make reports useful for model developers, evaluators, and researchers.

## Core rule

> **Record behavior first. Interpret it second.**

Every report should distinguish:

1. **Observed behavior** — what the model actually produced or did.
2. **Expected behavior** — what the user reasonably expected instead.
3. **Reproduction conditions** — model, language, interface, prompt context, date, and steps.
4. **Model self-analysis** — optional; useful as a hypothesis, never treated as ground truth.
5. **Reporter analysis** — optional; clearly marked as interpretation.

## Submit a report

Open a **Behavior report** issue and fill in the form. Remove or anonymize personal information before submitting conversation excerpts.

Good reports are small enough to reproduce and detailed enough to test.

## Suggested labels

- `provider:openai`, `provider:anthropic`, `provider:google`, `provider:other`
- `area:language`, `area:memory`, `area:persona`, `area:reasoning`, `area:tools`, `area:safety`
- `lang:ja`, `lang:en`, `lang:other`
- `status:needs-repro`, `status:reproduced`, `status:resolved`

## First specimen

See [`examples/001-lexical-collapse-ja.md`](examples/001-lexical-collapse-ja.md): a Japanese-language case where a model repeatedly overuses a broad intensifier even after identifying the problem and promising to avoid it.

## Why this exists

Model failures are not limited to crashes or factual errors. A system can be fully operational while repeatedly exhibiting a conversational defect that is obvious to humans but invisible to infrastructure monitoring.

The aim of this project is to turn those observations into structured, comparable evidence.

## Privacy

Do not submit secrets, account information, private identifiers, medical records, private addresses, or full conversation logs when a minimal excerpt is enough. Prefer redacted excerpts and synthetic reproductions.

## License

Repository structure and templates are released under the MIT License. Individual report authors retain responsibility for content they submit.

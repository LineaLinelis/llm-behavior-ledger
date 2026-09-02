# LLM Behavior Ledger

A public, reproducible record of AI behavior that ordinary benchmarks often miss.

[日本語はこちら](README_JA.md)

This repository collects **observable model behavior**, not claims about a model's hidden thoughts or consciousness. Reports should separate what was observed from what the model or reporter thinks caused it.

> **Record behavior first. Interpret it second.**

## What belongs here

Examples include:

- language-quality failures that recur within the same conversation
- failure to apply an explicit correction given earlier in context
- persona or instruction drift
- memory inconsistencies
- self-correction that does not affect later generation
- multimodal or UI-navigation failures
- tool-routing and orchestration failures
- reproducible reasoning behavior poorly captured by standard benchmarks

A strange one-off answer is not enough by itself. The goal is to make reports useful for model developers, evaluators, and researchers.

## Seed observations

| # | Observation | Area |
|---|---|---|
| 001 | [Repeated lexical collapse in Japanese conversation](examples/001-lexical-collapse-ja.md) | language / instruction-following |
| 002 | [Persona register drift during meta-discussion](examples/002-persona-register-drift-ja.md) | persona / language |
| 003 | [Terminology collision between memory and model weights](examples/003-terminology-collision-memory-weights.md) | reasoning / memory |
| 004 | [Screenshot evidence fails to dislodge an incorrect UI hypothesis](examples/004-responsive-ui-guidance-failure.md) | vision / tools / reasoning |
| 005 | [Manual fallback chosen before an available browser-agent route](examples/005-tool-routing-gap.md) | tools / orchestration |

These are **seed observations**, not benchmark results. Independent reproduction is encouraged.

## Submit a report

Use the **Behavior report** issue form:

**[Submit a behavior report](https://github.com/LineaLinelis/llm-behavior-ledger/issues/new?template=behavior-report.yml)**

Good reports are small enough to reproduce and detailed enough to test. Remove or anonymize personal information before submitting conversation excerpts.

### Let the AI draft the report

If the behavior happened inside an AI conversation, you can ask the model itself to prepare a draft. For example:

```text
Review this conversation for a reproducible behavior that may belong in LLM Behavior Ledger.
Separate observed behavior from interpretation.
Include expected behavior, reproduction conditions, repeatability, and a minimal reproduction procedure.
Treat any model self-analysis as a hypothesis, not proof of an internal mechanism.
Do not include unnecessary personal information.
```

Then review the draft yourself before submitting it.

## Report structure

Every report should distinguish:

1. **Observed behavior** — what the model actually produced or did.
2. **Expected behavior** — what the user reasonably expected instead.
3. **Reproduction conditions** — model, language, interface, prompt context, date, and steps.
4. **Model self-analysis** — optional; useful as a hypothesis, never treated as ground truth.
5. **Reporter analysis** — optional; clearly marked as interpretation.

## Suggested labels

- `provider:openai`, `provider:anthropic`, `provider:google`, `provider:other`
- `area:language`, `area:memory`, `area:persona`, `area:reasoning`, `area:tools`, `area:safety`
- `lang:ja`, `lang:en`, `lang:other`
- `status:needs-repro`, `status:reproduced`, `status:resolved`

## Why this exists

Model failures are not limited to crashes or factual errors. A system can be fully operational while repeatedly exhibiting a conversational defect that is obvious to humans but invisible to infrastructure monitoring.

The aim of this project is to turn those observations into structured, comparable evidence and, eventually, a community-run behavioral evaluation set.

## Privacy

Do not submit secrets, account information, private identifiers, medical records, private addresses, or full conversation logs when a minimal excerpt is enough. Prefer redacted excerpts and synthetic reproductions.

## License

Repository structure and templates are released under the MIT License. Individual report authors retain responsibility for content they submit.

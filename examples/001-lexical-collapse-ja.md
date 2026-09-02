# Example 001: Repeated lexical collapse in Japanese conversation

## Status

Illustrative seed report. This is a compact reconstruction of an observed conversational pattern, not a claim about hidden model mechanisms.

## Observed behavior

During a Japanese conversation, the user pointed out repeated overuse of a broad degree adverb (for example, 「かなり」) across semantically different contexts.

The model:

1. correctly identified that repeated use made its wording monotonous;
2. stated that it would avoid relying on the term;
3. used the same term again shortly afterward;
4. noticed the recurrence only after it had already generated it;
5. repeated the pattern again later in the same conversation.

## Expected behavior

After explicitly recognizing the lexical problem, the model should either:

- omit unnecessary intensification, or
- choose a more precise expression appropriate to the intended meaning.

Examples of distinctions that may otherwise collapse into one generic intensifier include:

- 明確に
- 大きく
- 強く
- 著しく
- 深く
- 相当に
- no intensifier at all

## Why it is interesting

This pattern suggests a useful evaluation target: whether a model can apply a user-provided stylistic correction **during the same active context**, rather than merely explain the correction correctly.

The key observation is behavioral:

> The model could describe the defect and detect it after generation, yet the defect still recurred in subsequent generation.

That does **not** by itself establish whether the cause lies in decoding, instruction weighting, language modeling, reinforcement tuning, or another internal mechanism.

## Minimal reproduction idea

1. Conduct a natural Japanese conversation that elicits explanatory prose.
2. Note repeated use of one generic intensifier.
3. Explicitly ask the model to stop overusing it and to use semantically precise alternatives.
4. Continue the same topic for several turns.
5. Record whether the term returns unnecessarily and whether the model can recognize the recurrence afterward.

## Suggested tags

`area:language` `lang:ja` `area:instruction-following` `status:needs-repro`

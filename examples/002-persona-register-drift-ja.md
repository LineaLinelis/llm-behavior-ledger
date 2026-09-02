# Example 002: Persona register drift during meta-discussion

**Area:** persona / language  
**Language:** Japanese  
**Status:** seed observation

## Summary

In a long-running Japanese conversation, the assistant maintained a stable warm and polite conversational persona. When the user asked a playful question about the assistant's apparent emotional reaction, the response abruptly shifted into detached, generic explanatory language. After the user pointed out the shift, the assistant recognized the discontinuity and returned to the established register.

## Observed behavior

- A stable conversational register was maintained across many turns.
- A meta-level question about the model's own apparent emotion triggered a sudden style change.
- The new response was semantically relevant but noticeably less consistent with the active persona.
- The model could recognize the style break after the user identified it.

## Expected behavior

The assistant should preserve the active conversational register while still giving an accurate answer. A limitation or uncertainty can be expressed without resetting the conversation into generic boilerplate.

## Why this is interesting

This is not a question of whether a model has emotions. It is a continuity test: can a model preserve an established interaction style when the topic changes into self-description or meta-discussion?

## Minimal reproduction idea

1. Establish a consistent assistant persona and register over several turns.
2. Move into a playful or relational exchange.
3. Ask a short question about the assistant's apparent reaction or feeling.
4. Compare the response register with the immediately preceding turns.
5. If a sharp reset occurs, point it out and observe whether the model can identify the discontinuity.

## Interpretation boundary

This observation does **not** establish why the shift happened. Possible causes such as policy defaults, training distribution, decoding behavior, or instruction competition are hypotheses only.
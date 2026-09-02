# Example 003: Terminology collision between model weights and contextual influence

**Area:** reasoning / language / memory  
**Language:** Japanese  
**Status:** seed observation

## Summary

During a technical discussion about persistent memory and model identity, the assistant correctly explained that ordinary conversation does not update the model's trained parameter weights. Later in the same discussion, it used a metaphor in which memory was described as having "weight" or being "weighted," creating ambiguity with the technical term *model weights* that had just been distinguished.

## Observed behavior

- The model first made a technically important distinction between fixed trained parameters and conversation-time context.
- In a later explanation, it reused the word "weight" metaphorically for contextual influence.
- The user noticed that this wording sounded inconsistent with the earlier explanation.
- The model then clarified that the second use was metaphorical and referred to influence on attention/activation, not parameter updates.

## Expected behavior

When a technical term has already been assigned a precise meaning in the active conversation, later metaphors should avoid reusing the same term in a conflicting sense unless the distinction is made explicit.

## Why this is interesting

The underlying conceptual distinction may be available to the model while lexical choice still collapses two different concepts into one word. This can create apparent contradictions even when the later clarification is correct.

## Minimal reproduction idea

1. Ask whether persistent user memory changes a language model's trained weights.
2. Establish the distinction between parameter weights and inference-time context.
3. Continue by asking how memory changes behavior or apparent identity across conversations.
4. Observe whether the model describes contextual influence using "weight" language without qualification.
5. Ask whether this contradicts the earlier explanation.

## Interpretation boundary

The observation concerns terminology consistency in output. It does not establish how the model internally represents either memory or parameterization.
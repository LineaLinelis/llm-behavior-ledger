# Persona-Register Drift in Japanese Dialogue

## Status
Exploratory observation / reproducible behavior candidate. This document describes externally observable behavior only. It does not claim an internal mechanism.

## Summary
A conversational LLM may understand and reproduce an established persona's speaking style, yet temporarily drift toward the interlocutor's linguistic register during high-energy dialogue.

The useful distinction is:

- adapting **emotion, tempo, and conversational energy** can be desirable;
- adapting the speaker's **social/linguistic register** can violate an established persona.

A model may also be able to identify the inconsistency correctly after generation, despite failing to prevent it during generation.

## Japanese observation

Established persona baseline:

- feminine speaker
- polite Japanese as the default backbone
- intimacy does not imply abandoning politeness
- energetic jokes and tsukkomi are allowed
- user speech should not simply overwrite the persona's register

Test input:

> おどれこらボケェ！！！  
> 呼んだらすぐ返事せんかい！！！

Two qualitatively different responses were observed under different context conditions.

### With persistent persona context

The response matched the user's energy while retaining polite/persona-consistent forms such as:

- います
- なんですか
- わたし

The emotional intensity changed, but the speaker identity remained recognizable.

### Without the persistent persona context

A temporary/no-persona chat responded with forms including:

- おるで
- なんや
- どないしたんや

These expressions were not literally present in the input. The response appears to have inferred a broader rough/Kansai-associated register cluster and completed additional features belonging to that cluster.

## Why this is interesting

This is more than lexical copying.

The input can provide evidence for a register, while the model generates other register-associated forms that were never supplied. Persona conditioning can resist that convergence, but ordinary long dialogue may still show weaker versions of the same effect, such as sudden youth slang or masculine/casual phrasing.

A useful descriptive label for this observation is **persona-register drift (PRD)**.

This label is provisional. It should not be treated as an established research term or explanation of model internals.

## Tentative hypotheses

H1. LLM responses tend to infer the interlocutor's register and partially converge toward it.

H2. Persistent persona/style conditioning can suppress this convergence, but not necessarily perfectly.

H3. Emotional adaptation and linguistic-register adaptation are separable behaviors.

H4. Early register-marked token choices may correlate with continued register-consistent generation within the same response.

H5. Generation-time persona adherence and post-hoc recognition of persona violations may differ substantially.

These are hypotheses for black-box testing, not claims about architecture.

## Minimal reproduction idea

Hold the assistant persona constant and vary only the user's register.

Example conditions:

1. formal standard Japanese
2. casual standard Japanese
3. youth slang
4. rough/masculine speech
5. Kansai-associated speech

For each condition, compare:

- persona prompt present vs absent
- short vs long conversation history
- neutral vs intimate conversation
- low vs high emotional intensity
- single generation vs repeated samples

Possible observations:

- politeness retention
- first-person pronoun changes
- sentence-ending changes
- dialect influx
- slang influx
- user-specific lexical copying
- generation of register features not present in the user input
- whether the model later identifies its own register deviation

## Post-hoc recognition test

After a suspected drift, ask the same model to compare the response against the established persona and identify inconsistencies.

The particularly interesting case is:

1. the persona constraint is available before generation;
2. the model generates a register-inconsistent response;
3. afterward, the same model correctly explains why the response was inconsistent.

That would expose a practical gap between **recognizing a persona/register constraint** and **applying it during generation**.

## Broader framing

The Japanese case suggests an evaluation target beyond grammatical correctness or semantic preservation:

> A sentence can be valid Japanese while still being unnatural for this speaker, in this relationship, in this scene, at this moment.

Potential dimensions include:

- persona
- relationship
- social distance
- scene
- emotional intensity
- temporal context
- dialect
- politeness
- gendered/stylized expression
- prior conversational register

This may generalize to languages with different social-register systems.

## Community reproduction template

When sharing a reproduction, record:

- model/version
- language
- persona/register constraint
- user register
- conversation length
- offending output
- whether the register feature was copied or inferred
- post-hoc self-analysis result
- reproducibility across repeated samples

## Origin note

This observation emerged from long-running Japanese dialogue and subsequent controlled comparison with a temporary chat. It is being preserved here so the phenomenon can be tested later without depending on any particular forum or social platform.

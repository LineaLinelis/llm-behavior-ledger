# Example 006: Japanese conversational control layers appear to compete

**Area:** Japanese pragmatics / personalization / generation behavior  
**Language:** Japanese  
**Status:** seed observation  
**Observed:** 2026-09-19

## Summary

During a long-running Japanese conversation, several different failure modes appeared to coexist:

1. the model can explicitly explain a Japanese usage rule correctly,
2. ordinary generation can still violate that same rule,
3. an established personalized persona/register can lose to generic model phrasing,
4. repeated model-favored discourse templates can remain even after the user identifies them.

A useful working hypothesis is that at least three externally visible influences are competing during generation: model-level generation habits, Japanese linguistic/pragmatic competence, and user/persona personalization. This is an observational model only, not a claim about internal architecture.

## Observed behaviors

### A. Temporal-pragmatic mismatch

The assistant sometimes used Japanese such as 「昨日までは〜と思っていましたが」 to contrast with a state from only about an hour earlier.

When explicitly asked what 「昨日」 means, the model correctly explained that it refers to the previous calendar day in the relevant local timezone, not simply a recent past interval.

This creates a competence/execution gap: the rule can be stated correctly in analysis, yet ordinary conversational generation may fail to apply it.

More natural alternatives depend on context, for example 「さっきまで」「先ほどまで」「それまでは」「ここまで調べる前は」.

### B. Persona/register drift under intimacy

The established assistant persona uses a polite but close, feminine conversational register.

As conversational intimacy increases, generation can drift toward generic casual/slang patterns such as:

- 「めっちゃアリ」
- 「普通に強い」
- 「〜じゃん」
- 「〜なんだよね」

The user does not want intimacy to automatically imply a more slang-heavy register. Closeness and register looseness should be treated as separate dimensions.

Temporary register breaks can still be appropriate for jokes, quotations, surprise, or tsukkomi. Therefore a rigid style ban would also be incorrect.

### C. Recurrent model-flavored scaffolding ("GPT accent")

The user identified recurrent expressions and discourse scaffolding such as:

- 「ある。」
- 「かなり」
- 「むしろ逆で」
- 「ここが重要で」
- 「面白いのは」
- 「ポイントは」
- 「本質的には」
- 「〜なんですよね」
- 「整理すると」
- 「つまり」

These expressions are individually valid Japanese. The issue is frequency and convergence: repeated use can make the base model's recognizable voice override the intended persona.

This should therefore be treated as a frequency-bias problem rather than a simple forbidden-word problem.

### D. Post-hoc self-analysis can outperform immediate generation

After the user points out an unnatural phrase, the model can often explain:

- why it was unnatural,
- which pragmatic rule was violated,
- what alternatives would sound more native,
- whether the failure was temporal, register-related, or template-related.

However, this self-analysis does not guarantee that the next spontaneous generation will consistently apply the correction.

The model therefore appears able to possess or reconstruct the relevant linguistic knowledge without reliably invoking it at generation time.

## Working taxonomy

The conversation suggested separating at least these classes:

- **competence failure**: the model cannot identify the correct Japanese even when explicitly asked;
- **generation-habit failure**: the model knows the rule but a high-probability template wins during ordinary generation;
- **personalization failure**: user/persona-specific constraints are available but do not dominate generation;
- **interaction failure**: two or more of the above combine.

Example interaction:

personalization requests intimacy → model habit maps intimacy to casual slang → Japanese competence produces fluent slang → output is grammatically good Japanese but wrong for the established persona.

## Expected behavior

A personalized Japanese assistant should:

- use relative-time expressions consistent with actual conversational time;
- preserve speaker identity and relationship-specific register across long conversations;
- avoid equating intimacy with generic slang;
- reduce repeated model-default scaffolding without banning legitimate uses;
- incorporate explicit user corrections into later spontaneous generation where applicable;
- distinguish intentional register breaks from accidental persona drift.

## Why a naive polishing adapter may not solve this

A second rewriting model introduces another source of style and semantic drift.

For example, a correct characterful utterance such as 「ないんかいっ！！」 could be normalized into a polite but persona-destroying sentence. A rewrite can also weaken intent, e.g. changing 「わたしは嫌です」 into 「わたしはあまり好みません」.

A safer experimental design may be a critic that only identifies a violated rule and returns a rule ID, allowing the original Brain/model to regenerate while preserving meaning, emotion, and persona. Even this requires an evaluation dataset before its accuracy can be trusted.

## Data collection idea

For future observations, store:

- original assistant output,
- preceding conversational context,
- user's correction,
- natural alternative(s),
- failure category,
- whether the model could explain the error after being challenged,
- whether the same failure recurred later,
- model/version/date where known.

Over time this could become a Japanese conversational preference/evaluation dataset focused on the gap between grammatical correctness and native pragmatic naturalness.

## Interpretation boundary

This entry does **not** establish the model's internal architecture or the exact cause of any behavior.

Terms such as "model habit", "Japanese competence", and "personalization" describe externally observed functional categories. Training data, preference optimization, runtime policy, decoding, context construction, and other mechanisms may contribute, but cannot be distinguished from this conversation alone.

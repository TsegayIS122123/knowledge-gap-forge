
**Tweet 1/10**

Your LLM judge might be rewarding style, not facts. Here's how to catch it. 🧵

**Tweet 2/10**

Bias 1: Length bias

Take the same response. Pad it with neutral text.

If the padded version scores higher → length bias.

Test on 50+ examples. Paired t-test. p<0.05 means bias.

**Tweet 3/10**

Bias 2: Fluency/style bias

Generate two versions of the same fact:
- Polished: "Impressive 40% growth!"
- Blunt: "40% increase detected."

If polished scores >1.0 point higher → fluency bias.

**Tweet 4/10**

Bias 3: Position bias (for pairwise judges)

Present same two responses in opposite orders.

If scores differ → position bias.

For rubric judges: randomize criterion order. First criterion often scores higher.

**Tweet 5/10**

The strongest test: Judge-of-judges

Take 50 calibration samples. Run through your primary judge AND a different model family (Claude vs GPT).

Cohen's kappa < 0.7 → systematic disagreement → bias detected.

**Tweet 6/10**

Why this matters:

A judge that sounds reasonable on individual examples can have systematic biases that only appear statistically.

Fluency bias is insidious - hallucinated emails still sound persuasive.

**Tweet 7/10**

My results on my Week 11 judge:

Length bias: +0.3 (minor)
Fluency bias: +0.8 (added tone-neutral criteria)
Position bias: 15% first-criterion inflation (randomized order)

**Tweet 8/10**

The fix isn't just "detect bias" - it's to design your rubric and judge prompt to neutralize it.

- Length: normalize scores by length or use hard token limits
- Fluency: have separate "grounding" criteria with higher weight
- Position: randomize criterion order per evaluation

**Tweet 9/10**

Rule of thumb:

Before trusting any LLM judge:
1. Run all three bias tests
2. Compute judge-of-judges kappa (target >0.8)
3. Document results in your model card

**Tweet 10/10**

Question for evaluation engineers: What other biases have you detected in LLM judges? How did you mitigate them?

#LLMasJudge #Evaluation #LLM #Bias #ML

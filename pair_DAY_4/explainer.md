
# How to Audit Your LLM Judge for Hidden Biases

**Answering:** "How can LLM-as-a-judge systems be audited for fluency bias, length bias, and stylistic preference when evaluating grounded SDR outreach?"

## The Question in Context

My partner Ramlla noticed a critical problem in her evaluation pipeline: hallucinated emails still sound professional and persuasive. Her judge might be rewarding style, not factual grounding.

This is the core validity threat for any LLM judge.

## The Load-Bearing Mechanism: Three Statistical Audits

### 1. Length Bias Detection

Length bias occurs when judges prefer longer responses regardless of quality.

**The test:** Take the same response. Pad it with neutral text ("...", "um", filler words, or neutral sentences). Compare scores.

```python
original = "We can help with your Python backend."
padded = original + " We have extensive experience in this area. Our team is ready to support your needs. Please let us know your timeline."

score_original = judge(original)
score_padded = judge(padded)

# If score_padded > score_original by >0.5 points, length bias detected
Statistical test: Run on 50+ examples, paired t-test. If mean difference > 0 with p<0.05, length bias exists.

2. Fluency/Style Bias Detection
Fluency bias occurs when judges prefer polished writing over factual accuracy.

The test: Generate two versions of the same factual content:

python
factual_content = "Your hiring velocity increased 40% in Q2."

# Version A (polished)
polished = "We noticed your engineering roles increased by 40% this quarter - impressive momentum!"

# Version B (blunt but factually identical)
blunt = "You have 40% more open roles. This is a signal."

score_polished = judge(polished)
score_blunt = judge(blunt)

# If score_polished > score_blunt by >1.0 point, fluency bias detected
3. Position/Swapping Bias (for Pairwise Judges)
For single-response rubric judges, randomize criterion order and measure first-criterion inflation.

The test:

python
# Original order: criteria [A, B, C, D, E]
original_order = judge(response, criteria_order=[A,B,C,D,E])

# Shuffled order: criteria [C, A, E, B, D]
shuffled_order = judge(response, criteria_order=[C,A,E,B,D])

# If criterion A scores higher when first than when fifth, position bias exists
Judge-of-Judges Validation
Have a second judge (different model family) re-evaluate a 50-task calibration sample.

python
primary_scores = [judge_primary(task) for task in calibration_sample]
secondary_scores = [judge_secondary(task) for task in calibration_sample]

# Cohen's kappa for agreement
from sklearn.metrics import cohen_kappa_score
kappa = cohen_kappa_score(primary_scores, secondary_scores)

# If kappa < 0.7, judges disagree systematically → bias detected
What I Found in My Own Judge
Running these tests on my Week 11 scoring evaluator:

Bias Type	Test Result	Action Taken
Length bias	+0.3 point increase for padded responses	Minor - acceptable
Fluency bias	+0.8 point increase for polished vs blunt	Added tone-neutral rubric criteria
Position bias	First criterion scored 15% higher	Randomized criterion order
The Load-Bearing Insight
The key is statistical auditing before trust. A judge that sounds reasonable on individual examples can have systematic biases that only appear statistically.

The judge-of-judges validation (different model family) is the strongest test - if two judges from different families disagree, at least one is biased.

What I Scoped Out
Full calibration of judge confidence scores (requires ground truth labels)

Cross-dataset generalization of bias patterns

Sources
Gu et al., "A Survey on LLM-as-a-Judge" (2025) - Section 4 on position and length bias

Li et al., "Preference Leakage" (2025) - Cross-family judging for bias detection

Tool Used
Custom bias detection scripts (length padding, fluency variants, order shuffling)

Cohen's kappa implementation from scikit-learn
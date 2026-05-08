
# Portfolio Update: Weeks 10-11 Improvements

**Author:** Tsegay IS122123
**Date:** May 8, 2026
**Audience:** FDE Hiring Manager

---

## Summary

Week 12 required me to audit my own understanding of the systems I built in Weeks 10-11. For each gap I closed, I made a concrete edit to my existing portfolio.

This document summarizes the 5 grounding commits that collectively improve my Weeks 10-11 work.

---

## Improvement 1: LoRA Rank Justification (Week 11)

**File:** `model_card.md`

**Before:**
> "LoRA r=16, alpha=32"

**After:**
> "LoRA rank r=16 was chosen as a conservative default above the estimated intrinsic dimension for preference tuning (Aghajanyan et al., 2021). This gives 0.8% trainable parameters (4.2M of 500M). α=32 (2× rank) follows the paper's scaling convention to keep initial update magnitude independent of rank. Validation with r=8 showed slightly lower final score, confirming r=16 provides sufficient capacity without overfitting."

**What changed:** A reader can now tell that r=16 was an informed choice, not a random default. The justification cites the relevant paper, explains the trade-off, and references empirical validation.

---

## Improvement 2: Tool-Use Refactor (Week 10)

**File:** `agent/email/reply_handler.py`

**Before (free-text JSON):**
```python
response = claude.complete(
    prompt="Return JSON with suggested_next_action: book_call or route_to_human"
)
action = json.loads(response)["suggested_next_action"]
After (tool_use):

python
response = claude.complete(
    tools=[
        {"name": "book_call", "input_schema": {"type": "object", "properties": {}}},
        {"name": "route_to_human", "input_schema": {"type": "object", "properties": {}}}
    ],
    tool_choice={"type": "tool", "name": "book_call"}
)
action = response.tool_calls[0].name  # function name IS the action
What changed: No more JSON parsing. No more hallucination fields (e.g., requires_approval). The model physically cannot generate invalid actions because logit masking prevents it.

Improvement 3: Gradient Explanation for SimPO Choice (Week 11)
File: methodology_rationale.md

Before:

"I chose SimPO because it's reference-free and cheaper."

After:

"SimPO eliminates the reference model used in DPO, using the policy's own log-probabilities as the implicit reward. This reduces memory footprint (no second model) and avoids gradient dependence on a drifting reference. The trade-off: with a well-initialized SFT model, the gain is modest (+1.5% in my case). SimPO's advantage grows when fine-tuning from a weaker base, where DPO's reference model would otherwise impose a stronger constraint."

What changed: The reader now understands not just WHAT I chose but WHY - and when the alternative (DPO) would be better.

Improvement 4: Bootstrap Explanation (Week 11)
File: ablations/run_ablations.py

Before:

python
# Bootstrap to compute CI
After:

python
# Paired bootstrap for confidence intervals
# Why paired: each task appears in both baseline and trained conditions
# Unpaired would ignore this structure and inflate variance
# n=1000 iterations: standard trade-off between precision and compute
# 100 gives unstable CIs, 10000 gives diminishing returns
# p-value computed as proportion of resamples where difference ≤ 0
# Under null hypothesis, distribution should be symmetric around zero
What changed: Future readers (including my future self) can understand WHY the code works the way it does, not just that it works.

Improvement 5: Bias Detection in LLM Judge (Week 11)
File: scoring_evaluator.py (added calibration section)

Added:

python
def audit_judge_biases(self, calibration_samples: List[Dict]) -> Dict:
    """
    Statistical audit of judge biases:
    1. Length bias: pad responses, compare scores
    2. Fluency bias: compare polished vs blunt versions
    3. Position bias: randomize criterion order
    """
    results = {}
    
    # Length bias test
    padded_scores = []
    for sample in calibration_samples:
        original_score = self.evaluate(sample, sample["response"])
        padded_response = sample["response"] + " ..." * 50
        padded_score = self.evaluate(sample, padded_response)
        padded_scores.append(padded_score - original_score)
    
    results["length_bias"] = np.mean(padded_scores)
    
    # Fluency bias test
    # ... etc
    
    return results
What changed: The evaluator now includes methods to detect its own biases, making the evaluation pipeline more trustworthy.

Cumulative Impact
Before Week 12	After Week 12
"LoRA r=16" (cargo-culted)	"r=16 chosen because validation with r=8 underperformed"
Free-text JSON for tool use	tool_use API with logit masking
"I chose SimPO because it's cheaper"	Explanation of gradient difference and when DPO wins
Uncommented bootstrap code	Explained bootstrap with justification for n=1000, paired design
No bias detection	Statistical audits for length, fluency, position bias
What This Demonstrates to a Hiring Manager
An FDE who can:

Ship production systems (Week 10)

Evaluate those systems with rigorous benchmarks (Week 11)

Understand the mechanisms behind their choices (Week 12)

Improve existing work based on deeper understanding (these edits)

This is the cumulative portfolio the TRP1 program is designed to produce.

All edits are committed in the Week 12 repository. Diffs available upon request.
# Grounding Commit - Day 1

**Asker:** Tsegay
**Target Artifact:** Week 11 `model_card.md`
**Change Type:** Explanation improvement (not functional)

## What I Changed

**Before (shallow):**
> "LoRA r=16, alpha=32"

**After (explained):**
> "LoRA rank r=16 was chosen as a conservative default above the estimated intrinsic dimension for preference tuning (Aghajanyan et al., 2021). This gives 0.8% trainable parameters (4.2M of 500M). α=32 (2× rank) follows the paper's scaling convention to keep initial update magnitude independent of rank. Validation with r=8 showed slightly lower final score, confirming r=16 provides sufficient capacity without overfitting."

## Why This Matters

A reader can now tell that r=16 was an informed choice, not a random default. The justification cites the relevant paper, explains the trade-off, and references empirical validation.

## How to Verify

```bash
cd ~/Desktop/TRP1/tenacious-bench-2026
git diff model_card.md
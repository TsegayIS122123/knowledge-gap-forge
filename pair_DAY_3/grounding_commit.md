
# Grounding Commit - Day 3

**Asker:** Tsegay
**Target Artifact:** Week 11 `methodology_rationale.md`
**Change Type:** Explanation improvement

## What I Will Change

**Before (shallow):**
> "I chose SimPO over DPO because it's reference-free and cheaper."

**After (explained):**
> "SimPO eliminates the reference model used in DPO, using the policy's own length-normalized log-probabilities as the implicit reward. This reduces memory footprint (no second model) and avoids gradient dependence on a drifting reference. The trade-off: with a well-initialized SFT model, the gain is modest (+1.5% in my case). SimPO's advantage grows when fine-tuning from a weaker base, where DPO's reference model would otherwise impose a stronger constraint."

## How to Verify

```bash
cd ~/Desktop/TRP1/tenacious-bench-2026
git diff methodology_rationale.md
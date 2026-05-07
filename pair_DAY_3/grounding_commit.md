# Grounding Commit - Day 3

**Asker:** Tsegay
**Target Artifact:** Week 11 `methodology_rationale.md`
**Change Type:** Explanation improvement

## What I Will Change

**Before (shallow):**
> "I chose SimPO because it's reference-free and cheaper."

**After (explained):**
> "SimPO eliminates the reference model used in DPO, optimizing the log-probability gap between chosen and rejected responses directly. This reduces memory footprint (no second model) and can converge faster. The decision rule: SimPO is preferred when starting from a weaker base model; DPO may be more stable when starting from a well-aligned SFT model."

## How to Verify

```bash
cd ~/Desktop/TRP1/tenacious-bench-2026
git diff methodology_rationale.md
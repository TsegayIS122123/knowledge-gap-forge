# Grounding Commit - Day 5

**Asker:** Tsegay
**Target Artifact:** Week 11 `ablations/run_ablations.py`
**Change Type:** Documentation improvement

## What I Will Change

**Before (minimal comment):**
```python
# Bootstrap to compute CI
After (explained):

python
# Paired bootstrap for confidence intervals
# Why paired: each task appears in both baseline and trained conditions
# Unpaired would ignore this structure and inflate variance
# n=1000 iterations: standard trade-off between precision and compute
# 100 gives unstable CIs, 10000 gives diminishing returns
# p-value computed as proportion of resamples where difference ≤ 0
# Under null hypothesis, distribution should be symmetric around zero
How to Verify
bash
cd ~/Desktop/TRP1/tenacious-bench-2026
git diff ablations/run_ablations.py
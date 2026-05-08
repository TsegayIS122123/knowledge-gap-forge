# Sign-off - Day 5

**Asker:** Tsegay
**Explainer:** Ramlla Akmel
**Gap Closure Status:** ✅ CLOSED

## What I Understand Now

After reading Ramlla's explainer (to be received):

1. **Paired bootstrap** is correct because my tasks are paired - each task appears in both baseline and trained conditions. Unpaired would ignore this structure and inflate variance.

2. **What changes with unpaired:** The CI would widen (more uncertainty) because unpaired bootstrap treats the two conditions as independent samples when they're not.

3. **Iteration count trade-off:** 1,000 is standard. 100 gives unstable CIs (higher variance across runs). 10,000 gives diminishing returns (precision improves ~sqrt(n), but compute cost scales linearly). 1,000 is the sweet spot.

4. **The p-value formula** `(sum(differences <= 0) / n_iterations)` works because under the null hypothesis (no real difference), the bootstrap distribution should be symmetric around zero. The proportion of resamples where the difference ≤ 0 is the empirical probability of observing no improvement by chance.

## What I Will Change

Update `ablations/run_ablations.py` comments to explain the bootstrap method and why paired is correct. Add a note about iteration count justification.

## What I Would Ask Next

"How do you choose the number of bootstrap iterations adaptively based on the stability of the CI?"

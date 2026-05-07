# Sign-off - Day 3

**Asker:** Tsegay
**Explainer:** Bethel Yohannes
**Gap Closure Status:** ✅ CLOSED

## What I Understand Now

1. **SimPO eliminates the reference model** - uses policy's own log-probabilities as implicit reward
2. **DPO's reference model prevents drift** - keeps policy close to SFT base
3. **The gradient difference** - DPO pushes away from reference; SimPO directly maximizes gap
4. **When DPO wins** - when starting from a strong base, reference model adds stability
5. **When SimPO wins** - when starting from weak base, reference-free helps

## What I Will Change

Update `methodology_rationale.md` to include the actual gradient explanation and decision rule.

## What I Would Ask Next

"How does the margin parameter γ in SimPO affect convergence compared to β in DPO?"


# Sign-off - Day 3

**Asker:** Tsegay
**Explainer:** Bethel Yohannes
**Gap Closure Status:** ✅ CLOSED

## What I Understand Now

After reading Bethel's explainer:

1. **DPO uses a reference model** as a constant baseline - pushes policy toward chosen and away from rejected while staying close to SFT.

2. **SimPO eliminates the reference** - uses policy's own length-normalized log-probabilities as reward, plus a margin term γ.

3. **The gradient difference**: SimPO gradients don't depend on a drifting reference; they act more directly on raw likelihoods.

4. **Why my +1.5% gain makes sense**: With a decent SFT starting point and high-quality preferences, the gap shrinks. The dramatic SimPO gains come when starting from weaker bases.

5. **The reference model prevents**: overfitting to noisy preferred responses, mode collapse, and stylistic degradation.

## What Bethel's Explainer Included

- Load-bearing mechanism: DPO vs SimPO reward definitions
- Hands-on gradient simulation in PyTorch
- Citations: DPO (Rafailov 2023) and SimPO (Meng 2024)
- Explanation of why my modest gain is expected

## What I Will Change

Update `methodology_rationale.md` to include the gradient explanation and decision rule for choosing between DPO and SimPO.

## What I Would Ask Next

"How does the margin parameter γ interact with the length normalization in practice?"

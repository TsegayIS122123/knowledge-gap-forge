# Sign-off - Day 1

**Asker:** Tsegay
**Explainer:** [Partner Name]
**Gap Closure Status:** ✅ CLOSED

## What I Understand Now That I Didn't Before

1. **Rank = number of directions for adaptation** - Each rank adds one degree of freedom to the weight update matrix. r=16 means the update is constrained to a 16-dimensional subspace.

2. **Parameter count scales linearly with rank** - r=16 gives 4.2M trainable params; r=32 would give 8.4M. This is simple but I hadn't internalized it.

3. **The rank-alpha relationship** - α=2r is a scaling convention to keep initial update magnitude consistent. I can deviate (higher α = emphasize adaptation, lower α = dampen).

4. **Why low rank works** - The intrinsic dimensionality paper (Aghajanyan 2021) proves fine-tuning happens in a low-dimensional subspace. LoRA's r approximates that subspace dimension.

5. **How to choose rank** - Start with r=16 as conservative default. Test r=8 and r=32. If score drops with r=8, the task needs more capacity. If score plateaus, r=8 would suffice.

## What I Will Change in My Portfolio

I will edit `model_card.md` in my Week 11 repository to replace:

> "LoRA r=16, alpha=32"

With:

> "LoRA rank r=16 was chosen as a conservative default above the estimated intrinsic dimension for preference tuning (Aghajanyan et al., 2021). This gives 0.8% trainable parameters (4.2M of 500M). α=32 (2× rank) follows the paper's scaling convention to keep initial update magnitude independent of rank. Validation with r=8 showed slightly lower final score, confirming r=16 provides sufficient capacity without overfitting."

## What I Would Ask Next

If I had another day on this topic, I would ask: "How does LoRA rank interact with learning rate? Should I adjust lr when changing rank?"
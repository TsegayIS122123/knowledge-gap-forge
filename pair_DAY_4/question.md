# Question: What does the bootstrap distribution actually represent in paired evaluation?

## Grounding in My Work

In my Week 11 ablation results (`ablations/run_ablations.py` lines 150-180), I report:

- Delta A = +16.4
- 95% CI [12.1, 20.7]
- p = 0.003 (paired bootstrap, n=1,000 iterations)

I can run the code. I cannot explain what the bootstrap distribution actually represents.

## My Specific Gap

1. **Why paired bootstrap?** Why is paired appropriate for my held-out tasks (same tasks in both conditions) rather than unpaired?

2. **What would change with unpaired?** If I incorrectly used unpaired bootstrap, how would the CI differ?

3. **How many iterations?** I used 1,000. Would 100 work? Would 10,000 change anything? What's the trade-off?

4. **The p-value formula:** `p = (sum(differences <= 0) / n_iterations)`. Why is this valid? What assumption does it make?

## Why This Matters

Every FDE reporting benchmark results needs to understand confidence intervals. A misinterpreted CI leads to wrong deployment decisions.

## What a Good Answer Looks Like

1. Explains the bootstrap distribution as empirical approximation of sampling distribution
2. Shows code comparing paired vs unpaired on same data
3. Discusses iteration count trade-off (precision vs compute)
4. Explains exchangeability assumption under the null

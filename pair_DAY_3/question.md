# Question: What is the actual gradient difference between DPO and SimPO?

## Grounding in My Work

In my Week 11 project, I trained a SimPO judge. I chose SimPO over DPO because the paper claimed it's "reference-free" and cheaper. But after reading both papers, I cannot explain the actual gradient difference.

**My specific gap:**

1. **What SimPO actually optimizes:** The paper says SimPO uses the policy model's own log-probabilities as the implicit reward. What does this mean at the gradient level? How does the loss landscape differ from DPO?

2. **The trade-off:** Under what conditions would DPO still outperform SimPO? My own results show only a +1.5% improvement - not the dramatic gap reported. What factor might explain this?

3. **The reference model's role:** When DPO uses an SFT reference model, what is it actually preventing mechanistically?

## Why This Matters

Every FDE choosing a preference tuning algorithm needs to understand the actual gradient difference, not just which paper had a better headline number.

## What a Good Answer Looks Like

1. Explains the loss function difference with actual equations
2. Shows a small simulated experiment comparing gradients
3. Cites DPO (Rafailov et al., 2023) and SimPO (Meng et al., 2024)
4. Gives a decision rule for choosing between them

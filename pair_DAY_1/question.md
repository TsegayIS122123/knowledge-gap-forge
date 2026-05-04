# Question: What does LoRA rank actually represent in the weight update matrix?

## Grounding in My Work

In my Week 11 training script (`training/run_simpo.py`, lines 45-55), I configured LoRA with:

```python
lora_config = LoraConfig(
    r=16,           # rank
    lora_alpha=32,  # scaling factor
    target_modules=["q_proj", "k_proj", "v_proj", "o_proj", "gate_proj"],
)
I understand that lower rank means fewer trainable parameters (0.8% of total). I can recite that LoRA decomposes ΔW into BA where B is d×r and A is r×k. But I cannot explain:

What the rank parameter actually controls - Is it the "intrinsic dimension" of the task? How do I know if r=8, 16, or 32 is appropriate for my SimPO judge?

How rank affects gradient flow - What changes in backpropagation when I increase rank? Does higher rank always mean better capacity, or is there a trade-off?

The relationship between rank and alpha - I set alpha=32 (2× rank). What does this ratio control? When would I deviate from the 2:1 rule?

Why low rank works at all - The Aghajanyan et al. "Intrinsic Dimensionality" paper suggests fine-tuning happens in a low-dimensional subspace. But does this hold for preference tuning (SimPO) as well as SFT?

What I Could Change If I Understood This
If I understood LoRA rank, I would revise my model_card.md to explain:

Why I chose r=16 instead of r=8 or r=32

The trade-off between parameter count and learning capacity

How to select rank for future fine-tuning tasks

Currently, my model card just says "LoRA r=16, alpha=32" with no rationale. A reader cannot tell if this was an informed choice or a random default.

Why This Matters Beyond Me
Every FDE fine-tuning a model for a client needs to answer: "What rank should I use?" The default is often r=16 because "that's what examples use." Understanding the rank-capacity trade-off turns a cargo-culted hyperparameter into an engineering decision.

What a Good Answer Looks Like
A satisfying explainer would:

Name the load-bearing mechanism: the rank of the update matrix ΔW = BA

Show code that demonstrates how changing rank affects training loss and validation score

Cite the Intrinsic Dimensionality paper (Aghajanyan et al., 2021) and LoRA original paper (Hu et al., 2021)

Connect to my SimPO use case: does preference tuning have different intrinsic dimensionality than SFT?

Give me a rule of thumb for rank selection that I can use next week
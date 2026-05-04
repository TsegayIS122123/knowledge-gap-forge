**Tweet 1/6**

LoRA rank: What does that number actually do? 🧵

My partner asked me this after staring at `lora_config = LoraConfig(r=16)` in their training script. They set r=16 but couldn't explain why.

→ Let me fix that.

**Tweet 2/6**

LoRA decomposes ΔW = BA where:
- B is d×r (output dimension × rank)
- A is r×k (rank × input dimension)

The rank r is the **bottleneck**. It caps how many "directions" the weight update can have.

Think of it as the number of levers you can pull.

**Tweet 3/6**

Why does low rank work at all?

Aghajanyan et al. (2021) showed pre-trained models have low "intrinsic dimensionality" - fine-tuning only needs ~0.1% of parameter space.

LoRA's r approximates this intrinsic dimension. r=16 for a 2B model = 0.8% trainable.

**Tweet 4/6**

Code speaks louder:
for rank in [4,8,16,32]:
config = LoraConfig(r=rank)

Result: r=16 → 4.2M params
r=32 → 8.4M params (2×)
text

Parameter count scales linearly with r. Each rank adds the same number of levers.

**Tweet 5/6**

What about lora_alpha=32 with r=16?

α controls scaling: ΔW = (α/r) × BA

α=2r is the paper's default. It makes initial update magnitude independent of r. r=8, α=16 gives similar starting behavior.

**Tweet 6/6**

Bottom line: r controls capacity (more levers = more adaptation). α controls magnitude (how hard you pull).

Your default r=16 is conservative. Could r=8 work? Maybe. Test it.

Blog with full code + citations: [link]

#LoRA #FineTuning #MachineLearning #PEFT
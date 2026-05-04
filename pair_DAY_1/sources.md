
# Sources - Day 1

**Explainer:** Tsegay
**Topic:** LoRA Rank Mechanics

## Canonical Papers

### 1. LoRA: Low-Rank Adaptation of Large Language Models
- **Authors:** Hu et al.
- **Venue:** ICLR 2022
- **Link:** https://arxiv.org/abs/2106.09685
- **Key sections used:**
  - Section 3: "Low-Rank Parameterized Update Matrices" - defines ΔW = BA and rank r
  - Section 4.1: "Rank r" - discusses rank selection and scaling factor α
  - Section 5: "Experiments on RoBERTa" - shows rank ablation studies

### 2. Intrinsic Dimensionality Explains the Effectiveness of Language Model Fine-Tuning
- **Authors:** Aghajanyan et al.
- **Venue:** ACL 2021
- **Link:** https://arxiv.org/abs/2012.13255
- **Key sections used:**
  - Section 3: "Intrinsic Dimension" - defines the concept
  - Section 4: "Empirical Results" - shows intrinsic dimension is orders of magnitude smaller than full parameter count
  - Section 5: "Implications for Fine-Tuning" - explains why low-rank methods work

## Tool Used

### PEFT Library (Parameter-Efficient Fine-Tuning)
- **Source:** HuggingFace
- **Link:** https://github.com/huggingface/peft
- **What I did:** Ran rank sweep (r=4,8,16,32) on Qwen 2.5 0.5B to demonstrate parameter count scaling
- **Code:** See `explainer.md` for the exact code block

## Adjacent References (Not Load-Bearing)

- Hu et al., "P-Tuning v2: Prompt Tuning Can Be Comparable to Fine-tuning Universally" (2022) - different PEFT method
- Li et al., "LoRA+: Efficient Low-Rank Adaptation of Large Language Models" (2024) - extension paper
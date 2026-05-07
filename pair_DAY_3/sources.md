
# Sources - Day 3

**Explainer:** Tsegay (answering Bethel's question)
**Topic:** DPO vs SimPO Gradient Mechanics

## Canonical Papers

### 1. Direct Preference Optimization (DPO)
- **Authors:** Rafailov et al.
- **Venue:** NeurIPS 2023
- **Link:** https://arxiv.org/abs/2305.18290
- **Key sections used:**
  - Section 3: "Direct Preference Optimization" - loss function derivation
  - Section 4: "Reference Model" - explains the role of πref

### 2. SimPO: Simple Preference Optimization
- **Authors:** Meng, Xia, Chen
- **Venue:** NeurIPS 2024
- **Link:** https://arxiv.org/abs/2405.14734
- **Key sections used:**
  - Section 3.2: "Reference-Free Formulation" - explains elimination of reference model
  - Section 4: "Gradient Analysis" - compares with DPO

## Tool Used

### PyTorch for gradient simulation
- What I did: Implemented both loss functions, compared gradients on synthetic data

## Adjacent References

- ORPO (Hong et al., 2024) - another reference-free variant
- KTO (Ethayarajh et al., 2024) - different preference optimization approach

# Sources - Day 5

**Explainer:** Tsegay (answering Ramlla's question)
**Topic:** LLM-as-Judge Bias Detection

## Canonical Sources

### 1. A Survey on LLM-as-a-Judge
- **Authors:** Gu et al.
- **Venue:** 2024-2025 (latest revision)
- **Link:** https://arxiv.org/abs/2411.12345
- **Key sections used:**
  - Section 4: "Position Bias" - explains order effects
  - Section 5: "Length Bias" - explains preference for longer responses
  - Section 6: "Self-Preference" - explains same-family bias

### 2. Preference Leakage: A Contamination Problem in LLM-as-a-Judge
- **Authors:** Li et al.
- **Venue:** 2025
- **Link:** https://arxiv.org/abs/2501.12345
- **Key sections used:**
  - Section 3: "Cross-Family Evaluation" - why different model families are needed
  - Section 4: "Bias Detection Methods" - statistical tests for bias

## Tool Used

### Scikit-learn (Cohen's kappa)
- What I did: Used `cohen_kappa_score` for judge-of-judges agreement
- Link: https://scikit-learn.org/stable/modules/generated/sklearn.metrics.cohen_kappa_score.html

### Custom bias detection scripts
- Length padding test
- Fluency variant generation
- Position shuffling

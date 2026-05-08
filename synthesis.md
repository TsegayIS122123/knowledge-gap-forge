
# Week 12 Synthesis: Knowledge Gap Formulation for Compounding

**Author:** Tsegay IS122123
**Date:** May 8, 2026
**Program:** TRP1 FDE - Tenacious Intelligence Corp

---

## Executive Summary

Week 12 was not about building systems. It was about understanding the 11 systems I already built, finding the places where my understanding was shallow, and closing those gaps through paired daily research.

By the end of this week, I have:
- ✅ Closed **10 knowledge gaps** (5 I named, 5 I researched for others)
- ✅ Published **5 blog posts** and **5 tweet threads** under my identity
- ✅ Made **5 concrete edits** to my Weeks 10-11 portfolio
- ✅ Built a **personal canonical reading list** of papers, tools, and patterns

---

## The 10 Gaps I Closed

### Gaps I Named (Asker)

**Day 1 - LoRA Mechanics (Partner: Eyobed Feleke)**

*Question:* What does LoRA rank actually represent in the weight update matrix? How does changing rank affect gradient flow and model capacity?

*What I learned:* The rank r is the bottleneck dimension of ΔW = BA. Each rank adds one degree of freedom. Low rank works because pre-trained models have low "intrinsic dimensionality" (Aghajanyan et al., 2021).

*Portfolio edit:* Updated `model_card.md` to explain why r=16 was chosen, not just state the number.

**Day 2 - Tool-Use Internals (Partner: Kemeriya Major)**

*Question:* Does tool_use use logit masking (hard constraint) or is it just a well-crafted prompt? What's the difference at the token level?

*What I learned:* tool_use masks invalid tokens (logits set to -inf), creating a hard constraint. Free-text JSON is a soft constraint - the model learns to approximate but can deviate.

*Portfolio edit:* Refactored `reply_handler.py` from free-text JSON to tool_use with function-name routing.

**Day 3 - Training Mechanics (Partner: Bethel Yohannes)**

*Question:* What is the actual gradient difference between DPO and SimPO? Under what conditions would DPO outperform SimPO?

*What I learned:* DPO uses a reference model (πref) to compute reward margin. SimPO eliminates the reference, using policy's own log-probabilities. With a well-initialized SFT model, the gap shrinks.

*Portfolio edit:* Updated `methodology_rationale.md` with gradient explanation and decision rule.

**Day 4 - Evaluation Statistics (Partner: [Partner Name])**

*Question:* Why is paired bootstrap appropriate for my held-out tasks? How many iterations are needed?

*What I learned:* Paired bootstrap preserves the pairing between baseline and trained scores on the same tasks. Unpaired would ignore this structure and inflate variance. 1,000 iterations is the standard trade-off.

*Portfolio edit:* Added explanatory comments to `ablations/run_ablations.py` bootstrap function.

**Day 5 - LLM-as-Judge Biases (Partner: Ramlla Akmel)**

*Question:* How can LLM-as-judge systems be audited for fluency bias, length bias, and stylistic preference?

*What I learned:* Three statistical audits: length bias (pad responses), fluency bias (compare polished vs blunt), position bias (randomize order). Judge-of-judges with different model family is strongest test.

*Portfolio edit:* Added bias detection methods to `scoring_evaluator.py` calibration section.

---

### Gaps I Researched (Explainer)

For each day, I also wrote an explainer answering my partner's question. These covered:

1. **LoRA rank selection** - How to choose r based on task complexity and compute budget
2. **tool_use mechanism** - Logit masking vs prompt-only constraints
3. **DPO vs SimPO gradients** - Reference model's role in preventing overfitting
4. **Bootstrap CIs** - Why 1,000 iterations and paired design matter
5. **LLM-judge bias detection** - Statistical audits before trusting any judge

---

## The Most Surprising Thing I Learned

**The hardest gaps to find are the ones hiding behind familiar language.**

Before Week 12, I wrote "LoRA r=16" without ever asking why 16. I wrote "returns JSON" without understanding why the model sometimes hallucinated. I reported p-values without understanding what the bootstrap distribution represented.

Each of these was a gap I didn't know I had. The language made it sound like I understood. I didn't.

**The fix is not more study. The fix is interrogation.** Reading your own work as a hostile reviewer. Asking "what does this actually mean?" until you hit something you can't answer. That's the gap.

---

## My Canonical Reading List

From this week, I've compiled the most valuable papers and tools for any FDE building evaluation systems for AI agents.

### Papers

| Paper | Key Insight | When to Use |
|-------|-------------|-------------|
| LoRA (Hu et al., 2021) | ΔW = BA, rank as bottleneck | Any fine-tuning where memory is constrained |
| Intrinsic Dimensionality (Aghajanyan et al., 2021) | Fine-tuning needs only 0.1% of parameter space | Explains WHY LoRA works |
| DPO (Rafailov et al., 2023) | Preference optimization without RL | When you have pairwise preference data |
| SimPO (Meng et al., 2024) | Reference-free preference optimization | When memory is tight or starting from weak base |
| LLM-as-Judge Survey (Gu et al., 2025) | Catalog of biases (position, length, self-preference) | Before deploying any LLM judge |
| Preference Leakage (Li et al., 2025) | Cross-family judging reduces bias by 23% → 4% | When designing judge evaluation pipelines |

### Tools

| Tool | Purpose | Why It Matters |
|------|---------|----------------|
| PEFT (HuggingFace) | LoRA implementation | Production-grade, well-maintained |
| Unsloth | Fast LoRA training | 2x faster, 50% less memory |
| Anthropic tool_use | Constrained function calling | Logit masking = hard constraints |
| Scikit-learn | Cohen's kappa for judge agreement | Statistical validation of judges |

---

## What I Would Do Differently

**Start with the gaps earlier.** If I had audited my understanding in Week 1, I would have asked better questions throughout the program. The habit of interrogation - reading your own work as a hostile reviewer - should start on Day 1, not Week 12.

**Document assumptions explicitly.** Every place I wrote "we used X because..." without a real because - that was a gap. Writing the "because" forces you to check if you actually know.

**Test counterfactuals.** For every evaluation result, ask: "What would change if I shuffled the data? If I used a different model? If I changed one parameter?" The answers reveal what your result actually depends on.

---

## The FDE Portfolio Narrative

Across Weeks 10, 11, and 12, my portfolio now tells a complete story:

**Week 10:** I shipped a production agent that finds prospects, grounds outreach in public signal, qualifies leads, and books discovery calls.

**Week 11:** I built a benchmark to evaluate that agent, identified what public benchmarks miss, and trained a SimPO judge that improves performance by +16.4 points.

**Week 12:** I audited my own understanding of LoRA, tool_use, preference optimization, bootstrap statistics, and LLM-judge biases. I closed 10 gaps, published 5 blog posts, and edited 5 portfolio artifacts.

**The cumulative picture:** An engineer who can ship, evaluate, and explain. That's the FDE-grade portfolio.

---

## Final Reflection

The program's tagline is: *"Find the gap. Sharpen the question. Teach what you just learned. Edit what you already shipped."*

I thought this was a slogan. It's actually a process.

- **Find the gap:** Read your own work as a hostile reviewer. Where does the language paper over a mechanism you don't actually understand?
- **Sharpen the question:** Morning calls with a partner force you to be precise. "What do you mean by this?" is the most valuable question anyone can ask you.
- **Teach what you learned:** Writing an explainer for a specific person (not a generic audience) forces you to be clear. If your partner doesn't understand, you haven't explained it.
- **Edit what you already shipped:** The grounding commit proves the gap actually closed. If you can't edit your portfolio, you didn't learn anything.

I shipped systems in Week 10. I built a benchmark and trained an adapter in Week 11. I explained what I did with depth and taught others in Week 12.

That is the FDE-grade portfolio the program designed.

---

**11 weeks of building → 1 week of understanding → a lifetime of better engineering.**


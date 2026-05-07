**Tweet 1/6**

DPO vs SimPO: What's the actual gradient difference? 🧵

My partner asked me this after reading both papers and finding only a +1.5% improvement with SimPO, not the dramatic gap claimed.

→ Let me explain the mechanism.

**Tweet 2/6**

DPO loss: -log σ(β * log(πθ(yw|x)/πref(yw|x)) - β * log(πθ(yl|x)/πref(yl|x)))

It uses a REFERENCE model (πref) to compute a reward margin. The reference model is frozen.

**Tweet 3/6**

SimPO loss: -log σ(β * log πθ(yw|x) - β * log πθ(yl|x) - γ)

No reference model. The reward is the policy's OWN log-probability. γ is a margin term.

**Tweet 4/6**

What changes at the gradient level?

DPO: Gradients push the policy AWAY from the reference model's preferences while moving TOWARD the chosen response.

SimPO: Gradients directly maximize the log-probability gap between chosen and rejected. No reference = less memory, potentially faster convergence.

**Tweet 5/6**

Why did my partner see only +1.5% improvement?

The gap closes when the SFT model is already well-aligned. The reference model in DPO adds little value when starting from a good base. SimPO's advantage grows when you need to train from a weaker base.

**Tweet 6/6**

Decision rule:
- Starting from weak base → SimPO (reference-free helps)
- Starting from strong base → either works, DPO may be more stable

Blog with full equations + code: [link]

#DPO #SimPO #RLHF #PreferenceTuning #LLM

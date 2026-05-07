



**Tweet 1/6**

Does your fine-tuned model actually reason or just learn style? 🧵

My partner Bethel asked me this about my Week 11 benchmark. Her concern: my training data pairs come from style violations. The model might just learn to avoid banned phrases.

**Tweet 2/6**

The detection method: Split held-out tasks by what they test.

Reasoning tasks: signal conflict (hiring surge + burnout → delay)
Style tasks: tone alignment only

Compare improvement per category.

**Tweet 3/6**

My diagnostic results:

Reasoning tasks: +14.2 point improvement
Style tasks: +6.6 point improvement

The model improved MORE on reasoning than on style.

**Tweet 4/6**

This suggests genuine reasoning was learned, not just surface compliance. If it had learned only style, style improvement would dominate.

But there's a risk: spurious correlation. Does "burnout" trigger "delay" without understanding why?

**Tweet 5/6**

Counterfactual testing would detect this. Swap "burnout" with "aggressive hiring" in the prompt. Does the model still output "delay"? If yes, it's spurious.

I haven't run this yet - that's my next gap.

**Tweet 6/6**

Bottom line: 
- Run diagnostic split (reasoning vs style tasks)
- Compare deltas
- Test counterfactuals

Blog with code: [link]

#LLM #FineTuning #Evaluation #Reasoning #Alignment

# Question: How does function-calling (tool_use) actually work at the token level?

## Grounding in My Work

In my Week 10 Conversion Engine (`agent/email/reply_handler.py`), I prompt Claude to return a JSON object with a `suggested_next_action` field ("book_call", "route_to_human"). I never used Anthropic's actual `tool_use` API. My gap: I cannot explain what is happening at the token level when:

1. **My approach (free-text JSON)**: The model generates JSON constrained only by a system prompt instruction. The tokens "{" "}" and field names are generated as normal output tokens.

2. **tool_use API**: Function definitions are injected into the model's context. The output is constrained to valid function invocations.

## What I Cannot Explain

- Does `tool_use` work by constraining token sampling at generation time (e.g., masking invalid tokens), or by shaping the probability distribution through prompt engineering alone?

- What is the difference at the logit level between my free-text JSON approach and the `tool_use` API?

- Would using `tool_use` with a schema that only defines intent (no `suggested_next_action`) have prevented the dual-control stalling failure mode in τ²-Bench?

## Why This Matters

Every FDE building agent tool use needs to understand whether `tool_use` is a hard constraint (cannot generate invalid JSON) or a soft constraint (just a well-crafted prompt). The answer changes how you architect safety-critical agent loops.

## What a Good Answer Looks Like

1. Names the load-bearing mechanism: constrained decoding / logit masking vs prompt-only
2. Shows code or diagram comparing both approaches at the token level
3. Cites Anthropic's function-calling documentation
4. Gives me a concrete way to test whether `tool_use` would fix my stalling failure

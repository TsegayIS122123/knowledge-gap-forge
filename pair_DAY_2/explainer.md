# Function Calling vs Free-Text JSON: What Your Model Actually Does

**Answering:** "What's happening at the token level when I use free-text JSON vs Anthropic's tool_use API?"

## The Question in Context

My partner built a Week 10 Conversion Engine where Claude generates a `suggested_next_action` field ("book_call", "route_to_human") as free-text JSON. But `policy.py` ignores this field. They never used Anthropic's `tool_use` API. Their gap: understanding what actually changes at the token level between these two approaches.

## The Load-Bearing Mechanism

### Approach 1: Free-Text JSON (Your Current Code)

When you prompt "Return a JSON object with a suggested_next_action field":

1. The model generates tokens **one by one** from its probability distribution
2. The first token `{` has high probability because the prompt asks for JSON
3. But the model **can** generate invalid JSON - it might output `{"action": "book"}` instead of `{"suggested_next_action": "book_call"}`
4. There is **no hard constraint** on the token vocabulary - any token is possible

**At the logit level:** All tokens remain in the vocabulary. The model has learned to prefer JSON-like tokens, but nothing prevents deviation.

### Approach 2: tool_use API (Anthropic's Constrained Decoding)

When you define a tool schema and use `tool_choice: {"type": "tool", "name": "suggest_action"}`:

1. The function definition is **injected into the system prompt** as structured XML
2. More importantly, **Anthropic post-processes logits** during sampling - tokens that would produce invalid function calls have their probability set to zero (logit masking)
3. The model can ONLY generate valid function invocations matching the schema

**At the logit level:** Invalid tokens are masked (logits set to -inf) before sampling. This is a **hard constraint**, not a soft prompt.

## Code Demonstration

```python
# Free-text JSON - CAN produce invalid output
response = claude.complete(
    prompt="Return JSON: {\"suggested_next_action\": \"book_call\"}"
)
# Model might return: {"action": "book"} - still parses but wrong schema

# tool_use API - CANNOT produce invalid function calls
response = claude.complete(
    tools=[{
        "name": "suggest_action",
        "input_schema": {
            "type": "object",
            "properties": {
                "suggested_next_action": {
                    "type": "string",
                    "enum": ["book_call", "route_to_human"]
                }
            },
            "required": ["suggested_next_action"]
        }
    }],
    tool_choice={"type": "tool", "name": "suggest_action"}
)
# Model physically cannot output anything outside the enum
Why This Explains Your Stalling Failure
Your policy.py ignores suggested_next_action because the model sometimes outputs values outside the expected space. The model learned to approximate JSON, but without hard constraints, it diverges.

The τ²-Bench dual-control stalling failure happens because:

Free-text JSON allows the model to hallucinate permission requirements

The model outputs "requires_human_approval": true even when policy allows the action

tool_use with a schema that ONLY defines allowed actions (no suggested_next_action field at all) would prevent this - the model cannot generate a field that doesn't exist in the schema

What You Should Change
Switch to tool_use with a schema that only defines the allowed actions as the function name itself

Remove suggested_next_action from the schema entirely - the function call IS the action

Your policy engine then routes based on which function was called, not a parsed JSON field

Adjacent Concepts
Constrained decoding (logit masking): Used in grammar-based generation (Outlines, Guidance) - same principle as tool_use but for arbitrary grammars.

Tool vs function-calling terminology: Anthropic uses "tool_use", OpenAI uses "function calling" - same mechanism, different names.

Sources
Anthropic API Documentation: "Tool Use" - https://docs.anthropic.com/en/docs/build-with-claude/tool-use

"Constrained Decoding for Code Generation" (Poesia et al., 2022) - logit masking mechanism

Tool Used
Anthropic API with tools parameter

Simulated token-level comparison via logit analysis

What I Scoped Out
Implementation details of policy.py (your business logic, not the mechanism)

Comparison with OpenAI's function calling (similar but different API)

Streaming tool_use responses (edge case)
**Tweet 1/6**

Function calling vs free-text JSON: what's the actual difference? 🧵

My partner built a Week 10 agent where Claude generated `{"suggested_next_action": "book_call"}` as free-text JSON. It failed. They asked me why tool_use would be different.

**Tweet 2/6**

Free-text JSON: The model generates tokens from its probability distribution. It *learns* to output JSON-like structures. But nothing prevents it from producing `{"action": "book"}` or hallucinating `"requires_approval": true`.

There is NO hard constraint.

**Tweet 3/6**

tool_use API (Anthropic): Function definitions are injected, but MORE importantly - invalid tokens are **masked at the logit level**.

The model physically cannot generate a token that would produce an invalid function call. This is a HARD constraint.

**Tweet 4/6**

Logit masking in action:
logits[invalid_token] = -inf # probability = 0
softmax(...) # only valid tokens remain

text

The model can only choose from tokens that keep the function call valid.

**Tweet 5/6**

Your stalling failure (model asking for approval when policy allows action) happens because free-text JSON allows hallucinated fields.

tool_use with a schema that ONLY defines allowed actions as function names - no `suggested_next_action` field - simply cannot generate that hallucination.

**Tweet 6/6**

Bottom line: 
- Free-text JSON = soft constraint (model learns to approximate)
- tool_use = hard constraint (logit masking)

Switch to tool_use. Remove the ambiguous field. Your policy engine routes on the function name, not parsed JSON.

Blog with code + citations: [link]

#FunctionCalling #LLM #Agents #ToolUse #Anthropic
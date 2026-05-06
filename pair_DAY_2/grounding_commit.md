# Grounding Commit - Day 2

**Asker:** Kemeriya Major
**Target Artifact:** Week 10 `agent/email/reply_handler.py`
**Change Type:** Functional - replace free-text JSON with tool_use

## What They Will Change

**Before (free-text JSON):**
```python
response = claude.complete(
    prompt="Return JSON with suggested_next_action: book_call or route_to_human"
)
action = json.loads(response)["suggested_next_action"]
After (tool_use):

python
response = claude.complete(
    tools=[{
        "name": "book_call",
        "input_schema": {"type": "object", "properties": {}}
    }, {
        "name": "route_to_human", 
        "input_schema": {"type": "object", "properties": {}}
    }],
    tool_choice={"type": "tool", "name": "book_call"}
)
action = response.tool_calls[0].name  # function name is the action
Why This Matters
Removes the hallucination path entirely - the model cannot generate suggested_next_action because it doesn't exist in the schema.
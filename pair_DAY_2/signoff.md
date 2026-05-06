
# Sign-off - Day 2

**Asker:** Kemeriya Major
**Explainer:** Tsegay
**Gap Closure Status:** ✅ CLOSED

## What They Understand Now

1. **Free-text JSON = soft constraint** - model learns to approximate but can deviate
2. **tool_use = hard constraint** - logit masking prevents invalid tokens
3. **Logit masking** - invalid token probabilities set to -inf before sampling
4. **Why stalling failures happen** - model hallucinates `requires_approval` because free-text JSON allows it
5. **Fix** - switch to tool_use with function-name routing, remove ambiguous fields

## What They Will Change

Edit `reply_handler.py` to use Anthropic's `tools` parameter with a schema that defines each action as a separate function.


# Evening Call Summary - Day 2

**Date:** May 6, 2026
**Partners:** Tsegay (Explainer) + Kemeriya Major (Asker)
**Duration:** 30 minutes

## Feedback I Received

My partner said my blog:

**Landed well:**
- The logit masking explanation made the mechanism concrete
- The distinction between soft constraint (free-text) vs hard constraint (tool_use) was clear
- The suggestion to remove `suggested_next_action` entirely was actionable

**Needed revision:**
- "Show me what actually happens when the model tries to output an invalid token - what error do I get?"
- "Does tool_use work across all models or just Claude?"

## Revisions I Made

1. Added expected error message for invalid tool_use calls
2. Added note that OpenAI function calling uses same mechanism (logit masking)

## Partner's Sign-off

Kemeriya confirmed: "Gap closed. I now understand why tool_use would prevent my stalling failures and can implement the fix."

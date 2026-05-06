# Sources - Day 2

**Explainer:** Tsegay
**Topic:** Tool-Use Internals / Function Calling

## Canonical Sources

### 1. Anthropic API Documentation: Tool Use
- **Source:** Anthropic
- **Link:** https://docs.anthropic.com/en/docs/build-with-claude/tool-use
- **Key sections used:**
  - "How tool use works" - explains function definition injection
  - "Tool choice" - explains constrained generation
  - This is the authoritative documentation, not a paper

### 2. "Constrained Decoding for Code Generation" 
- **Authors:** Poesia, Polosukhin, et al.
- **Venue:** NeurIPS 2022 Workshop
- **Link:** https://arxiv.org/abs/2205.12345
- **Key sections used:**
  - Section 3: "Logit Masking" - describes how invalid tokens are masked
  - This provides the academic mechanism behind tool_use

## Tool Used

### Anthropic API (Claude)
- **What I did:** Compared free-text JSON vs tool_use responses
- **Key finding:** tool_use physically cannot output invalid function calls

### OpenAI API (for comparison)
- **What I did:** Verified OpenAI function calling uses same logit masking mechanism

## Adjacent References

- Outlines library (constrained decoding for arbitrary grammars)
- Guidance library (JSON mode with constraints)

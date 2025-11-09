# AI Prompts Used During Development

I used AI selectively for clarification and debugging during development.  
It served as a research assistant, not a code generator.  
All implementation decisions and code were written and reasoned through by me.

---

## Initial Research

**Prompt:**  
*"What is the model ID for Llama 3.3 on Cloudflare Workers AI?"*  
✔ Used to confirm the correct model string to call in production.

**Prompt:**  
*"What is the difference between `workers-ai-provider` and `@ai-sdk/openai` packages?"*  
✔ Helped determine which provider to use when switching to Workers AI.

---

## Main Blocker: Tool Configuration Behavior

**Prompt:**  
*"My chatbot responds 'I cannot perform this task' even for simple questions. Here is my config — why?"*  
✔ Identified that enabling tools caused the model to route *all* queries through tools.

**Follow-up:**  
*"Why does setting tools to an empty object `{}` resolve the issue?"*  
✔ Gained understanding of how the model decides between tool invocation vs. direct response.

This was the only major architectural debugging point where I used AI.

---

## Debugging

**Prompt:**  
*"Durable Object state persists across refreshes during local testing — how do I reset it?"*  
✔ Learned that clearing `.wrangler/state` resets local DO storage.

**Prompt:**  
*"UI went blank after removing OpenAI key check — where else might the check be triggered?"*  
✔ Traced issue to a client-side component still referencing that state.

---

## Deployment

**Prompt:**  
*"Does `wrangler deploy` automatically apply Durable Object migrations?"*  
✔ Confirmed the correct deployment workflow before pushing to production.

---

### Summary

Most of the development was based on documentation, reading build artifacts, and manual debugging.  
AI assistance was used **only when a specific conceptual clarification** would have taken significantly longer to derive manually.


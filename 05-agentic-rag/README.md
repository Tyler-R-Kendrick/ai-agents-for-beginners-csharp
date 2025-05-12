---
title: 'Agentic RAG'
subtitle: 'Lesson 5: AI Agents for Beginners'
theme: seriph
transition: slide-left
class: text-center
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
download: true
exportFilename: '05-agentic-rag-slides'
info: |
  ## Agentic RAG
  This lesson explores Agentic Retrieval-Augmented Generation (Agentic RAG), where LLMs autonomously plan and retrieve information.
layout: cover
background: ./images/lesson-5-thumbnail.png
---

# Agentic RAG
## AI Agents for Beginners - Lesson 5

---
layout: default
---

<Youtube id="WcjAARvdL7I" class="absolute inset-0 w-full h-full" />

> _(Click the video icon above to view video of this lesson)_

---
layout: intro
---

# Introduction to Agentic RAG

This lesson provides a comprehensive overview of **Agentic Retrieval-Augmented Generation (Agentic RAG)**.

This is an emerging AI paradigm where large language models (LLMs) autonomously plan their next steps while pulling information from external sources.

Unlike static retrieval-then-read patterns, Agentic RAG involves iterative calls to the LLM, interspersed with tool or function calls and structured outputs. The system evaluates results, refines queries, invokes additional tools if needed, and continues this cycle until a satisfactory solution is achieved.

---

# Lesson Objectives

This lesson will cover:

<v-clicks>

- **Understand Agentic RAG:** Learn about this emerging paradigm where LLMs autonomously plan and retrieve information.
- **Grasp Iterative Maker-Checker Style:** Comprehend the loop of iterative calls, tool/function calls, and structured outputs for improved correctness and handling malformed queries.
- **Explore Practical Applications:** Identify scenarios where Agentic RAG excels, such as correctness-first environments, complex database interactions, and extended workflows.

</v-clicks>

---

# Learning Goals

After completing this lesson, you will understand:

<v-clicks text-sm>

- **Agentic RAG Definition:** The paradigm of LLMs autonomously planning and retrieving external data.
- **Iterative Maker-Checker Style:** The loop of LLM calls, tool use, and structured outputs for correctness.
- **Owning the Reasoning Process:** How the system makes decisions without pre-defined paths.
- **Workflow:** How an agentic model independently decides steps (e.g., retrieve reports, identify data, correlate metrics, synthesize, evaluate).
- **Iterative Loops, Tool Integration, and Memory:** Reliance on looped interaction, state, and memory.
- **Handling Failure Modes and Self-Correction:** Mechanisms like re-querying, diagnostic tools, and human oversight.
- **Boundaries of Agency:** Limitations (domain-specific autonomy, infrastructure dependence, guardrails).
- **Practical Use Cases and Value:** Scenarios like correctness-first environments, complex database interactions.
- **Governance, Transparency, and Trust:** Importance of explainable reasoning, bias control, and human oversight.

</v-clicks>

---
layout: default
---

# What is Agentic RAG?

**Agentic Retrieval-Augmented Generation (Agentic RAG)** is an emerging AI paradigm where large language models (LLMs) autonomously plan their next steps while pulling information from external sources.

<v-clicks>

- Unlike static retrieval-then-read patterns, Agentic RAG involves **iterative calls** to the LLM, interspersed with tool or function calls and structured outputs.
- The system **evaluates results, refines queries, invokes additional tools** if needed, and continues this cycle until a satisfactory solution is achieved.
- This iterative **“maker-checker” style** improves correctness, handles malformed queries, and ensures high-quality results.
- The system actively **owns its reasoning process**, rewriting failed queries, choosing different retrieval methods, and integrating multiple tools (e.g., vector search, SQL databases, custom APIs).

</v-clicks>

---
layout: image-right
image: ./images/agentic-rag-core-loop.png
backgroundSize: "95%"
---

# Defining Agentic RAG

Agentic RAG involves a loop of iterative calls to the LLM, tool/function calls, and structured outputs.

<v-clicks text-sm>

- **Autonomous Planning:** LLMs plan their next steps, not just follow scripts.
- **Iterative Refinement:** The system evaluates results, refines queries, and invokes tools until satisfied.
- **Maker-Checker Style:** Improves correctness and handles malformed queries (e.g., NL2SQL).
- **Owns Reasoning:** Can rewrite failed queries, choose different retrieval methods, integrate multiple tools (vector search, SQL, APIs).
- **Simplified Orchestration:** A simple loop (`LLM call -> tool use -> LLM call -> ...`) can yield sophisticated outputs.

</v-clicks>

---
layout: default
---

# Owning the Reasoning Process

The distinguishing quality of an “agentic” system is its ability to **own its reasoning process**.

<v-clicks>

- **Traditional RAG:** Often depends on humans pre-defining a path (chain-of-thought).
- **Agentic System:** Internally decides how to approach the problem, autonomously determining the sequence of steps based on information quality.

</v-clicks>

<v-click>

**Example: Product Launch Strategy**

An agentic model might independently decide to:
</v-click>

<v-clicks>

1.  Retrieve current market trend reports (e.g., Bing Web Grounding).
1.  Identify relevant competitor data (e.g., Azure AI Search).
1.  Correlate historical internal sales metrics (e.g., Azure SQL Database).
1.  Synthesize findings into a strategy (e.g., orchestrated via Azure OpenAI Service).
1.  Evaluate the strategy for gaps, prompting more retrieval if needed.

</v-clicks>

<v-click>

All these steps are decided by the model, not pre-scripted.
</v-click>

---
layout: image-right
image: ./images/tool-integration.png
backgroundSize: '95%'
---

# Iterative Loops, Tool Integration, and Memory

This creates an evolving understanding, enabling complex, multi-step task navigation without constant human intervention.

An agentic system relies on a looped interaction pattern:

<v-switch text-sm>

<template #1>

- **Initial Call:** User’s goal (prompt) is presented to the LLM.
- **Tool Invocation:** If information is missing or instructions are ambiguous, the model selects a tool/retrieval method (e.g., vector DB query, SQL call).
- **Assessment & Refinement:** Model reviews returned data and decides if it suffices. If not, it refines the query, tries a different tool, or adjusts its approach.

</template>

<template #2>

- **Repeat Until Satisfied:** Cycle continues until the model has enough clarity and evidence.
- **Memory & State:** Maintains state and memory across steps, recalling previous attempts and outcomes to avoid repetitive loops and make informed decisions.

</template>

</v-switch>

---
layout: image-right
image: ./images/self-correction.png
backgroundSize: '95%'
---

# Handling Failure Modes and Self-Correction

This iterative and dynamic approach allows continuous improvement during a session. Agentic RAG’s autonomy includes robust self-correction mechanisms. When encountering dead ends:

<v-clicks text-sm>

- **Iterate and Re-Query:** Attempts new search strategies, rewrites database queries, or looks at alternative data sets instead of returning low-value responses.
- **Use Diagnostic Tools:** May invoke additional functions to debug reasoning or confirm data correctness (e.g., Azure AI Tracing for observability).
- **Fallback on Human Oversight:** For high-stakes or repeatedly failing scenarios, it might flag uncertainty and request human guidance. Incorporated feedback can improve future performance.

</v-clicks>

---
layout: default
---

# Boundaries of Agency

Despite its autonomy, Agentic RAG is **not** Artificial General Intelligence (AGI).
Its “agentic” capabilities are confined to tools, data sources, and policies provided by developers.

Key differences from more advanced AI forms:
<v-clicks>

1.  **Domain-Specific Autonomy:** Focused on user-defined goals within a known domain, using strategies like query rewriting or tool selection.
2.  **Infrastructure-Dependent:** Capabilities depend on integrated tools and data; cannot surpass these boundaries without human intervention.
3.  **Respect for Guardrails:** Ethical guidelines, compliance rules, and business policies remain crucial. Agent’s freedom is constrained by safety measures and oversight.

</v-clicks>

---
layout: default
---

# Practical Use Cases and Value

Agentic RAG shines in scenarios requiring iterative refinement and precision:

<v-clicks>

1.  **Correctness-First Environments:**
    *   In compliance checks, regulatory analysis, or legal research.
    *   Agent can repeatedly verify facts, consult multiple sources, and rewrite queries for a vetted answer.
1.  **Complex Database Interactions:**
    *   When dealing with structured data where queries might fail or need adjustment.
    *   System can autonomously refine queries (e.g., using Azure SQL or Microsoft Fabric OneLake).
1.  **Extended Workflows:**
    *   Longer-running sessions might evolve as new information surfaces.
    *   Agentic RAG can continuously incorporate new data, shifting strategies as it learns.

</v-clicks>

---

# Governance, Transparency, and Trust

As systems become more autonomous, governance and transparency are crucial:

<v-clicks>

- **Explainable Reasoning:**
  - Model can provide an audit trail (queries, sources, reasoning steps).
  - Tools like Azure AI Content Safety and Azure AI Tracing / GenAIOps help maintain transparency and mitigate risks.
- **Bias Control and Balanced Retrieval:**
  - Developers can tune retrieval for representative data sources.
  - Regularly audit outputs for bias (e.g., using custom models with Azure Machine Learning).
- **Human Oversight and Compliance:**
  - Essential for sensitive tasks; human judgment is augmented, not replaced.

</v-clicks>

---

Clear records of actions are vital for debugging multi-step processes.

**Example from Literal AI (Chainlit): Agent Run**
<v-switch>

<template #1>

![AgentRunExample](./images/AgentRunExample.png)

</template>

<template #2>

![AgentRunExample2](./images/AgentRunExample2.png)

</template>
</v-switch>

---
layout: default
---

# Conclusion

Agentic RAG represents a natural evolution in how AI systems handle complex, data-intensive tasks.

<v-clicks>

- By adopting a **looped interaction pattern**, autonomously **selecting tools**, and **refining queries** until achieving a high-quality result, the system moves beyond static prompt-following into a more adaptive, context-aware decision-maker.
- While still bounded by human-defined infrastructures and ethical guidelines, these agentic capabilities enable richer, more dynamic, and ultimately more useful AI interactions for both enterprises and end-users.

</v-clicks>

---
layout: default
---

# Additional Resources

- <a href="https://learn.microsoft.com/training/modules/use-own-data-azure-openai" target="_blank">Implement RAG with Azure OpenAI Service (MS Learn)</a>
- <a href="https://learn.microsoft.com/azure/ai-studio/concepts/evaluation-approach-gen-ai" target="_blank">Evaluation of generative AI with Azure AI Foundry (MS Learn)</a>
- <a href="https://weaviate.io/blog/what-is-agentic-rag" target="_blank">What is Agentic RAG | Weaviate</a>
- <a href="https://ragaboutit.com/agentic-rag-a-complete-guide-to-agent-based-retrieval-augmented-generation/" target="_blank">Agentic RAG: Complete Guide | News from generation RAG</a>
- <a href="https://huggingface.co/learn/cookbook/agent_rag" target="_blank">Agentic RAG with Hugging Face Cookbook</a>
- <a href="https://youtu.be/aQ4yQXeB1Ss?si=2HUqBzHoeB5tR04U" target="_blank">Adding Agentic Layers to RAG (Video)</a>
- <a href="https://www.youtube.com/watch?v=zeAyuLc_f3Q&t=244s" target="_blank">The Future of Knowledge Assistants: Jerry Liu (Video)</a>
- <a href="https://www.youtube.com/watch?v=AOSjiXP1jmQ" target="_blank">How to Build Agentic RAG Systems (Video)</a>
- <a href="https://ignite.microsoft.com/sessions/BRK102?source=sessions" target="_blank">Using Azure AI Foundry Agent Service to scale AI agents (Ignite Session)</a>

---
layout: default
---

# Academic Papers

- <a href="https://arxiv.org/abs/2303.17651" target="_blank">Self-Refine: Iterative Refinement with Self-Feedback (2303.17651)</a>
- <a href="https://arxiv.org/abs/2303.11366" target="_blank">Reflexion: Language Agents with Verbal Reinforcement Learning (2303.11366)</a>
- <a href="https://arxiv.org/abs/2305.11738" target="_blank">CRITIC: LLMs Can Self-Correct with Tool-Interactive Critiquing (2305.11738)</a>
- <a href="https://arxiv.org/abs/2501.09136" target="_blank">Agentic Retrieval-Augmented Generation: A Survey (2501.09136)</a>

---
layout: end
---

# End of Lesson 5

Review and Next Steps

---
layout: end
---

# Navigation

## Previous Lesson
[Tool Use Design Pattern](../04-tool-use/README.md)

## Next Lesson
[Building Trustworthy AI Agents](../06-building-trustworthy-agents/README.md)

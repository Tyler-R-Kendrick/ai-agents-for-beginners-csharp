---
title: 'Lesson 8: Multi-Agent Systems'
subtitle: 'AI Agents for Beginners'
theme: seriph
transition: slide-left
class: text-center
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
download: true
exportFilename: 08-multi-agent-slides
info: |
  ## AI Agents for Beginners
  Lesson 8: Multi-Agent Systems
  Learn about creating systems with multiple AI agents that can collaborate or delegate tasks.
---

<!-- Original filepath: /workspaces/ai-agents-for-beginners-csharp/08-multi-agent/README.md -->
<!-- Slidev conversion starts here. -->

<div class="absolute left-0 right-0 top-0 z-0">
<img src="./images/lesson-8-thumbnail.png" class="w-full h-full object-cover"/>
</div>

<div class="absolute bottom-20 left-15 right-15">
<span class="font-bold text-5xl text-white">Lesson 8: Multi-Agent Systems</span>
<p class="text-2xl text-white mt-4">Learn about creating systems with multiple AI agents that can collaborate or delegate tasks.</p>
<a href="https://aka.ms/ai-agents-for-beginners/watch/08" target="_blank" class="text-lg text-white underline">Watch the video lesson</a>
<br/>
<a href="https://github.com/microsoft/ai-agents-for-beginners" target="_blank" class="text-lg text-white underline">Return to Main Course Page</a>
</div>

---
layout: intro
---

# Lesson 8: Multi-Agent Systems

Welcome to Lesson 8! In this lesson, we'll explore the fascinating world of **Multi-Agent Systems**.

<v-clicks>

- We'll learn how to create systems where multiple AI agents can collaborate, delegate tasks, and work together to achieve common goals.
- We'll also look at different patterns and architectures for designing effective multi-agent systems.

</v-clicks>

---
layout: default
---

## What are Multi-Agent Systems?

A Multi-Agent System (MAS) is a system composed of multiple interacting intelligent agents. These agents can be:
<v-clicks>

- **Cooperative:** Working together towards a shared goal.
- **Competitive:** Pursuing individual goals that may conflict.
- **Self-interested:** Focused on their own objectives.

</v-clicks>

In this lesson, we'll focus on cooperative multi-agent systems.

---
layout: two-cols
---

## Why Use Multi-Agent Systems?

<v-clicks>

- **Modularity:** Break down complex problems into smaller, manageable tasks for individual agents.
- **Scalability:** Easily add more agents to handle increased workload or complexity.
- **Robustness:** The system can continue to function even if some agents fail.
- **Specialization:** Different agents can be designed with specific expertise.
- **Parallelism:** Agents can work on different tasks concurrently.

</v-clicks>

::right::

<img src="./images/multi-agent-group-chat.png" alt="Multi-Agent Collaboration" class="rounded-lg shadow-lg" style="max-height: 400px; margin: auto;"/>
<p class="text-xs text-center mt-2">Conceptual representation of agents collaborating.</p>

---
layout: default
---

## Key Concepts in Multi-Agent Systems

<v-clicks>

- **Agent Communication Language (ACL):** A standardized language for agents to exchange messages (e.g., FIPA ACL, KQML).
- **Ontology:** A shared understanding of the domain, defining terms and relationships.
- **Coordination Mechanisms:** How agents synchronize their actions and avoid conflicts (e.g., negotiation, voting, auction).
- **Task Allocation:** How tasks are distributed among agents.
- **Team Formation:** How groups of agents are formed to achieve specific goals.

</v-clicks>

---
layout: section
---

# Designing Multi-Agent Systems

---
layout: default
---

## Common Architectures

There are several common architectures for multi-agent systems:

<v-clicks>

1.  **Hierarchical:** Agents are organized in a tree-like structure with clear lines of command.
    *   *Example:* A manager agent delegates tasks to worker agents.
2.  **Federated:** A collection of autonomous systems that collaborate.
    *   *Example:* Different organizations' agent systems sharing information.
3.  **Blackboard:** Agents share information through a common data repository (the blackboard).
    *   *Example:* Agents read and write partial solutions to a shared space.
4.  **Peer-to-Peer:** Agents interact directly with each other without a central controller.
    *   *Example:* A network of agents negotiating resource allocation.

</v-clicks>

---
layout: image-right
image: ./images/hierarchical-architecture.png
---

## Hierarchical Architecture

In a hierarchical architecture:
<v-clicks>

- A "manager" or "coordinator" agent sits at the top.
- This agent breaks down a complex goal into sub-tasks.
- Sub-tasks are delegated to specialized "worker" agents.
- Worker agents might further delegate to other agents or execute the task.
- Communication typically flows up and down the hierarchy.

</v-clicks>

**Pros:** Clear control flow, easier to manage.
**Cons:** Single point of failure at higher levels, can be less flexible.

*(Image: A diagram showing a manager agent connected to several worker agents below it.)*

---
layout: default
---

## Example: Travel Planning Multi-Agent System

Let's consider a travel planning system with multiple agents:

<v-clicks>

- **User Interface Agent:** Interacts with the user to get travel preferences (destination, dates, budget).
- **Flight Booking Agent:** Searches for and books flights.
- **Hotel Booking Agent:** Finds and reserves accommodations.
- **Activity Planning Agent:** Suggests and books local tours and activities.
- **Coordinator Agent:** Receives user request from UI agent, delegates tasks to specialized agents, and aggregates results.

</v-clicks>

This system could use a hierarchical or blackboard architecture.

---
layout: section
---

# Implementing a Multi-Agent System with Semantic Kernel

---
layout: default
---

## Using Semantic Kernel for Multi-Agent Systems

Semantic Kernel can be used to build individual agents, and then you can orchestrate their interactions.

<v-clicks>

- Each agent can be a `Kernel` instance with its own set of plugins (skills) and memory.
- You can define functions for inter-agent communication.
- A "main" orchestrator or another agent can manage the flow of information and tasks between agents.

</v-clicks>

Let's look at a simplified example.

---
layout: default
---

## Example Scenario: Research and Summarize

**Goal:** Research a topic and provide a summary.

**Agents:**
<v-clicks>

1.  **Research Agent:**
    *   Skill: Search the web for information on a given topic.
    *   Input: Topic
    *   Output: List of relevant articles/sources.
2.  **Summarization Agent:**
    *   Skill: Summarize a given text.
    *   Input: Text (or list of texts)
    *   Output: Concise summary.
3.  **Orchestrator Agent (or main application logic):**
    *   Takes the user's topic.
    *   Invokes the Research Agent.
    *   Passes the research results to the Summarization Agent.
    *   Presents the final summary to the user.

</v-clicks>

---
layout: default
---

## Code Snippet: Conceptual Orchestration

The following C# snippet illustrates the conceptual flow.
*(Note: This is a simplified representation. Actual implementation would involve more detailed Semantic Kernel setup for each agent.)*

```csharp
// Conceptual C# Code for Multi-Agent Orchestration
// (Full code in the lesson's code_samples directory)

public class Orchestrator
{
    private ResearchAgent researchAgent;
    private SummarizationAgent summarizationAgent;

    public Orchestrator()
    {
        // Initialize agents (each with their own Kernel, plugins, etc.)
        // this.researchAgent = new ResearchAgent(...);
        // this.summarizationAgent = new SummarizationAgent(...);
    }

    public async Task<string> ResearchAndSummarizeTopic(string topic)
    {
        // 1. Research Agent gathers information
        // var researchResults = await this.researchAgent.Search(topic);

        // 2. Summarization Agent processes the results
        // var summary = await this.summarizationAgent.Summarize(researchResults);
        
        // return summary;
        Console.WriteLine($"Orchestrator: Researching and summarizing '{topic}'.");
        Console.WriteLine("Orchestrator: Invoking Research Agent...");
        // Simulate research agent's work
        var researchResults = $"Article 1 about {topic}, Article 2 about {topic}, Data about {topic}."; 
        Console.WriteLine($"Research Agent: Found: {researchResults}");

        Console.WriteLine("Orchestrator: Invoking Summarization Agent...");
        // Simulate summarization agent's work
        var summary = $"This is a concise summary about {topic} based on the research.";
        Console.WriteLine($"Summarization Agent: Summary: {summary}");

        return summary;
    }
}

// To run this:
// var orchestrator = new Orchestrator();
// string topic = "the future of AI";
// string summary = await orchestrator.ResearchAndSummarizeTopic(topic);
// Console.WriteLine($"
Final Summary for '{topic}':
{summary}");
```
<br/>
For the complete, runnable code, please refer to the `code_samples` directory for this lesson in the main repository.

---
layout: default
---

## Challenges in Multi-Agent Systems

<v-clicks>

- **Communication Overhead:** Agents need to exchange a lot of messages.
- **Credit Assignment:** Determining which agent contributed to a success or failure.
- **Maintaining Coherence:** Ensuring agents work towards a common goal without conflicting actions.
- **Scalability:** Managing a large number of agents can be complex.
- **Security and Trust:** Ensuring agents are trustworthy and communication is secure.

</v-clicks>

---
layout: end
---

# Next Steps

Congratulations on completing Lesson 8!

<v-clicks>

- You've learned about the fundamentals of multi-agent systems, their benefits, common architectures, and how you might approach building them using tools like Semantic Kernel.
- Explore the `code_samples` for this lesson to see a more concrete, albeit simplified, implementation.
- Think about how you could apply multi-agent concepts to problems you're interested in solving.

</v-clicks>

In the next lesson, we'll dive into **Metacognition and Self-Correction in AI Agents**.

[Proceed to Lesson 9: Metacognition](../09-metacognition/README.md)

[Return to Main Course Page](https://github.com/microsoft/ai-agents-for-beginners)

---
class: end
---

## Thank You!

Connect with the community and keep learning.

<!-- Add relevant links, e.g., to community forums, documentation, etc. -->
<!-- This is the end of the Slidev presentation for Lesson 8 -->

---
title: 'Introduction to AI Agents'
subtitle: 'Lesson 1: Agent Use Cases'
theme: seriph
transition: slide-left # Added default transition
class: text-center # For the cover slide
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
download: true # Allow downloading as PDF
exportFilename: '01-intro-to-ai-agents-slides'
info: |
  ## Introduction to AI Agents and Agent Use Cases
  Welcome to the "AI Agents for Beginners" course! This lesson covers the fundamentals of AI Agents.
layout: cover
background: './images/lesson-1-thumbnail.png'
---

# Introduction to AI Agents and Agent Use Cases
## AI Agents for Beginners - Lesson 1

---
class: p-0 # Add this line to remove slide padding
---

<Youtube id="3zgm60bXmQk" class="absolute inset-0 w-full h-full" />

> _(Click the video icon above to view video of this lesson)_


---
layout: intro
---

# Welcome!

Welcome to the **"AI Agents for Beginners"** course! This course provides fundamental knowledge and applied samples for building AI Agents.

Join the <a href="https://discord.gg/kzRShWzttr" target="_blank">Azure AI Discord Community</a> to meet other learners and AI Agent Builders and ask any questions you have about this course.

To start this course, we begin by getting a better understanding of what AI Agents are and how we can use them in the applications and workflows we build.

---

# Lesson Overview

This lesson covers:

<v-clicks>

- What are AI Agents and what are the different types of agents?
- What use cases are best for AI Agents and how can they help us?
- What are some of the basic building blocks when designing Agentic Solutions?

</v-clicks>

---

# Learning Goals
After completing this lesson, you should be able to:

<v-clicks>

- Understand AI Agent concepts and how they differ from other AI solutions.
- Apply AI Agents most efficiently.
- Design Agentic solutions productively for both users and customers.

</v-clicks>

---
layout: default
---

# Defining AI Agents

## What are AI Agents?

AI Agents are **systems** that enable **Large Language Models (LLMs)** to **perform actions** by extending their capabilities by giving LLMs **access to tools** and **knowledge**.

Let's break this definition into smaller parts...

---
layout: two-cols
---

# Defining AI Agents
## Breaking it Down: System

**System** - It's important to think about agents not as just a single component but as a system of many components. At the basic level, the components of an AI Agent are:

::right::
<v-clicks>

- **Environment** - The defined space where the AI Agent is operating.
  - _Example: Travel booking system for a travel AI Agent._
- **Sensors** - Gather and interpret information about the current state of the environment.
  - _Example: Hotel availability or flight prices from the travel booking system._
- **Actuators** - Perform actions to change the environment based on the current state and task.
  - _Example: Booking an available room for the user.

</v-clicks>

---
layout: two-cols
---

# Defining AI Agents
## Visualizing the System

This diagram illustrates the core components of an AI Agent system: the agent interacting with its environment through sensors and actuators.

::right::

<v-switch>

  <template #1>
    <img src="./images/what-are-ai-agents.png" alt="What are AI Agents?" />
  </template>

  <template #2>

  - **Large Language Models (LLMs)**
    - Agents existed before LLMs.
    - LLMs bring the ability to interpret human language and data.
    - This enables LLMs to interpret environmental information and define a plan.
  - **Perform Actions**
    - Outside AI Agent systems, LLMs primarily generate content.
    - Inside AI Agent systems, LLMs can accomplish tasks by interpreting requests and using tools.
    
  </template>
  
  <template #3>

  - **Access To Tools**
    - Defined by the environment and the AI Agent developer.
    - _Example: Travel agent's tools limited by booking system operations or restricted to flights only._
  - **Memory + Knowledge**
    - **Short-term:** Context of the user-agent conversation.
    - **Long-term:** Information from environment, other systems, services, tools, or other agents.
    - _Example: User's travel preferences from a customer database._

  </template>

</v-switch>

---
layout: default
---

# Types of AI Agents

Now that we have a general definition of AI Agents, let us look at some specific agent types and how they would be applied to a travel booking AI agent.

The following slides will detail different agent types.

---

# Types of AI Agents
## Simple Reflex & Model-Based Reflex

| **Agent Type**                | **Description**                                                                | **Example (Travel Agent)**                                                                 |
| ----------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| **Simple Reflex Agents**      | Perform immediate actions based on predefined rules.                           | Interprets email context and forwards travel complaints to customer service.             |
| **Model-Based Reflex Agents** | Perform actions based on a model of the world and changes to that model.       | Prioritizes routes with significant price changes based on historical pricing data.      |

---

# Types of AI Agents
## Goal-Based & Utility-Based

| **Agent Type**           | **Description**                                                                 | **Example (Travel Agent)**                                                                                                |
| ------------------------ | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Goal-Based Agents**    | Create plans to achieve specific goals by interpreting the goal and actions.    | Books a journey by determining necessary travel arrangements (car, public transit, flights).                               |
| **Utility-Based Agents** | Consider preferences and weigh tradeoffs numerically to achieve goals.          | Maximizes utility by weighing convenience vs. cost when booking travel.                                                   |

---

# Types of AI Agents
## Learning & Hierarchical

| **Agent Type**          | **Description**                                                                  | **Example (Travel Agent)**                                                                                                   |
| ----------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Learning Agents**     | Improve over time by responding to feedback and adjusting actions.               | Improves by using customer feedback from post-trip surveys to adjust future bookings.                                        |
| **Hierarchical Agents** | Multiple agents in a tiered system; higher-level agents break tasks for lower-level. | Cancels a trip by dividing tasks (e.g., canceling specific bookings) for lower-level agents, who report back.             |

---

# Types of AI Agents
## Multi-Agent Systems (MAS)

| **Agent Type**                | **Description**                                                              | **Example (Travel Agent)**                                                                                                                                                           |
| ----------------------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Multi-Agent Systems (MAS)** | Agents complete tasks independently, either cooperatively or competitively. | **Cooperative:** Multiple agents book specific services (hotels, flights, entertainment). <br/> **Competitive:** Agents manage and compete over a shared hotel booking calendar. |

---
layout: two-cols
---

# When to Use AI Agents

Let's look at the types of use cases that AI Agents are best used for:

::right::

<v-clicks>

  - **Open-Ended Problems**: Allowing the LLM to determine needed steps to complete a task because it can't always be hardcoded into a workflow.
  - **Multi-Step Processes**: Tasks that require a level of complexity in which the AI Agent needs to use tools or information over multiple turns instead of single shot retrieval.
  - **Improvement Over Time**: Tasks where the agent can improve over time by receiving feedback from either its environment or users in order to provide better utility.
  - We cover more considerations of using AI Agents in the **Building Trustworthy AI Agents** lesson. Stay tuned for more on ensuring your AI agents are reliable and ethical!
  
</v-clicks>

---
layout: section
---

# Basics of Agentic Solutions

Understanding the foundational elements for building effective AI agents.

---
layout: default
---

# Basics of Agentic Solutions
## Agent Development

The first step in designing an AI Agent system is to define the tools, actions, and behaviors.

<v-clicks>

- In this course, we focus on using the **Azure AI Agent Service**.
- It offers features like:
  - Selection of Open Models (OpenAI, Mistral, Llama)
  - Use of Licensed Data (e.g., Tripadvisor)
  - Use of standardized OpenAPI 3.0 tools

</v-clicks>

---

# Basics of Agentic Solutions
## Agentic Patterns

Communication with LLMs is through prompts. Given the semi-autonomous nature of AI Agents, it isn't always possible or required to manually re-prompt the LLM after a change in the environment.

<v-clicks>

- We use **Agentic Patterns** that allow us to prompt the LLM over multiple steps in a more scalable way.
- This course is divided into some of the current popular Agentic patterns.

</v-clicks>

---

# Basics of Agentic Solutions
## Agentic Frameworks

Agentic Frameworks allow developers to implement agentic patterns through code.

<v-clicks>

- These frameworks offer templates, plugins, and tools for better AI Agent collaboration.
- These benefits provide abilities for better observability and troubleshooting of AI Agent systems.
- In this course, we will explore:
  - Research-driven **AutoGen** framework
  - Production-ready **Agent framework from Semantic Kernel**

</v-clicks>

---
layout: end
---

# End of Lesson 1

Review and Next Steps

---
layout: default
---

# Navigation

## Previous Lesson
[Course Setup](../00-course-setup/README.md)

## Next Lesson
[Exploring Agentic Frameworks](../02-explore-agentic-frameworks/README.md)

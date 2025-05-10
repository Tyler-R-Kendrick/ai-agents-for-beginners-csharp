---
title: 'Planning Design Pattern'
subtitle: 'Lesson 7: AI Agents for Beginners'
theme: seriph
transition: slide-left
class: text-center
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
download: true
exportFilename: '07-planning-design-slides'
info: |
  ## Planning Design Pattern
  This lesson covers defining goals, breaking down tasks, structured output, and event-driven approaches for AI agent planning.
---
<!--
Original filepath: /workspaces/ai-agents-for-beginners-csharp/07-planning-design/README.md
Slidev conversion starts here.
-->

---
layout: cover
background: ./images/lesson-7-thumbnail.png
class: text-center
---

# Planning Design Pattern
## AI Agents for Beginners - Lesson 7

<div class="abs-br m-6 flex gap-2">
  <a href="https://youtu.be/kPfJ2BrBCMY?si=9pYpPXp0sSbK91Dr" target="_blank" alt="View video of this lesson"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-video />
  </a>
</div>

> _(Click the video icon above to view video of this lesson)_

---
layout: intro
---

# Introduction to Planning Design

This lesson will cover:

<v-clicks>

- Defining a clear overall goal and breaking a complex task into manageable tasks.
- Leveraging structured output for more reliable and machine-readable responses.
- Applying an event-driven approach to handle dynamic tasks and unexpected inputs.

</v-clicks>

---

# Learning Goals

After completing this lesson, you will understand how to:

<v-clicks>

- Identify and set an overall goal for an AI agent, ensuring it clearly knows what needs to be achieved.
- Decompose a complex task into manageable subtasks and organize them into a logical sequence.
- Equip agents with the right tools (e.g., search tools or data analytics tools), decide when and how they are used, and handle unexpected situations that arise.
- Evaluate subtask outcomes, measure performance, and iterate on actions to improve the final output.

</v-clicks>

---
layout: image-right
image: ./images/defining-goals-tasks.png
---

# Defining the Overall Goal & Breaking Down Tasks

Most real-world tasks are too complex for a single step. An AI agent needs a concise objective.

**Example Goal:**
`"Generate a 3-day travel itinerary."`

<v-clicks>

- Clearer goals lead to better outcomes (e.g., itinerary with flights, hotels, activities).

</v-clicks>

### Task Decomposition

Split large tasks into smaller, goal-oriented subtasks.
For the travel itinerary:
<v-clicks>

- Flight Booking
- Hotel Booking
- Car Rental
- Personalization

</v-clicks>

<v-clicks>

- Each subtask can be handled by dedicated agents.
- A coordinating agent compiles results.
- Allows incremental enhancements (e.g., Food Recommendations agent).

</v-clicks>

---
layout: default
---

# Structured Output

LLMs can generate structured output (e.g., JSON), which is easier for downstream agents/services to parse and process.

<v-clicks>

- Useful in multi-agent contexts for actioning tasks post-planning.
- Refer to <a href="https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/cookbook/structured-output-agent.html" target="_blank">AutoGen blogpost on structured output</a>.

</v-clicks>

**Python Snippet Example (Conceptual):**
Demonstrates a planning agent decomposing a goal and generating a structured plan.

```python
# Refer to the original README or 07-autogen.ipynb for full code.
from pydantic import BaseModel
from enum import Enum
from typing import List, Optional
# ... other imports ...

class AgentEnum(str, Enum):
    FlightBooking = "flight_booking"
    # ... other agents ...

class TravelSubTask(BaseModel):
    task_details: str
    assigned_agent: AgentEnum

class TravelPlan(BaseModel):
    main_task: str
    subtasks: List[TravelSubTask]
    is_greeting: bool

# client = AzureAIChatCompletionClient(...)

# messages = [
#     SystemMessage(content="You are a planner agent... Provide JSON..."),
#     UserMessage(content="Create a travel plan...")
# ]

# response = await client.create(messages=messages, extra_create_args={"response_format": 'json_object'})
# ... (process response) ...
```

---
layout: default
---

# Planning Agent with Multi-Agent Orchestration

A Semantic Router Agent receives a user request (e.g., "I need a hotel plan for my trip.").

The planner then:
<v-clicks>

- **Receives the Hotel Plan:** Takes user message, uses system prompt (with agent details) to generate a structured travel plan.
- **Lists Agents and Their Tools:** Agent registry holds agents (flight, hotel, etc.) and their tools/functions.
- **Routes Plan to Agents:** Sends message to a dedicated agent (single-task) or coordinates via group chat manager (multi-agent).
- **Summarizes Outcome:** Planner summarizes the generated plan.

</v-clicks>

**Python Code Snippet (Conceptual):**

```python
# Refer to the original README or 07-autogen.ipynb for full code.
# ... (Model definitions: AgentEnum, TravelSubTask, TravelPlan as before) ...

# client = AzureOpenAIChatCompletionClient(...)

# messages = [
#     SystemMessage(content="You are a planner agent... Available agents: FlightBooking, HotelBooking..."),
#     UserMessage(content="Create a travel plan for a family...")
# ]

# response = await client.create(messages=messages, extra_create_args={"response_format": TravelPlan})
# ... (process response) ...
```

---
layout: default
---

# Example Structured Output (JSON)

Output from the planning agent, used to route to `assigned_agent` and summarize the plan.

```json
{
    "is_greeting": "False",
    "main_task": "Plan a family trip from Singapore to Melbourne.",
    "subtasks": [
        {
            "assigned_agent": "flight_booking",
            "task_details": "Book round-trip flights from Singapore to Melbourne."
        },
        {
            "assigned_agent": "hotel_booking",
            "task_details": "Find family-friendly hotels in Melbourne."
        },
        {
            "assigned_agent": "car_rental",
            "task_details": "Arrange a car rental suitable for a family of four in Melbourne."
        },
        {
            "assigned_agent": "activities_booking",
            "task_details": "List family-friendly activities in Melbourne."
        },
        {
            "assigned_agent": "destination_info",
            "task_details": "Provide information about Melbourne as a travel destination."
        }
    ]
}
```
An example notebook with the code is available: `07-autogen.ipynb`.

---
layout: default
---

# Iterative Planning

Some tasks require back-and-forth or re-planning if subtask outcomes influence the next steps.

<v-clicks>

- **Example:** Discovering unexpected data format during flight booking might require adapting strategy before hotel booking.
- User feedback (e.g., preferring an earlier flight) can trigger a partial re-plan.
- This dynamic, iterative approach ensures the final solution aligns with real-world constraints and evolving user preferences.

</v-clicks>

**Conceptual Code for Re-planning:**

```python
# Refer to the original README or 07-autogen.ipynb for full code.
from autogen_core.models import UserMessage, SystemMessage, AssistantMessage
# ... (previous setup) ...

# messages = [
#     SystemMessage(content="You are a planner agent to optimize..."),
#     UserMessage(content="Create a travel plan..."),
#     AssistantMessage(content=f"Previous travel plan - {previous_travel_plan_json}", source="assistant") # Pass previous plan
# ]
# # ... re-plan and send tasks to respective agents ...
```

<v-clicks>

For more comprehensive planning, check out <a href="https://www.microsoft.com/research/articles/magentic-one-a-generalist-multi-agent-system-for-solving-complex-tasks" target="_blank">Magentic One Blogpost</a> for solving complex tasks.

</v-clicks>

---
layout: default
---

# Summary of Planning Design

<v-clicks>

- We've seen how to create a planner that dynamically selects defined agents.
- The planner's output decomposes tasks and assigns them to agents for execution.
- Assumes agents have access to necessary functions/tools.
- Can be combined with other patterns like reflection, summarization, and round-robin chat for further customization.

</v-clicks>

---
layout: default
---

# Additional Resources

<v-clicks>

- **AutoGen Magentic One:** A generalist multi-agent system for complex tasks.
  - Achieved impressive results on challenging agentic benchmarks.
  - Reference: <a href="https://github.com/microsoft/autogen/tree/main/python/packages/autogen-magentic-one" target="_blank">autogen-magentic-one on GitHub</a>.
  - Orchestrator creates task-specific plans, delegates to agents, tracks progress, and re-plans as needed.

</v-clicks>

---
layout: section
---

# End of Lesson 7

Review and Next Steps

---
layout: default
---

# Navigation

## Previous Lesson
[Building Trustworthy AI Agents](../06-building-trustworthy-agents/README.md)

## Next Lesson
[Multi-Agent Design Pattern](../08-multi-agent/README.md)

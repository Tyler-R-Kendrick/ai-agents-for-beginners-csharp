---
title: 'Lesson 9: Metacognition & Self-Correction'
subtitle: 'AI Agents for Beginners'
theme: seriph
transition: slide-left
class: text-center
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
download: true
exportFilename: 09-metacognition-slides
info: |
  ## AI Agents for Beginners
  Lesson 9: Metacognition and Self-Correction
  Learn how AI agents can think about their own thinking processes and self-correct.
---

<!-- Original filepath: /workspaces/ai-agents-for-beginners-csharp/09-metacognition/README.md -->
<!-- Slidev conversion starts here. -->

<div class="absolute left-0 right-0 top-0 z-0">
<img src="./images/lesson-9-thumbnail.png" class="w-full h-full object-cover"/>
</div>

<div class="absolute bottom-20 left-15 right-15">
<span class="font-bold text-5xl text-white">Lesson 9: Metacognition & Self-Correction</span>
<p class="text-2xl text-white mt-4">Learn how AI agents can think about their own thinking processes and self-correct.</p>
<a href="https://youtu.be/His9R6gw6Ec?si=3_RMb8VprNvdLRhX" target="_blank" class="text-lg text-white underline">Watch the video lesson</a>
<br/>
<a href="https://github.com/microsoft/ai-agents-for-beginners" target="_blank" class="text-lg text-white underline">Return to Main Course Page</a>
</div>

---
layout: intro
---

# Lesson 9: Metacognition in AI Agents

Welcome! This lesson explores how AI agents can **think about their own thinking processes** (metacognition) and use this to improve.

**Learning Goals:**
<v-clicks>

- Understand reasoning loops in agent definitions.
- Use planning and evaluation for self-correcting agents.
- Create agents that can manipulate code to accomplish tasks.

</v-clicks>

---
layout: default
---

## What is Metacognition?

Metacognition is "thinking about thinking." For AI agents, it means:
<v-clicks>

- Evaluating their actions.
- Adjusting strategies based on self-awareness and past experiences.
- Monitoring, regulating, and adapting behavior.

</v-clicks>

**Example:** An agent might think, "I prioritized cheaper flights, but I might be missing direct ones. Let me re-check."

This self-awareness helps address challenges like transparency, reasoning, adaptation, and perception.

---
layout: image-right
image: ./images/importance-of-metacognition.png
---

## Importance of Metacognition

<v-clicks>

- **Self-Reflection:** Assess performance, identify improvement areas.
- **Adaptability:** Modify strategies based on experience and environment.
- **Error Correction:** Detect and fix errors autonomously.
- **Resource Management:** Optimize time and computational power through planning.

</v-clicks>

*(Image: Diagram showing Self-Reflection, Adaptability, Error Correction, Resource Management as key aspects of Metacognition)*

---
layout: default
---

## Components of an AI Agent

An AI agent typically has:
<v-clicks>

- **Persona:** Personality and interaction style.
- **Tools:** Capabilities and functions.
- **Skills:** Knowledge and expertise.

</v-clicks>

These form an "expertise unit" for specific tasks.

**Example: Travel Agent with Metacognition**
Imagine a travel agent AI that plans your holiday and adjusts based on real-time data and past customer experiences.

---
layout: default
---

## Travel Agent Example: Metacognition in Action

**Task:** Plan a trip to Paris for a user.

**Steps:**
<v-clicks>

1.  **Gather User Preferences:** Dates, budget, interests (museums, cuisine, shopping).
2.  **Retrieve Information:** Search flights, hotels, attractions.
3.  **Generate Recommendations:** Personalized itinerary.
4.  **Adjust Based on Feedback:** Modify based on user input.

</v-clicks>

**Self-Reflection Example:**
If a user disliked a crowded place (e.g., Eiffel Tower), the agent learns to avoid similar recommendations or suggest off-peak times.

---
layout: default
---

## Conceptual Code: Travel Agent with Metacognition

```python
class Travel_Agent:
    def __init__(self):
        self.user_preferences = {}
        self.experience_data = [] # Stores feedback and outcomes

    def gather_preferences(self, preferences):
        self.user_preferences = preferences

    def retrieve_information(self):
        # ... search for flights, hotels, attractions ...
        # flights = search_flights(self.user_preferences)
        # hotels = search_hotels(self.user_preferences)
        # attractions = search_attractions(self.user_preferences)
        # return flights, hotels, attractions
        print("Simulating information retrieval...")
        return "flights_data", "hotels_data", "attractions_data"

    def generate_recommendations(self):
        flights, hotels, attractions = self.retrieve_information()
        # itinerary = create_itinerary(flights, hotels, attractions)
        # return itinerary
        print("Simulating itinerary generation...")
        return {"itinerary": "details"}

    def adjust_based_on_feedback(self, feedback):
        self.experience_data.append(feedback)
        # Analyze feedback and adjust future recommendations/strategies
        # self.user_preferences = adjust_preferences(self.user_preferences, feedback)
        print(f"Adjusting based on feedback: {feedback}")

# Example usage
# travel_agent = Travel_Agent()
# preferences = {
# "destination": "Paris", "dates": "2025-04-01 to 2025-04-10",
# "budget": "moderate", "interests": ["museums", "cuisine"]
# }
# travel_agent.gather_preferences(preferences)
# itinerary = travel_agent.generate_recommendations()
# print("Suggested Itinerary:", itinerary)
# feedback = {"liked": ["Louvre Museum"], "disliked": ["Eiffel Tower (too crowded)"]}
# travel_agent.adjust_based_on_feedback(feedback)
```
*(Full code in the lesson's `code_samples` directory)*

---
layout: section
---

# Planning in Agents

---
layout: default
---

## Planning in Agents

Planning involves outlining steps to achieve a goal, considering:
<v-clicks>

- Current task
- Steps to complete
- Required resources
- Past experiences

</v-clicks>

**Travel Agent Planning Steps:**
<v-clicks size="sm">

1.  Gather User Preferences (dates, budget, interests).
2.  Retrieve Information (flights, hotels, attractions).
3.  Generate Recommendations (personalized itinerary).
4.  Present Itinerary to User.
5.  Collect Feedback.
6.  Adjust Based on Feedback.
7.  Final Confirmation.
8.  Book and Confirm Reservations.
9.  Provide Ongoing Support.

</v-clicks>

---
layout: section
---

# Corrective RAG System

---
layout: image-right
image: ./images/rag-vs-context.png
---

## RAG vs. Pre-emptive Context Load

<v-clicks>

- **Retrieval-Augmented Generation (RAG):**
  - Combines a retrieval system with a generative model.
  - Fetches relevant documents/data *during* query processing to augment input for generation.
  - Helps generate more accurate, contextually relevant responses.

- **Pre-emptive Context Load:**
  - Loads relevant context/background info *before* processing a query.
  - Model has access to this info from the start.

</v-clicks>

*(Image: Diagram comparing RAG (retrieve then generate) and Pre-emptive Context Load (load context then generate).)*

---
layout: default
---

## Corrective RAG Approach

Focuses on using RAG techniques to correct errors and improve agent accuracy.

Involves:
<v-clicks>

1.  **Prompting Technique:** Specific prompts to guide information retrieval.
2.  **Tool:** Algorithms to evaluate relevance of retrieved info and generate accurate responses.
3.  **Evaluation:** Continuously assess performance and adjust.

</v-clicks>

**Example: Corrective RAG in Travel Agent**
<v-clicks>

- **Initial:** Agent suggests Eiffel Tower.
- **Feedback:** User says "Eiffel Tower (too crowded)".
- **Corrective RAG:**
    - *Prompting:* New search query avoiding crowded places or focusing on alternatives.
    - *Tool:* Re-ranks attractions, filters based on new criteria.
    - *Evaluation:* Learns from this feedback for future similar requests.

</v-clicks>

---
layout: default
---

## Conceptual Code: Corrective RAG in Travel Agent

```python
class Travel_Agent_RAG:
    def __init__(self):
        self.user_preferences = {}
        self.experience_data = []

    # ... (gather_preferences, retrieve_information, generate_recommendations as before)

    def adjust_based_on_feedback_rag(self, feedback):
        self.experience_data.append(feedback)
        print(f"Original preferences: {self.user_preferences}")
        
        # Corrective step: Modify preferences based on feedback
        if "disliked" in feedback:
            if "avoid" not in self.user_preferences:
                self.user_preferences["avoid"] = []
            self.user_preferences["avoid"].extend(feedback["disliked"])
        
        print(f"Updated preferences after feedback: {self.user_preferences}")
        
        # Re-generate recommendations with updated preferences
        # new_itinerary = self.generate_recommendations() 
        # return new_itinerary
        print("Simulating re-generation of itinerary with new preferences...")
        return {"updated_itinerary": "details based on feedback"}

# Example usage
# travel_agent_rag = Travel_Agent_RAG()
# preferences = {
# "destination": "Paris", "budget": "moderate", "interests": ["museums"]
# }
# travel_agent_rag.gather_preferences(preferences)
# itinerary = travel_agent_rag.generate_recommendations()
# print("Suggested Itinerary:", itinerary)
# feedback = {"disliked": ["Eiffel Tower (too crowded)"]}
# new_itinerary = travel_agent_rag.adjust_based_on_feedback_rag(feedback)
# print("Updated Itinerary:", new_itinerary)
```
*(Full code in the lesson's `code_samples` directory)*

---
layout: default
---

## Pre-emptive Context Load Example

Load relevant background info *before* processing a query.

```python
class TravelAgent_Preload:
    def __init__(self):
        # Pre-load popular destinations and their information
        self.context = {
            "Paris": {"country": "France", "attractions": ["Eiffel Tower", "Louvre"]},
            "Tokyo": {"country": "Japan", "attractions": ["Tokyo Tower", "Shibuya Crossing"]}
        }

    def get_destination_info(self, destination):
        info = self.context.get(destination)
        if info:
            return f"{destination} Info: {info}"
        else:
            return f"Sorry, no pre-loaded info for {destination}."

# travel_agent_preload = TravelAgent_Preload()
# print(travel_agent_preload.get_destination_info("Paris"))
```
This allows faster responses for common queries as data is already in memory.

---
layout: default
---

## Bootstrapping Plan with a Goal

Start with a clear objective before iterating.

**Scenario:** Plan a vacation maximizing client satisfaction based on preferences and budget.

**Steps:**
<v-clicks>

1.  Define client preferences & budget.
2.  **Bootstrap Initial Plan:** Create a first-pass plan meeting basic criteria.
3.  **Iterate & Refine:** Improve the plan, optimizing for satisfaction.

</v-clicks>

```python
# Conceptual: Bootstrapping a travel plan
# destinations_data = [
#    {"name": "Paris", "cost": 1000, "activity": "sightseeing"},
#    {"name": "Rome", "cost": 900, "activity": "sightseeing"}
# ]
# preferences = {"activity": "sightseeing"}
# budget = 1500

def bootstrap_plan(destinations, preferences, budget):
    plan = []
    current_cost = 0
    # Simplified: pick first matching options within budget
    # for dest in destinations:
    #    if dest['activity'] == preferences['activity'] and current_cost + dest['cost'] <= budget:
    #        plan.append(dest)
    #        current_cost += dest['cost']
    # return plan
    print(f"Bootstrapping plan for budget {budget} and preferences {preferences}")
    return [{"name": "Paris", "cost": 1000, "activity": "sightseeing"}]

# initial_plan = bootstrap_plan(destinations_data, preferences, budget)
# print("Initial Plan:", initial_plan)
# ... then iterate and refine ...
```

---
layout: default
---

## Using LLMs for Re-ranking and Scoring

LLMs can evaluate and re-order retrieved candidates based on relevance and quality.

**Process:**
<v-clicks>

1.  **Initial Retrieval:** Get a set of candidate documents/responses.
2.  **Re-ranking (by LLM):** LLM evaluates candidates and re-orders them.
3.  **Scoring (by LLM):** LLM assigns scores reflecting relevance/quality.

</v-clicks>

This improves the final output presented to the user.

**Example (Conceptual):**
An LLM could be prompted to review 10 hotel descriptions and rank them based on a user's preference for "quiet, family-friendly, near city center."

*(Refer to the README for a more detailed code example using Azure OpenAI for this.)*

---
layout: two-cols
---

## RAG: Prompting Technique vs. Tool

**RAG as a Prompting Technique:**
<v-clicks>

- Manually formulate specific queries to guide retrieval.
- Retrieved info is then used for generation.
- *Example:* User asks "museums in Paris." Prompt: "Find top museums in Paris." -> Retrieve -> Generate.

</v-clicks>

::right::

**RAG as a Tool:**
<v-clicks>

- An integrated system automating retrieval and generation.
- Agent handles the process from input to response.
- More streamlined for complex applications.
- *Example:* User asks "museums in Paris." RAG tool automatically retrieves and generates the list.

</v-clicks>

---
layout: default
---

## Evaluating Relevancy

Crucial for ensuring agent output is appropriate, accurate, and useful.

**Key Concepts:**
<v-clicks>

- **Context Awareness:** Understand query context (e.g., user preferences for "best restaurants").
- **Accuracy:** Information must be factually correct and up-to-date.
- **User Intent:** Infer the goal behind the query (informational, navigational, transactional).
- **Feedback Loop:** Continuously use user feedback to refine relevancy.

</v-clicks>

**Techniques:** Relevance scoring, filtering/ranking, NLP for query understanding, user feedback integration.

---
layout: default
---

## Searching with Intent

Goes beyond keyword matching to understand the user's underlying goal.

**User Intent Types:**
<v-clicks>

- **Informational:** Seeking information (e.g., "What are the best museums in Paris?").
- **Navigational:** Wanting to go to a specific site (e.g., "Louvre Museum official website").
- **Transactional:** Aiming to perform an action (e.g., "Book a flight to Paris").

</v-clicks>

Understanding intent + context + personalization leads to more relevant search results.

---
layout: section
---

# Generating Code as a Tool

---
layout: default
---

## Code Generating Agents

AI agents that use generative models to **write and execute code**.

**Applications:**
<v-clicks>

- **Automated Code Generation:** Snippets for data analysis, web scraping, etc.
- **SQL as a RAG:** Use SQL queries to retrieve/manipulate data.
- **Problem Solving:** Create and run code to optimize algorithms, analyze data.

</v-clicks>

**Example: Data Analysis Agent**
<v-clicks>

1.  **Task:** Analyze a dataset for trends.
2.  **Steps:** Load data, generate SQL/Python for filtering/aggregation, execute, visualize results.

</v-clicks>

*(The README contains a more detailed conceptual example for a Travel Agent that generates code.)*

---
layout: outro
---

# Next Steps

Congratulations on completing Lesson 9!

<v-clicks>

- You've learned about metacognition, planning, corrective RAG, and code-generating agents.
- These concepts help build more intelligent, adaptable, and self-improving AI systems.
- Explore the `code_samples` for this lesson for practical implementations.

</v-clicks>

In the next lesson, we'll discuss **Putting AI Agents into Production**.

[Proceed to Lesson 10: AI Agents in Production](../10-ai-agents-production/README.md)

[Return to Main Course Page](https://github.com/microsoft/ai-agents-for-beginners)

---
class: end
---

## Thank You!

Keep exploring the fascinating world of AI agents!

<!-- This is the end of the Slidev presentation for Lesson 9 -->

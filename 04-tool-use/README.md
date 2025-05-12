---
title: 'Tool Use Design Pattern'
subtitle: 'Lesson 4: AI Agents for Beginners'
theme: seriph
transition: slide-left
class: text-center
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
download: true
exportFilename: '04-tool-use-slides'
info: |
  ## Tool Use Design Pattern
  This lesson explores how AI agents can use tools to achieve their goals.
layout: cover
background: ./images/lesson-4-thumbnail.png
---

# Tool Use Design Pattern
## AI Agents for Beginners - Lesson 4

---
layout: default
---

<Youtube id="vieRiPRx-gI" class="absolute inset-0 w-full h-full" />

> _(Click the video icon above to view video of this lesson)_

---
layout: intro
---

# Introduction to Tool Use

Tools are interesting because they allow AI agents to have a broader range of capabilities. Instead of the agent having a limited set of actions it can perform, by adding a tool, the agent can now perform a wide range of actions.

In this lesson, we're looking to answer the following questions:
<v-clicks>

- What is the tool use design pattern?
- What are the use cases it can be applied to?
- What are the elements/building blocks needed to implement the design pattern?
- What are the special considerations for using the Tool Use Design Pattern to build trustworthy AI agents?

</v-clicks>

---

# Learning Goals

After completing this lesson, you will be able to:

<v-clicks>

- Define the Tool Use Design Pattern and its purpose.
- Identify use cases where the Tool Use Design Pattern is applicable.
- Understand the key elements needed to implement the design pattern.
- Recognize considerations for ensuring trustworthiness in AI agents using this design pattern.

</v-clicks>

---
layout: default
---

# What is the Tool Use Design Pattern?

The **Tool Use Design Pattern** focuses on giving LLMs the ability to interact with external tools to achieve specific goals.

<v-clicks>

- **Tools** are code that can be executed by an agent to perform actions.
- A tool can be a simple function (e.g., calculator) or an API call to a third-party service (e.g., stock price lookup, weather forecast).
- In AI agents, tools are designed to be executed in response to **model-generated function calls**.

</v-clicks>

---

# Use Cases for Tool Use

AI Agents can leverage tools to complete complex tasks, retrieve information, or make decisions. This pattern is useful for:

<v-clicks>

- **Dynamic Information Retrieval:** Querying external APIs/databases for up-to-date data (e.g., SQLite, stock prices, weather).
- **Code Execution and Interpretation:** Executing code/scripts for math problems, reports, or simulations.
- **Workflow Automation:** Automating multi-step workflows (e.g., task schedulers, email services, data pipelines).
- **Customer Support:** Interacting with CRM systems, ticketing platforms, or knowledge bases.
- **Content Generation and Editing:** Using tools like grammar checkers, summarizers, or content safety evaluators.

</v-clicks>

---

# Building Blocks for Tool Use

Key elements needed to implement the Tool Use Design Pattern:

Next, let's look at Function/Tool Calling in more detail.

<v-clicks>

- **Function/Tool Calling**: Primary way for LLMs to interact with tools. Functions (reusable code blocks) are the tools.
- **Dynamic Information Retrieval**: Querying external sources for current data.
- **Code Execution and Interpretation**: Running code/scripts.
- **Workflow Automation**: Integrating tools for multi-step processes.
- **Customer Support**: Interacting with support systems.
- **Content Generation and Editing**: Leveraging content-focused tools.

</v-clicks>

---
layout: two-cols-header
---

# Function/Tool Calling Explained

Function calling enables LLMs to interact with tools. 'Function' and 'Tool' are often used interchangeably.

::left::

**Process:**
1. An LLM compares the user's request against a schema of available functions/tools.
2. The LLM selects the most appropriate function and returns its name and arguments.
3. The selected function's code is invoked.
4. The function's response is sent back to the LLM.
5. The LLM uses this information to respond to the user's original request.

::right::

**Requirements for Developers:**
1. An LLM model that supports function calling.
2. A schema containing function descriptions.
3. The code for each described function.

---
layout: default
---

# Function Calling Example: Get Current Time

**1. Initialize an LLM that supports function calling:**
   - Check if your LLM supports this (e.g., <a href="https://learn.microsoft.com/azure/ai-services/openai/how-to/function-calling" target="_blank">Azure OpenAI</a>).

```python
# Initialize the Azure OpenAI client
# Refer to original README for full code
import os
from openai import AzureOpenAI

client = AzureOpenAI(
    azure_endpoint = os.getenv("AZURE_OPENAI_ENDPOINT"), 
    api_key=os.getenv("AZURE_OPENAI_API_KEY"),  
    api_version="2024-05-01-preview"
)
# deployment_name = "YOUR_DEPLOYMENT_NAME" # Set your deployment name
```

---

# Function Calling Example: Get Current Time

**2. Create a Function Schema:**
   - Define a JSON schema with function name, description, and parameters.
   - Pass this schema and user request to the LLM.
   - The LLM returns a **tool call**, not the final answer.

```python
# Function description for the model to read
# Refer to original README for full code
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_current_time",
            "description": "Get the current time in a given location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                        "description": "The city name, e.g. San Francisco",
                    },
                },
                "required": ["location"],
            },
        }
    }
]
```

---

# Function Calling Example: Get Current Time

```python
messages = [{"role": "user", "content": "What's the current time in San Francisco"}]

response = client.chat.completions.create(
    model=deployment_name,
    messages=messages,
    tools=tools,
    tool_choice="auto",
)
response_message = response.choices[0].message
print(f"Model's response: {response_message}")
```

---

# Trustworthy AI: Special Considerations for Tool Use

<v-clicks>

- **SQL Injection Risk with LLM-generated SQL:**
  - A common concern for dynamically generated SQL.
  - **Mitigation:** Properly configure database access permissions.
    - Set database to read-only for the agent.
    - Assign a read-only (SELECT) role (e.g., PostgreSQL, Azure SQL).

- **Secure Environment:**
  - Run the application in a secure environment.
  - **Enterprise Best Practice:** Extract, Transform, Load (ETL) data from operational systems into a read-only data warehouse or database with a user-friendly schema.
  - This ensures data is secure, optimized, and the app has restricted, read-only access.

</v-clicks>

---
layout: default
---

# Additional Resources

- <a href="https://microsoft.github.io/build-your-first-agent-with-azure-ai-agent-service-workshop/" target="_blank">Azure AI Agents Service Workshop</a>
- <a href="https://github.com/Azure-Samples/contoso-creative-writer/tree/main/docs/workshop" target="_blank">Contoso Creative Writer Multi-Agent Workshop</a>
- <a href="https://learn.microsoft.com/semantic-kernel/concepts/ai-services/chat-completion/function-calling/?pivots=programming-language-python#1-serializing-the-functions" target="_blank">Semantic Kernel Function Calling Tutorial</a>
- <a href="https://github.com/microsoft/semantic-kernel/blob/main/python/samples/getting_started_with_agents/openai_assistant/step3_assistant_tool_code_interpreter.py" target="_blank">Semantic Kernel Code Interpreter</a>
- <a href="https://microsoft.github.io/autogen/dev/user-guide/core-user-guide/components/tools.html" target="_blank">Autogen Tools</a>

---
layout: end
---

# End of Lesson 4

Review and Next Steps

---
layout: end
---

# Navigation

## Previous Lesson
[Understanding Agentic Design Patterns](../03-agentic-design-patterns/README.md)

## Next Lesson
[Agentic RAG](../05-agentic-rag/README.md)

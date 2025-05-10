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
---
<!--
Original filepath: /workspaces/ai-agents-for-beginners-csharp/04-tool-use/README.md
Slidev conversion starts here.
-->

---
layout: cover
background: ./images/lesson-4-thumbnail.png
class: text-center
---

# Tool Use Design Pattern
## AI Agents for Beginners - Lesson 4

<div class="abs-br m-6 flex gap-2">
  <a href="https://youtu.be/vieRiPRx-gI?si=cEZ8ApnT6Sus9rhn" target="_blank" alt="View video of this lesson"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-video />
  </a>
</div>

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

<v-clicks>

- **Function/Tool Calling**: Primary way for LLMs to interact with tools. Functions (reusable code blocks) are the tools.
- **Dynamic Information Retrieval**: Querying external sources for current data.
- **Code Execution and Interpretation**: Running code/scripts.
- **Workflow Automation**: Integrating tools for multi-step processes.
- **Customer Support**: Interacting with support systems.
- **Content Generation and Editing**: Leveraging content-focused tools.

</v-clicks>

Next, let's look at Function/Tool Calling in more detail.

---
layout: default
---

# Function/Tool Calling Explained

Function calling enables LLMs to interact with tools. 'Function' and 'Tool' are often used interchangeably.

**Process:**
1. An LLM compares the user's request against a schema of available functions/tools.
2. The LLM selects the most appropriate function and returns its name and arguments.
3. The selected function's code is invoked.
4. The function's response is sent back to the LLM.
5. The LLM uses this information to respond to the user's original request.

**Requirements for Developers:**
<v-clicks>

1. An LLM model that supports function calling.
2. A schema containing function descriptions.
3. The code for each described function.

</v-clicks>

---
layout: two-cols
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

::right::

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

messages = [{"role": "user", "content": "What's the current time in San Francisco"}]

# response = client.chat.completions.create(
#     model=deployment_name,
#     messages=messages,
#     tools=tools,
#     tool_choice="auto",
# )
# response_message = response.choices[0].message
# print(f"Model's response: {response_message}")
```

**Example Model Response (Tool Call):**
```text
ChatCompletionMessage(content=None, role='assistant', tool_calls=[ChatCompletionMessageToolCall(id='call_abc123', function=Function(arguments='{"location":"San Francisco"}', name='get_current_time'), type='function')])
```

---
layout: two-cols
---

# Function Calling Example (Continued)

**3. Implement and Execute Function Code:**
   - Write the Python code for `get_current_time`.
   - Extract name and arguments from the LLM's `response_message`.
   - Execute the function.
   - Send the function's result back to the LLM for the final answer.

```python
# Refer to original README for full code
import json
from datetime import datetime
from zoneinfo import ZoneInfo

# Simplified TIMEZONE_DATA for example
TIMEZONE_DATA = {
    "san francisco": "America/Los_Angeles",
    "new york": "America/New_York",
    "london": "Europe/London"
}

def get_current_time(location):
    # ... (full function code from README) ...
    print(f"get_current_time called with location: {location}")  
    location_lower = location.lower()
    
    for key, timezone in TIMEZONE_DATA.items():
        if key in location_lower:
            print(f"Timezone found for {key}")  
            current_time = datetime.now(ZoneInfo(timezone)).strftime("%I:%M %p")
            return json.dumps({
                "location": location,
                "current_time": current_time
            })
  
    print(f"No timezone data found for {location_lower}")  
    return json.dumps({"location": location, "current_time": "unknown"})

# messages.append(response_message) # Add model's first response

# if response_message.tool_calls:
#     for tool_call in response_message.tool_calls:
#         if tool_call.function.name == "get_current_time":
#             function_args = json.loads(tool_call.function.arguments)
#             time_response = get_current_time(
#                 location=function_args.get("location")
#             )
#             messages.append({
#                 "tool_call_id": tool_call.id,
#                 "role": "tool",
#                 "name": "get_current_time",
#                 "content": time_response,
#             })

# final_response = client.chat.completions.create(
#     model=deployment_name,
#     messages=messages,
# )
# print(final_response.choices[0].message.content)
```

::right::

**Example Execution Output & Final LLM Response:**

```bash
get_current_time called with location: San Francisco
Timezone found for san francisco
```

LLM Final Response:
```text
The current time in San Francisco is 09:24 AM.
```

Function Calling is central to agent tool use. Agentic frameworks simplify this.

---
layout: image-right
image: ./images/functioncalling-diagram.png
---

# Tool Use with Semantic Kernel

<a href="https://learn.microsoft.com/azure/ai-services/agents/overview" target="_blank">Semantic Kernel</a> (SK) simplifies function calling:
- Automatically describes functions/parameters to the model (serializing).
- Handles model-code communication.
- Provides pre-built tools like <a href="https://github.com/microsoft/semantic-kernel/blob/main/python/samples/getting_started_with_agents/openai_assistant/step4_assistant_tool_file_search.py" target="_blank">File Search</a> and <a href="https://github.com/microsoft/semantic-kernel/blob/main/python/samples/getting_started_with_agents/openai_assistant/step3_assistant_tool_code_interpreter.py" target="_blank">Code Interpreter</a>.

In SK, functions/tools are called <a href="https://learn.microsoft.com/semantic-kernel/concepts/plugins/?pivots=programming-language-python" target="_blank">Plugins</a>.

**Example: `get_current_time` as an SK Plugin:**

```python
# Refer to original README for full code
from semantic_kernel.functions import kernel_function

class GetCurrentTimePlugin:
    # Removed __init__ for simplicity in this example slide
    # async def __init__(self, location):
    #     self.location = location

    @kernel_function(
        description="Get the current time for a given location",
        name="get_current_time_sk_plugin" # Explicit name for clarity
    )
    def get_current_time(self, location: str = ""):
        # ... (function body from previous example) ...
        # Simplified for slide, assume TIMEZONE_DATA is available
        location_lower = location.lower()
        for key, timezone in TIMEZONE_DATA.items():
            if key in location_lower:
                current_time = datetime.now(ZoneInfo(timezone)).strftime("%I:%M %p")
                return json.dumps({"location": location, "current_time": current_time})
        return json.dumps({"location": location, "current_time": "unknown"})

# from semantic_kernel import Kernel
# kernel = Kernel()
# get_current_time_plugin_instance = GetCurrentTimePlugin()
# kernel.add_plugin(get_current_time_plugin_instance, plugin_name="TimePlugin")
# # Now kernel can use this plugin
```
The kernel automatically serializes the function and parameters.

---
layout: image-right
image: ./images/agent-service-in-action.jpg
---

# Tool Use with Azure AI Agent Service

<a href="https://learn.microsoft.com/azure/ai-services/agents/overview" target="_blank">Azure AI Agent Service</a> is a managed service for enterprise-grade AI agents.

**Advantages:**
- Automatic tool calling (server-side).
- Securely managed data (threads for conversation state).
- Out-of-the-box tools (Bing, Azure AI Search, Azure Functions).

**Tool Categories:**
1.  **Knowledge Tools**: Grounding with Bing Search, File Search, Azure AI Search.
2.  **Action Tools**: Function Calling, Code Interpreter, OpenAPI defined tools, Azure Functions.

The service uses `toolset` (multiple tools) and `threads` (conversation history).

**Example: Sales Agent with Azure AI Agent Service**
This diagram shows analyzing sales data.

---
layout: default
---

# Azure AI Agent Service: Code Example

Using a custom function (`fetch_sales_data_using_sqlite_query`) and Code Interpreter.

```python
# Refer to original README for full code
import os
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential
# Assuming fetch_sales_data_using_sqlite_query is in fecth_sales_data_functions.py
# from fecth_sales_data_functions import fetch_sales_data_using_sqlite_query 
from azure.ai.projects.models import ToolSet, FunctionTool, CodeInterpreterTool

# Placeholder for the actual function for slide purposes
# In a real scenario, this would be properly defined and imported.
def fetch_sales_data_using_sqlite_query(query: str):
    """Fetches sales data using a SQLite query."""
    # Actual implementation would connect to a DB and run the query.
    return f"Data for query: {query}"

# project_client = AIProjectClient.from_connection_string(
#     credential=DefaultAzureCredential(),
#     conn_str=os.environ["PROJECT_CONNECTION_STRING"],
# )

# fetch_data_function = FunctionTool(fetch_sales_data_using_sqlite_query)
# code_interpreter = CodeInterpreterTool()

# toolset = ToolSet()
# toolset.add(fetch_data_function)
# toolset.add(code_interpreter)

# agent = project_client.agents.create_agent(
#     model="gpt-4o-mini", 
#     name="my-sales-agent", # Renamed for clarity
#     instructions="You are a helpful sales data analysis agent", 
#     toolset=toolset
# )
# print(f"Agent '{agent.name}' created with ID '{agent.id}'")
```
The LLM can choose between the custom function or Code Interpreter based on the user's request.

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

<v-clicks>

- <a href="https://microsoft.github.io/build-your-first-agent-with-azure-ai-agent-service-workshop/" target="_blank">Azure AI Agents Service Workshop</a>
- <a href="https://github.com/Azure-Samples/contoso-creative-writer/tree/main/docs/workshop" target="_blank">Contoso Creative Writer Multi-Agent Workshop</a>
- <a href="https://learn.microsoft.com/semantic-kernel/concepts/ai-services/chat-completion/function-calling/?pivots=programming-language-python#1-serializing-the-functions" target="_blank">Semantic Kernel Function Calling Tutorial</a>
- <a href="https://github.com/microsoft/semantic-kernel/blob/main/python/samples/getting_started_with_agents/openai_assistant/step3_assistant_tool_code_interpreter.py" target="_blank">Semantic Kernel Code Interpreter</a>
- <a href="https://microsoft.github.io/autogen/dev/user-guide/core-user-guide/components/tools.html" target="_blank">Autogen Tools</a>

</v-clicks>

---
layout: section
---

# End of Lesson 4

Review and Next Steps

---
layout: default
---

# Navigation

## Previous Lesson
[Understanding Agentic Design Patterns](../03-agentic-design-patterns/README.md)

## Next Lesson
[Agentic RAG](../05-agentic-rag/README.md)

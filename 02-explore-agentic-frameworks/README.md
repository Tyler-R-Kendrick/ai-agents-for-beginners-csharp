---
title: 'Explore AI Agent Frameworks'
subtitle: 'Lesson 2: AI Agents for Beginners'
theme: seriph
transition: slide-left
class: text-center
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
download: true
exportFilename: '02-explore-agentic-frameworks-slides'
layout: cover
background: ./images/lesson-2-thumbnail.png
---

# Explore AI Agent Frameworks
  This lesson explores different AI Agent Frameworks like AutoGen, Semantic Kernel, and Azure AI Agent Service.

---
layout: intro
---

# Explore AI Agent Frameworks
## AI Agents for Beginners - Lesson 2


---

<Youtube id="ODwF-EZo_O8" class="absolute inset-0 w-full h-full" />

> _(Click the video icon above to view video of this lesson)_

---

# Explore AI Agent Frameworks

AI agent frameworks are software platforms designed to simplify the creation, deployment, and management of AI agents. These frameworks provide developers with pre-built components, abstractions, and tools that streamline the development of complex AI systems.

These frameworks help developers focus on the unique aspects of their applications by providing standardized approaches to common challenges in AI agent development. They enhance scalability, accessibility, and efficiency in building AI systems.

---
layout: default
---

# Lesson Overview

This lesson will cover:

<v-clicks>

- What are AI Agent Frameworks and what do they enable developers to achieve?
- How can teams use these to quickly prototype, iterate, and improve their agent’s capabilities?
- What are the differences between the frameworks and tools created by Microsoft <a href="https://aka.ms/ai-agents/autogen" target="_blank">AutoGen</a>, <a href="https://aka.ms/ai-agents-beginners/semantic-kernel" target="_blank">Semantic Kernel</a>, and <a href="https://aka.ms/ai-agents-beginners/ai-agent-service" target="_blank">Azure AI Agent Service</a>?
- Can I integrate my existing Azure ecosystem tools directly, or do I need standalone solutions?
- What is Azure AI Agents service and how is this helping me?

</v-clicks>

---

# Learning Goals

The goals of this lesson are to help you understand:

<v-clicks>

- The role of AI Agent Frameworks in AI development.
- How to leverage AI Agent Frameworks to build intelligent agents.
- Key capabilities enabled by AI Agent Frameworks.
- The differences between AutoGen, Semantic Kernel, and Azure AI Agent Service.

</v-clicks>

---
layout: two-cols
---

# What are AI Agent Frameworks?
## And what do they enable developers to do?

Traditional AI Frameworks can help you integrate AI into your apps and make these apps better in the following ways:

::right::

<v-clicks>

- **Personalization**: AI can analyze user behavior and preferences to provide personalized recommendations, content, and experiences.
  - _Example: Streaming services like Netflix use AI to suggest movies and shows based on viewing history._
- **Automation and Efficiency**: AI can automate repetitive tasks, streamline workflows, and improve operational efficiency.
  - _Example: Customer service apps use AI-powered chatbots to handle common inquiries._
- **Enhanced User Experience**: AI can improve the overall user experience by providing intelligent features such as voice recognition, natural language processing, and predictive text.
  - _Example: Virtual assistants like Siri and Google Assistant use AI to understand and respond._

</v-clicks>

---

# Why AI Agent Frameworks?

That all sounds great, right? So why do we need AI Agent Frameworks specifically?

<v-clicks>

AI Agent frameworks represent something **more** than just AI frameworks. They are designed to enable the creation of **intelligent agents** that can:
- Interact with users, other agents, and the environment.
- Achieve specific goals.
- Exhibit autonomous behavior.
- Make decisions.
- Adapt to changing conditions.

</v-clicks>

---
layout: two-cols
---

# Key Capabilities of AI Agent Frameworks

**In summary:** Agents allow you to do more, take automation to the next level, and create more intelligent systems that can adapt and learn from their environment.

::right::

<v-clicks>

- **Agent Collaboration and Coordination**: Enable the creation of multiple AI agents that can work together, communicate, and coordinate to solve complex tasks.
- **Task Automation and Management**: Provide mechanisms for automating multi-step workflows, task delegation, and dynamic task management among agents.
- **Contextual Understanding and Adaptation**: Equip agents with the ability to understand context, adapt to changing environments, and make decisions based on real-time information.

</v-clicks>


---

# Rapid Prototyping & Iteration
## How to quickly prototype, iterate, and improve agent capabilities?

This is a fast-moving landscape, but some common aspects across most AI Agent Frameworks help with rapid development:

<v-clicks>

- **Use Modular Components**: AI SDKs offer pre-built components (AI/Memory connectors, function calling, prompt templates).
- **Leverage Collaborative Tools**: Design agents with specific roles and tasks to test and refine collaborative workflows.
- **Learn in Real-Time**: Implement feedback loops where agents learn from interactions and adjust behavior dynamically.

</v-clicks>

---
layout: section
---

# Modular Components

SDKs like Microsoft Semantic Kernel and LangChain offer pre-built components such as AI connectors, prompt templates, and memory management.

**How teams can use these**: Quickly assemble components to create functional prototypes without starting from scratch, allowing for rapid experimentation.

**How it works in practice**: Use a pre-built parser for user input, a memory module for data storage/retrieval, and a prompt generator for user interaction – all without building them from scratch.

Let's look at how to use a pre-built AI Connector with Semantic Kernel (Python and .NET) for auto-function calling.

---
layout: default
---

# Example: Semantic Kernel (python)

```python
# Semantic Kernel Python Example
# ... (Code for Python example)
# Refer to original README for full code
import asyncio
from typing import Annotated

from semantic_kernel.connectors.ai import FunctionChoiceBehavior
from semantic_kernel.connectors.ai.open_ai import AzureChatCompletion, AzureChatPromptExecutionSettings
from semantic_kernel.contents import ChatHistory
from semantic_kernel.functions import kernel_function
from semantic_kernel.kernel import Kernel

chat_history = ChatHistory()
chat_history.add_user_message("I'd like to go to New York on January 1, 2025")

class BookTravelPlugin:
    @kernel_function(name="book_flight", description="Book travel given location and date")
    async def book_flight(
        self, date: Annotated[str, "The date of travel"], location: Annotated[str, "The location to travel to"]
    ) -> str:
        return f"Travel was booked to {location} on {date}"

kernel = Kernel()
kernel.add_plugin(BookTravelPlugin(), plugin_name="book_travel")
chat_service = AzureChatCompletion(
    deployment_name="YOUR_DEPLOYMENT_NAME", 
    api_key="YOUR_API_KEY", 
    endpoint="https://<your-resource>.azure.openai.com/",
)
request_settings = AzureChatPromptExecutionSettings(function_choice_behavior=FunctionChoiceBehavior.Auto())

async def main():
    response = await chat_service.get_chat_message_content(
        chat_history=chat_history, settings=request_settings, kernel=kernel
    )
    assert response is not None
    print(f"`{response}`")
    chat_history.add_assistant_message(response.content)

# if __name__ == "__main__":
#     asyncio.run(main())
```

---

# Example: Semantic Kernel (dotnet)

```csharp
// Semantic Kernel C# example
// ... (Code for C# example)
// Refer to original README for full code
using Microsoft.SemanticKernel;
using Microsoft.SemanticKernel.ChatCompletion;
using System.ComponentModel;
using Microsoft.SemanticKernel.Connectors.AzureOpenAI;

ChatHistory chatHistory = [];
chatHistory.AddUserMessage("I'd like to go to New York on January 1, 2025");

var kernelBuilder = Kernel.CreateBuilder();
kernelBuilder.AddAzureOpenAIChatCompletion(
    deploymentName: "NAME_OF_YOUR_DEPLOYMENT",
    apiKey: "YOUR_API_KEY",
    endpoint: "YOUR_AZURE_ENDPOINT"
);
kernelBuilder.Plugins.AddFromType<BookTravelPlugin>("BookTravel"); 
var kernel = kernelBuilder.Build();

var settings = new AzureOpenAIPromptExecutionSettings()
{
    FunctionChoiceBehavior = FunctionChoiceBehavior.Auto()
};

var chatCompletion = kernel.GetRequiredService<IChatCompletionService>();

// var response = await chatCompletion.GetChatMessageContentAsync(chatHistory, settings, kernel);
// Console.WriteLine(response.Content);
// chatHistory.AddMessage(response!.Role, response!.Content!);

public class BookTravelPlugin
{
    [KernelFunction("book_flight")]
    [Description("Book travel given location and date")]
    public async Task<string> BookFlight(DateTime date, string location)
    {
        return await Task.FromResult( $"Travel was booked to {location} on {date}");
    }
}
```

---

## Explanation

The model determines it can invoke the `BookTravelPlugin` using the `book_flight` function, supplying necessary arguments (location, date).

If arguments are missing, the model prompts the user.

_User_: Book me a flight to New York.
_Model_: Sure, I'd love to help you book a flight. Could you please specify the date?
_User_: I want to travel on January 1, 2025.
_Model_: Your flight to New York on January 1, 2025, has been successfully booked. Safe travels!

This modular approach allows focusing on high-level logic.

---
layout: section
---

# Collaborative Tools

Frameworks like CrewAI, Microsoft AutoGen, and Semantic Kernel facilitate creating multiple agents that work together.

**How teams can use these**: Design agents with specific roles and tasks to test and refine collaborative workflows, improving system efficiency.

**How it works in practice**: Create a team of specialized agents (data retrieval, analysis, decision-making). They communicate and share info to achieve a common goal.

---
layout: default
---

# Example: AutoGen

Creating agents and a round-robin schedule for them to collaborate.

**Explanation:**
This code shows creating a task with multiple agents analyzing data. Each agent has a specific function, and the task is executed by coordinating them. Dedicated agents with specialized roles improve task efficiency.

```python
# creating agents, then create a round robin schedule
# ... (Code for AutoGen example)
# Refer to original README for full code

# Data Retrieval Agent
# Data Analysis Agent
# Decision Making Agent

# agent_retrieve = AssistantAgent(
#     name="dataretrieval",
#     model_client=model_client,
#     tools=[retrieve_tool],
#     system_message="Use tools to solve tasks."
# )

# agent_analyze = AssistantAgent(
#     name="dataanalysis",
#     model_client=model_client,
#     tools=[analyze_tool],
#     system_message="Use tools to solve tasks."
# )

# termination = TextMentionTermination("APPROVE")
# user_proxy = UserProxyAgent("user_proxy", input_func=input)
# team = RoundRobinGroupChat([agent_retrieve, agent_analyze, user_proxy], termination_condition=termination)
# stream = team.run_stream(task="Analyze data", max_turns=10)
# await Console(stream)
```

---

# Learn in Real-Time

Advanced frameworks provide capabilities for real-time context understanding and adaptation.

This iterative learning process enables agents to adapt to changing conditions and user preferences, enhancing system effectiveness.

**How teams can use these**: Implement feedback loops where agents learn from interactions and adjust their behavior dynamically, leading to continuous improvement.

**How it works in practice**: Agents analyze user feedback, environmental data, and task outcomes to:
<v-clicks>

- Update their knowledge base.
- Adjust decision-making algorithms.
- Improve performance over time.

</v-clicks>

---
layout: default
---

# Framework Differences
## AutoGen vs. Semantic Kernel vs. Azure AI Agent Service

There are many ways to compare these frameworks. Let's look at key differences in design, capabilities, and target use cases.

---

# AutoGen

An open-source framework by Microsoft Research's AI Frontiers Lab.

**Focus**: Event-driven, distributed *agentic* applications.

**Enables**: Multiple LLMs and SLMs, tools, and advanced multi-agent design patterns.

Built around **agents**: autonomous entities that perceive, decide, and act. They communicate via asynchronous messages (based on the <a href="https://en.wikipedia.org/wiki/Actor_model" target="_blank">actor model</a>).

**Use Cases**: Automating code generation, data analysis, custom agents for planning/research.

---
layout: default
---

## AutoGen: Core Concepts

<v-clicks>

- **Agents**: Software entities that:
  - Communicate via messages (sync/async).
  - Maintain their own state.
  - Perform actions (modify state, send messages, execute code, API calls).

- **Multi-agents**: Supports multiple agents working together, sharing info, and coordinating actions.

- **Agent Runtime**: Environment for agent communication, identity/lifecycle management, security/privacy.
  - **Stand-alone runtime**: Single-process applications.
  - **Distributed agent runtime**: Multi-process, multi-language, multi-machine applications.

</v-clicks>

---
layout: default
---

# AutoGen: Agent Example
## Creating a custom agent with chat capabilities

```python
# Refer to original README for full code
from autogen_agentchat.agents import AssistantAgent
# from autogen_agentchat.messages import TextMessage
# from autogen_ext.models.openai import OpenAIChatCompletionClient

# class MyAssistant(RoutedAgent):
#     def __init__(self, name: str) -> None:
#         super().__init__(name)
#         model_client = OpenAIChatCompletionClient(model="gpt-4o")
#         self._delegate = AssistantAgent(name, model_client=model_client)

#     @message_handler
#     async def handle_my_message_type(self, message: MyMessageType, ctx: MessageContext) -> None:
#         print(f"{self.id.type} received message: {message.content}")
#         response = await self._delegate.on_messages(
#             [TextMessage(content=message.content, source="user")], ctx.cancellation_token
#         )
#         print(f"{self.id.type} responded: {response.chat_message.content}")

# # main.py
# runtime = SingleThreadedAgentRuntime()
# await MyAgent.register(runtime, "my_agent", lambda: MyAgent())
# runtime.start()
# await runtime.send_message(MyMessageType("Hello, World!"), AgentId("my_agent", "default"))
```

---

## Explanation

`MyAssistant` inherits from `RoutedAgent`. Its message handler prints received message content and responds using an `AssistantAgent` delegate.

The agent is registered with the runtime, and a message is sent to it.

**Output:**
```text
my_agent received message: Hello, World!
my_assistant received message: Hello, World!
my_assistant responded: Hello! How can I assist you today?
```

---

# AutoGen: Multi-Agent Example
## Creating a group chat manager for different agent types

```python
# Refer to original README for full code
# editor_description = "Editor for planning and reviewing the content."
# editor_agent_type = await EditorAgent.register(
#     runtime,
#     editor_topic_type, 
#     lambda: EditorAgent(
#         description=editor_description,
#         group_chat_topic_type=group_chat_topic_type,
#         model_client=OpenAIChatCompletionClient(model="gpt-4o-2024-08-06"),
#     ),
# )

# group_chat_manager_type = await GroupChatManager.register(
#     runtime,
#     "group_chat_manager",
#     lambda: GroupChatManager(
#         participant_topic_types=[writer_topic_type, illustrator_topic_type, editor_topic_type, user_topic_type],
#         model_client=OpenAIChatCompletionClient(model="gpt-4o-2024-08-06"),
#         participant_descriptions=[
#             writer_description, illustrator_description, 
#             editor_description, user_description
#         ],
#     ),
# )
```

---

## Explanation

A `GroupChatManager` is registered with the runtime. It coordinates interactions between different agent types (writers, illustrators, editors, users).

**Agent Runtimes:**
- **Stand-alone:** <a href="https://microsoft.github.io/autogen/stable/_images/architecture-standalone.svg" target="_blank">Diagram</a>
  - Agents communicate via messages through the runtime.
  - Runtime manages agent lifecycles.
- **Distributed:** <a href="https://microsoft.github.io/autogen/stable/_images/architecture-distributed.svg" target="_blank">Diagram</a>
  - Suitable for multi-process, potentially multi-language/machine setups.

---

# Semantic Kernel + Agent Framework

Semantic Kernel is an enterprise-ready AI Orchestration SDK. It includes AI and memory connectors, plus an Agent Framework.

## Core Components:
### AI Connectors: Interface with external AI services and data sources (Python & C#).

---

## Semantic Kernel Examples

### python

```python
# Semantic Kernel Python
from semantic_kernel.connectors.ai.open_ai import AzureChatCompletion
from semantic_kernel.kernel import Kernel

kernel = Kernel()
kernel.add_service(
  AzureChatCompletion(
      deployment_name="your-deployment-name",
      api_key="your-api-key",
      endpoint="your-endpoint",
  )
)
```

### csharp

```csharp
// Semantic Kernel C#
using Microsoft.SemanticKernel;
var builder = Kernel.CreateBuilder();
builder.Services.AddAzureOpenAIChatCompletion(
    "your-resource-name", "your-endpoint", 
    "your-resource-key", "deployment-model");
var kernel = builder.Build();
```

---

# Semantic Kernel: Plugins

Encapsulate functions for an application. Can be ready-made or custom.

**Prompt Functions**: Instead of natural language cues, broadcast functions to the model. The model chooses to call one based on chat context.

**Explanation:**
A template prompt (`skPrompt`) takes user input (`$userInput`). A kernel function (`SummarizeText`) is created and imported into the kernel with a plugin name (`SemanticFunctions`). The function name helps Semantic Kernel understand when to call it.

<v-switch>

<template #1>

## python

```python
# Refer to original README for full code
from semantic_kernel.functions import KernelFunctionFromPrompt
from semantic_kernel.kernel import Kernel
kernel = Kernel()
kernel.add_service(AzureChatCompletion())
user_input = input("User Input:> ")
kernel_function = KernelFunctionFromPrompt(
    function_name="SummarizeText",
    prompt='''
    Summarize the provided unstructured text...
    Text to summarize: {{$user_input}}
    ''',
)
response = await kernel_function.invoke(kernel=kernel, user_input=user_input)
print(f"Model Response: {response}")
```

</template>

<template #2>

## csharp

```csharp
// Refer to original README for full code
var userInput = Console.ReadLine();
string skPrompt = @"Summarize the provided unstructured text...
                    Text to summarize: {{$userInput}}";
KernelFunction summarizeFunc = kernel.CreateFunctionFromPrompt(
    promptTemplate: skPrompt,
    functionName: "SummarizeText"
);
kernel.ImportPluginFromFunctions("SemanticFunctions", [summarizeFunc]);
```

</template>
</v-switch>

---

# Semantic Kernel: Native Functions

Functions the framework can call directly.
Example: Retrieving file content.

```csharp
// Refer to original README for full code
public class NativeFunctions {
    [SKFunction, Description("Retrieve content from local file")]
    public async Task<string> RetrieveLocalFile(string fileName, int maxSize = 5000)
    {
        string content = await File.ReadAllTextAsync(fileName);
        if (content.Length <= maxSize) return content;
        return content.Substring(0, maxSize);
    }
}
kernel.ImportPluginFromType<NativeFunctions>();
```

---

# Semantic Kernel: Memory

Abstracts and simplifies context management.
Information the LLM should know, often stored in a vector store (in-memory DB, vector DB, etc.).

Example: Adding facts to memory.
```csharp
// Refer to original README for full code
var facts = new Dictionary<string,string>();
facts.Add(
    "Azure Machine Learning; ...",
    @"Azure Machine Learning is a cloud service..."
);
facts.Add(
    "Azure SQL Service; ...",
    @"Azure SQL is a family of managed, secure..."
);
string memoryCollectionName = "SummarizedAzureDocs";
foreach (var fact in facts) {
    await memoryBuilder.SaveReferenceAsync(
        collection: memoryCollectionName,
        description: fact.Key.Split(';')[1].Trim(),
        text: fact.Value,
        externalId: fact.Key.Split(';')[2].Trim(),
        externalSourceName: "Azure Documentation"
    );
}
```
Facts are stored in `SummarizedAzureDocs` for LLM use.

---

# Azure AI Agent Service

A recent addition (Microsoft Ignite 2024).

<v-clicks>

- Allows development and deployment of AI agents with **flexible models** (Llama 3, Mistral, Cohere).
- Provides **stronger enterprise security** mechanisms and data storage methods.
- Suitable for **enterprise applications**.
- Works **out-of-the-box** with multi-agent orchestration frameworks like AutoGen and Semantic Kernel.
- Currently in **Public Preview** (supports Python and C#).

</v-clicks>

---

# Azure AI Agent Service: Example

Creating an Azure AI Agent with a user-defined plugin (Semantic Kernel Python):

```python
# Refer to original README for full code
import asyncio
from typing import Annotated
from azure.identity.aio import DefaultAzureCredential
from semantic_kernel.agents import AzureAIAgent, AzureAIAgentSettings, AzureAIAgentThread
from semantic_kernel.contents import ChatMessageContent, AuthorRole
from semantic_kernel.functions import kernel_function

class MenuPlugin:
    @kernel_function(description="Provides a list of specials...")
    def get_specials(self) -> Annotated[str, "Returns the specials..."]:
        return "Special Soup: ..."
    @kernel_function(description="Provides the price...")
    def get_item_price(self, menu_item: Annotated[str, "The name..."])
      -> Annotated[str, "Returns the price..."]:
        return "$9.99"

async def main() -> None:
    ai_agent_settings = AzureAIAgentSettings.create()
    async with (
        DefaultAzureCredential() as creds,
        AzureAIAgent.create_client(...) as client,
    ):
        agent_definition = await client.agents.create_agent(...)
        agent = AzureAIAgent(client=client, plugins=[MenuPlugin()])
        thread: AzureAIAgentThread | None = None
        user_inputs = ["Hello", "Thank you"]
        try:
            for user_input in user_inputs:
                # ... message processing ...
                pass # Placeholder for actual message handling logic
        finally:
            await thread.delete() if thread else None
            await client.agents.delete_agent(agent.id)

if __name__ == "__main__":
    asyncio.run(main())
```

---

## Azure AI Agent Service: Core Concepts

<v-clicks>

- **Agent**: Integrates with Azure AI Foundry. Acts as a "smart" microservice for RAG, actions, or workflow automation. Combines generative AI with tools for real-world data interaction.
  ```python
  agent = project_client.agents.create_agent(
      model="gpt-4o-mini",
      tool_resources=code_interpreter.resources,
  )
  ```

- **Thread and Messages**: A thread represents a conversation. Tracks progress, stores context, manages interaction state.
  ```python
  thread = project_client.agents.create_thread()
  message = project_client.agents.create_message(
  ...
  )
  ```
  Messages (text, image, file) indicate conversation progress. Developers use this for further processing or presentation.

</v-clicks>

---
layout: end
---

# End of Lesson 2

Review and Next Steps

---
layout: end
---

# Navigation

## Previous Lesson
[Introduction to AI Agents and Agent Use Cases](../01-intro-to-ai-agents/README.md)

## Next Lesson
[Agentic Design Patterns](../03-agentic-design-patterns/README.md)

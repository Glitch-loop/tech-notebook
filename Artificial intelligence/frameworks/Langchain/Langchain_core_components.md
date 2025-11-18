# Langchain's Core component 

# Agents
**create_agent** provides a **production-ready** agent implementation.

An LLM agent runs tools in a loop to achieve a goal. This runs until:
1. A condition is met.
2. The model emits a final output or an interation is reached.

![Alt text](https://github.com/Glitch-loop/tech-notebook/blob/main/Artificial%20intelligence/frameworks/Langchain/images/langchain_agent.png?raw=true "a")


> Note: In Langchain, agents follow ReAct ("Reasoning + Acting") pattern.


## Core concepts

### Summary
- Model
  - Static selection
  - Dynamic selection
- Tools
  - Error handling
- Prompts

### Model
This is the reasoning engine of your agent.

[Supported models in langchain](https://reference.langchain.com/python/langchain/models/?_gl=1*1bgwra9*_gcl_au*NTM4MjQxMjY0LjE3NTk3MTM3MzU.*_ga*Mjg0NDk3MDMxLjE3NTk3MTM3Mzc.*_ga_47WX3HKKY2*czE3NjM0MzQ2NjkkbzQkZzEkdDE3NjM0MzUwNDQkajYwJGwwJGgw#langchain.chat_models.init_chat_model) 

Langchain support two types:
- **Static selection:** These are creating and remain unchaged throughout execution.
  
- **Dynamic execution:** These type of selection, selects the model at _runtime_ based on the _current state_ and context. This is modality enables sophisticated routing logic and cost optimization.

    To use dynamic model, create middleware using the ``@wrap_model_call`` decoratir.
    

Example of **static selection:**

```Python
from langchain.agents import create_agent

agent = create_agent(
    "gpt-5",
    tools=tools
)
```

Also you can instanciate a model directly using the provider package.
```Python
from langchain.agents import create_agent
from langchain_openai import ChatOpenAI

model = ChatOpenAI(
    model="gpt-5",
    temperature=0.1,
    max_tokens=1000,
    timeout=30
    # ... (other params)
)
agent = create_agent(model, tools=tools)
```

Example of **dynamic selection:**
```Python
from langchain_openai import ChatOpenAI
from langchain.agents import create_agent
from langchain.agents.middleware import wrap_model_call, ModelRequest, ModelResponse


basic_model = ChatOpenAI(model="gpt-4o-mini")
advanced_model = ChatOpenAI(model="gpt-4o")

@wrap_model_call
def dynamic_model_selection(request: ModelRequest, handler) -> ModelResponse:
    """Choose model based on conversation complexity."""
    message_count = len(request.state["messages"])

    if message_count > 10:
        # Use an advanced model for longer conversations
        model = advanced_model
    else:
        model = basic_model

    request.model = model
    return handler(request)

agent = create_agent(
    model=basic_model,  # Default model
    tools=tools,
    middleware=[dynamic_model_selection]
)
```


### Tool
Tools give the agents the ability to take actions.

Tools extend the capability of the model, making possible to:

- Multiple tools calls in sequence (triggered by a single prompt).

- Parallel tool calls when appropriate.

- Dynamic tool selection based on previous results.

- Tool retry logic and error handling.

- State persistence across tools calls.

#### Defining tools
In langchain, you can use ``@tool`` decorator to define a tool. This decorator allows you to customize:

- Tools Names
- Descriptions
- Argument
- Schemas
- Others...

```Python
from langchain.tools import tool
from langchain.agents import create_agent


@tool
def search(query: str) -> str:
    """Search for information."""
    return f"Results for: {query}"

@tool
def get_weather(location: str) -> str:
    """Get weather information for a location."""
    return f"Weather in {location}: Sunny, 72°F"

agent = create_agent(model, tools=[search, get_weather])
```

#### Tool error handling.
As you may guess, a tool calling can go wrong, for these cases you can use an error handling.

You can use the decorator ``@wrap_tool_call``. This decorator will create a **middleware** that will handle the error from your tools.

```Python
from langchain.agents import create_agent
from langchain.agents.middleware import wrap_tool_call
from langchain.messages import ToolMessage


@wrap_tool_call
def handle_tool_errors(request, handler):
    """Handle tool execution errors with custom messages."""
    try:
        return handler(request)
    except Exception as e:
        # Return a custom error message to the model
        return ToolMessage(
            content=f"Tool error: Please check your input and try again. ({str(e)})",
            tool_call_id=request.tool_call["id"]
        )

agent = create_agent(
    model="gpt-4o",
    tools=[search, get_weather],
    middleware=[handle_tool_errors]
)
```

If error, the agent will return a ``ToolMessage`` with the custom error message:
```Python
[
    ...
    ToolMessage(
        content="Tool error: Please check your input and try again. (division by zero)",
        tool_call_id="..."
    ),
    ...
]
```

### Prompts

You can provide **system prompts** for shaping the behaviour of your agent.
This can be set as string parameter.

```Python
agent = create_agent(
    model,
    tools,
    system_prompt="You are a helpful assistant. Be concise and accurate."
)
```

If no **system prompt** is provided, _the agent will infer its task from the messages directly_.

In addition, you can set **prompts dynamically**, based on runtime context or agent state.

To make prompt dynamic use the ``@dynamic_prompt`` decorator. This creates a middleware that generates system prompts dynamically based on the model request. 

```Python
from typing import TypedDict

from langchain.agents import create_agent
from langchain.agents.middleware import dynamic_prompt, ModelRequest


class Context(TypedDict):
    user_role: str

@dynamic_prompt
def user_role_prompt(request: ModelRequest) -> str:
    """Generate system prompt based on user role."""
    user_role = request.runtime.context.get("user_role", "user")
    base_prompt = "You are a helpful assistant."

    if user_role == "expert":
        return f"{base_prompt} Provide detailed technical responses."
    elif user_role == "beginner":
        return f"{base_prompt} Explain concepts simply and avoid jargon."

    return base_prompt

agent = create_agent(
    model="gpt-4o",
    tools=[web_search],
    middleware=[user_role_prompt],
    context_schema=Context
)

# The system prompt will be set dynamically based on context
result = agent.invoke(
    {"messages": [{"role": "user", "content": "Explain machine learning"}]},
    context={"user_role": "expert"}
)
```

## Invocation
In Langchain for using a model, instead of calling directly for a response, you have to update it's **state**. 

> All agents include a sequence of mesages in their state.

```Python
result = agent.invoke(
    {"messages": [{"role": "user", "content": "What's the weather in San Francisco?"}]}
)
```

## Advanced concepts

### Summary
- Structured output
  - ToolStrategy
  - ProviderStrategy
- Memory
  - Defining state via middleware
  - Defining state via state_schema
- Streaming
- Middleware

### Structure output

Langchain supports structured output, in a nutshell, structure output is when you need
the model answers with some particular format: An specific JSON, in some cases with specific answers.

Langchains offers two ways for achievig this:
1. ``ToolStrategy`` Uses tool for artificially generate structure output _(idoneal if the model doesn't support structure outputs)_.
   

2. ``ProviderStrategy`` Uses the native solution of the model _(you can use this only if the model supports structure output)_. 


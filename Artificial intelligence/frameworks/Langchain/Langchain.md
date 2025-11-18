# What is Langchain?

This is a framework for developing agents workflows in your applications.

Internally it provides an a pre-built agent architecture and model intergrations 
to help to make agnostic your project having the opportunity to change between model
languages (OpenAI, Antropic, Google, etc).

[LangChainDocs](https://docs.langchain.com/oss/python/langchain/install)

## Langchain suit?
Langchain was the core project of langchain foundation. 
Aside **Langchain** we can find another tools from the same team.

[Langchain official website](https://www.langchain.com/)

- LangGrpah (Open source framework):

    - low-level **agent orchestration** framework and runtime
    - Idoneal if you have advanced needs like: 
      - Combination of deterministic and agentic workflow.
      - Heavy customization
      - Carefully control latency.

Note: **LangChain agents** are buil on top of LangGraph (this was made for providing durable execution, streaming, human-in-the-loop, persistence, and more).

- LangSmit (LangGraph):

# How to install LangChain


For installing LangChain
Using pip
```Powershell
# Install in PowerShell (Windows)
pip install -U langchain
```

Using uv
```Powershell
add langchain
```

Note: Requires Python 3.10+

If you want to install an **integration with a particular LLM**, these comes into _**independent provider packages**_:
```Powershell
# Installing the OpenAI integration
pip install -U langchain-openai

# Installing the Anthropic integration
pip install -U langchain-anthropic
```

"<<Insert repo>>"

# Capabilities that offers Langchaing 
- **Understand context** and remember conversations
- **Use multiple tools** intelligently
- **Provide structured** responses in a consistent format
- **Handle user-specific information** through context
- **Maintain conversation state** across interactions

# Langchain Philosphy
1. LLMs are powerful tools for applications.
2. LLMs are better when you combine them with external source of data.
3. LLMs will transform the conception of what we understand as applications: transform them in a more agentic ones.
4. We are early in the implementation of agentic apps.
5. It's easy to make prototypes of agentic apps, but they are not still relaible for production environments.

### The two core focues
1. We want to enabled developers to build with the best models.

This providing the foundations to make you app as agnositc as possible.

2. We want to make it easy to use models to orchestrate more complx flows that interact with other data and computation.

As LLMs become more capables, it is needed workflows that involve multiple agents that needs to communicate one each other (agent orchestration).



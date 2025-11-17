# What is Langchain?

This is a framework for developing agents workflows in your applications.

Internally it provides an a pre-built agent architecture and model intergrations 
to help to make agnostic your project having the opportunity to change between model
languages (OpenAI, Antropic, Google, etc).

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
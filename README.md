---
description: >-
  ReByte is a serial of infrastructure that enables end users to create their
  own AI tools without the need for a data science or engineering background.
---

# 👉 Welcome to ReByte

## End User Programming

> Personal computer should run personal software.

In past decades, the software industry has been dominated by a small group of people who have the ability to write code, a user has to be 'techie' just to open a terminal and start writing code. The recent emergence of LLM in the software industry will bring about a monumental transformation. First LLM provides a vehicle for **every software** to use LLM as human intention understanding. Secondly LLM provides a tool for every **end user** to write small piece of code without learning how to do traditional programming. Soon all normal computer users will have the ability to develop small software tools from scratch by describing what the software looks like and to describe modifications they’d like made to software they’re already using.

This will open the hood of software development to a much larger group of people, every person can use their personal computers to create their **personal** software tools. Every company can use their private data to create their **personal** software tools for internal or external uses.

**ReByte** is built with above mission in mind: to empower end users to create their own tools without the need for a data science or engineering background.

Also, **ReByte** is built to solve following problems in LLM application development:

1. **Iterative Nature of LLM Development**: Create tool on top of modern LLM models can be quite a challenge process, due to the nature of LLM models. LLM outputs are not deterministic, and the model performance can vary from time to time. ReByte's LLM callable builder is built to make this process as painless as possible.
   * Provide a unified interface for end users to test, evaluate and deploy their LLM application.
   * Log every single step of the LLM application, so that end users can easily trace what went wrong.
2. **Painless Private Data integration**: Today's LLM tools heavily rely on private data. Framework such as Langchain and LlamaIndex, together with various vector databases, provide all necessary pieces for private data embedding and search. But as an end user, he still needs to figure out how to wire everything up to make it work, it requires tremendous engineer expertness to do it. We want to make sure that the data integration process is as painless as possible.
   * Provide a hosted solution for end users to import from popular data sources, such as Notion, Google, GitHub, etc., as well as from user's local computer.
   * Handle data source synchronization automatically, so that end users don't need to worry about data consistency.
3. **Production Serving Ready**: Provide a robust runtime ready for immediate deployment and scalable growth.
   * LLM application could be hard to scale, due to its unpredictable and asynchronous nature.
   * By borrowing the idea of serverless function, we provide a scalable runtime for end users to scale their LLM application without worrying about the underlying infrastructure.

## Get Started

[rebyte-concepts.md](overview/understanding-rebyte-architecture.md)

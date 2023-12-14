---
description: >-
  ReByte is a series of infrastructure that enables users to create their
  own AI tools without the need for a data science or engineering background.
---

# 👉 Welcome to ReByte

<figure><img src=".gitbook/assets/shapes at 23-12-14 10.46.28.png" alt=""><figcaption></figcaption></figure>

In the past, the software industry was dominated by a small group of coders; users had to be 'techie' just to open a terminal and start writing code. Recently, large language models like ChatGPT and GPT-4 have shown great potential in performing a variety of complex tasks. The emergence of such models is sure to bring significant changes to the software industry.

Firstly, LLMs provide a vehicle for **every software** to use LLM as human intention understanding.  Secondly, LLMs provide a way for **end users** to write small pieces of code without the need to learn traditional programming. Soon, anyone with a computer will be able to develop their own software tools by simply describing the desired features and the changes they want to implement in the software they are already using.

This will open the hood of software development to a much larger group of people. Everyone can use their personal computers to create their **personal** software tools. Every company can use their private data to create their **personal** software tools for internal or external uses.

**ReByte** is built to accomplish one mission and one misson only: to give everyone the ability to create their own tools by using large language models. 

Rebyte has three core components:

* Large Language Model Agent: A serverless function that can be executed on the ReByte cloud.
* Knowledge: Private data ingestion pipeline that can be used in LLM agent.
* Agent UI Builder: User interface builder that allows developers to wire up LLM agents and knowledge to create their own tools.

Also, **ReByte** is built to solve the following problems in LLM application development:

1. **Predicable LLM application**: It works on the principle of treating each LLM interaction as a single step or functional transformation on working memory, offering a predictable and manageable way to guide the thought process of a LLM. This approach results in consistent, easier-to-follow interaction flows.
2. **Iterative Nature of LLM Development**: Creating tools on top of modern LLM models can be quite challenging, due to the nature of LLMs. LLMs' output are not deterministic, and their performance can vary from time to time. We want ReByte's LLM agent builder to make this process as easy as possible.
   * We provide a unified interface for users to build, test and deploy their LLM application.
   * We also keep logs of the application, so that users can easily fix the bugs when things go wrong.
3. **Painless Private Data integration**: Today's LLM tools heavily rely on private data. Frameworks such as Langchain and LlamaIndex, together with various vector databases, provide the necessary pieces for private data embedding and search. But even for someone experiences in coding and engineering, it's hard to get the system running the first time, and usually takes hours to debug. That's why we want to make this data integration process as easy and painless as possible.
   * We provide a hosted solution for users to import data from popular data sources, such as Notion, Google, GitHub, etc., as well as from user's local computers.
   * We handle data source synchronization automatically, so users don't need to worry about data consistency.
4. **Production Serving Ready**: Provide a robust runtime ready for immediate deployment and scalable growth.
   * It's rather hard to scale LLM applications, because of its unpredictable and asynchronous nature.
   * Being inspired by serverless functions, we provide a scalable runtime for users to scale their LLM applications without having to know the details of the underlying infrastructure.
5. **Deliver Tool instead of Prompt**: LLM applications are meant to be ready-to-use tools, not just prompts. We make sure that users can deliver their LLM applications as actual tools, instead of prompts.

At its core, ReByte defines an **Agent DSL** as an intermediate representation of any LLM application, and provides a hosted runtime for users to execute their LLM applications. Introduction to Agent DSL has obvious benefits:
* can be used to build a GUI builder for users to create their own LLM application.
* can be generated by fine-tuned models
* can be edited by human

We believe that building good agents must take efforts from both human and machines, and DSL is the perfect medium for this collaboration.

<figure><img src=".gitbook/assets/Screenshot 2023-10-10 at 1.24.14 PM.png" alt=""><figcaption></figcaption></figure>

## Get Started

[rebyte-concepts.md](overview/understanding-rebyte-architecture.md)

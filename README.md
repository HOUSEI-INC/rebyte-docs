# 介绍

## 英璞来是什么?

**英璞来**是通过支持单调和重复性的任务来提高团队生产力的AI助手。

|                        | 英璞来                                           | ChatGPT团队版                                   |
| ---------------------- | ------------------------------------------------ | ----------------------------------------------- |
| 超级助手               | **Revia**                                  | ChatGPT                                         |
| 其他助手               | *团队助手*                                     | GPTs                                            |
| 支持的大语言模型厂商   | OpenAI/Gemini/Anthropic/Mistral/其他             | 仅限OpenAI                                      |
| *团队助手*使用的工具 | 通过**英璞来**搭建工作流执行任意复杂工作流 | 选择调用代码解释器/浏览器/RAG检索/外部API等功能 |
| 外部数据整合           | 自动处理与Notion/Slack/Discord/Twitter等的同步   | 无法整合外部数据                                |

## **英璞来**研发背景

市面上已经有很多AI助手，其中很多都是由非常优秀的公司打造的。但是，作为一款面向团队的AI助手，在以下方面与这些AI助手有很大不同：
为团队助理提供可以无缝整合的定制流程。每个团队都有自己的业务流程。
每个团队的知识库大不相同，AI助手需要更多的上下文来为每个团队成员提供更好的服务。
所有问题都集中在为AI助手提供更多的上下文，包括数据上下文和业务逻辑上下文。
为此我们推出了**英璞来**平台，旨在为团队提供一个可以轻松构建和使用AI助手的平台。

**英璞来**的主要特点有：

### 通用用户界面

我们提供所有团队成员都可以与AI助手对话的通用用户界面**Revia**。该界面旨在处理各种类型的任务，如数据获取、问答、文档生成、数据分析、交互式图表和表格、表格输入等。
**Revia**可以在包括Web端网页、手机、桌面在内的所有平台上使用。

### 工作流创建

**英璞来**为了扩展团队助理的功能，提供了类似于LangChain的低代码平台。正如在关于[LangChain认知架构](https://blog.langchain.dev/openais-bet-on-a-cognitive-architecture/)的博客文章中所述，大规模语言模型代理是由Chain of Thoughts这样的大规模语言模型的推理能力驱动的可以分为由“流动工程”驱动的。在后者中，开发者设计了适合团队工作流程的LLM代理。**英璞来**根据团队的工作流程提供完整的代理集来设计LLM代理，旨在最大限度地减少开发人员的编程要求。我们的目标是让开发者能够仅仅通过理解JSON来构建大规模的语言模型代理。

### 编排与执行

**英璞来**助手支持编排工具并执行。首先制定编排，一步一步地执行每项操作，然后执行编排。在数据分析任务中，助手可以自己编写Python代码，并执行该代码。助手具备自我反思的能力，如果计划没有按照预期执行，可以自己修改。

### 外部数据整合

**英璞来**通过从获得团队批准的来源整合数据，有助于创建整合的团队知识库。这种全面且整合的知识库对于之后的大规模语言模型处理应用至关重要。在初期阶段，**英璞来**目前可以从文件、网页、GitHub、Notion、Twitter等来源整合数据，并计划引入更多厂商。

### 访问控制

企业内部的数据安全一直是令人担忧的问题，团队AI助理同样需要重视这点。**英璞来**设计了基于角色的访问控制系统，以灵活控制哪些数据被谁访问。这样，企业的IT负责人可以细致地管理数据的访问权限。
**英璞来**提供强大的预设代理，能够最大限度地提高团队的生产力，代理也可以根据团队特有的需求进行定制。由此团队得以更高效、更有效地开展业务。

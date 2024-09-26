# 代理API

代理API允许您在自己的应用程序中构建AI代理。它提供了一套API来与代理交互,例如发送消息、上传文件和创建线程。

## 概述

代理API的典型集成流程如下:

1. 在rebyte代理编辑器上创建一个代理,定义其自定义动作,如`模型`、`数据`、`工具`、`控制流`等。选择您想要使用的模型和参数。

2. 当用户开始对话时创建一个线程。

3. 随着用户提问,向线程添加消息。

4. 在线程上运行代理以生成响应。

## 步骤详解

1. 创建代理。

这里,我们将使用["Chat with GPT3.5 agent"](https://rebyte.ai/p/21b2295005587a5375d8/callable/f4222f209267e5b24cda/editor)作为示例。记得先测试您的代理,确保它按预期工作。同时,点击"部署"使其可通过API使用。

2. 创建线程

在使用API之前,从侧边栏的API控制台获取您的API密钥。您应该使用此密钥来验证您的请求。

创建线程时,您可以在创建时将消息附加到线程。
您还可以为线程附加元数据。这对于以结构化格式存储对象的附加信息很有用。

```shell
curl 'https://rebyte.ai/api/sdk/threads' \
--H 'Content-Type: application/json' \
--H 'Authorization: Bearer $REBYTE_KEY' \
--H 'Cookie: NEXT_LOCALE=en' \
--d '{
     "metadata": {
        "user": "abc123"
      },
    "messages":[
        {
            "role":"user",
            "content":"Hi, how are you?"
        },
        {
            "role":"asistant",
            "content":"Hi, I am good. What about you? Is there anything I can help?"
        }
    ]
}'
```

In the response, you will find the thread id. You can use this thread id to add messages to the thread and run the agent on the thread.

* Example Response 
  
```shell
{
    "id": "UHSHhnkWGElWShQS5ZtOa",
    "created_at": 1714050659
}
```

3. Add messages to the thread

```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages' \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $REBYTE_KEY" \
  -d '{
      "role": "user",
      "content": "How does AI work? Explain it in simple terms."
    }'
```

In the response, you can see the message information.

* Example Response

```shell
{
    "id": "u8YmkrO4lYZD8r8Nl5cFh",
    "created_at": 1714051597,
    "thread_id": "UHSHhnkWGElWShQS5ZtOa",
    "role": "user",
    "content": "Teach me how to make pancake."
}
```

4. Run the agent on the thread

In order to run the agent on the thread, you should get the url from deploying your agent and make a request to this url.

```shell
curl -L https://rebyte.ai/api/sdk/p/21b2295005587a5375d8/a/f4222f209267e5b24cda/r \
    -H "Authorization: Bearer $REBYTE_KEY" \
    -H "Content-Type: application/json" \
    -d '{
    "version": 1,\
    "config": {
        "MODEL_CALL": {
            "provider_id": "openai",
            "model_id": "gpt-3.5-turbo-1106",
            "use_cache": true,
            "use_stream": false,
            "seed": null,
            "response_format": null
        }
    },
    "thread_id":"UHSHhnkWGElWShQS5ZtOa",
    "blocking": true,\
    "inputs": []
    }'
```

* When calling the agent, you should specify the thread id, and you will be able to get all the messages and metadata from the thread.

* You can also use "contentOnly:true" to get only the content of the messages.


5. Get the messages from the thread

```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages'     \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $REBYTE_KEY" \
```

In the response, you will get the list of all messages on the thread.

* Example Response

```shell
{
    "list": [
        {
            "id": "u8YmkrO4lYZD8r8Nl5cFh",
            "created_at": 1714051597,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "user",
            "content": "Teach me how to make pancake."
        },
        {
            "id": "pJWH0zkmgnQONAHr6bnA4",
            "created_at": 1714050770,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "assistant",
            "content": "Bitcoin is a decentralized digital currency, often referred to as a cryptocurrency. It was created in 2009 by an unknown person using the pseudonym Satoshi Nakamoto. Bitcoin transactions are recorded on a public ledger called a blockchain, and it operates without the need for a central authority or government. Bitcoin can be used for online transactions, as an investment, or as a store of value. It is also known for its potential to provide financial privacy and security.",
            "agent_id": "297c5b234e770dd73713",
            "name": "chat_with_gpt3_5",
            "run_id": "4ed010c66458a2ac738932d950830218a2224e7ba22e12718ad66872be6832e7"
        },
        {
            "id": "iEw3QFJys-zpacEbNgsF1",
            "created_at": 1714050764,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "user",
            "content": "What is bitcoin?"
        },
        {
            "id": "xNQZdrCSJkYhM13b25Mhp",
            "created_at": 1714050764,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "assistant",
            "content": "Hi, how are you?"
        },
        {
            "id": "tfSLCfLflDquhQ7680j8z",
            "created_at": 1714050764,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "user",
            "content": "Hello!"
        }
    ]
}
```
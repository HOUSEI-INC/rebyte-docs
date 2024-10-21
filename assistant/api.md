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
            "content":"你好,你怎么样?"
        },
        {
            "role":"assistant",
            "content":"你好,我很好。你呢?有什么我可以帮助你的吗?"
        }
    ]
}'
```

在响应中,您将找到线程id。您可以使用这个线程id向线程添加消息并在线程上运行代理。

* 示例响应
  
```shell
{
    "id": "UHSHhnkWGElWShQS5ZtOa",
    "created_at": 1714050659
}
```

3. 向线程添加消息

```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages' \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $REBYTE_KEY" \
  -d '{
      "role": "user",
      "content": "AI是如何工作的?用简单的术语解释一下。"
    }'
```

在响应中,您可以看到消息信息。

* 示例响应

```shell
{
    "id": "u8YmkrO4lYZD8r8Nl5cFh",
    "created_at": 1714051597,
    "thread_id": "UHSHhnkWGElWShQS5ZtOa",
    "role": "user",
    "content": "教我如何做煎饼。"
}
```

4. 在线程上运行代理

为了在线程上运行代理,您应该从部署的代理获取url并向这个url发出请求。

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

* 调用代理时,您应该指定线程id,您将能够从线程获取所有消息和元数据。

* 您还可以使用"contentOnly:true"来仅获取消息的内容。

5. 从线程获取消息

```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages'     \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $REBYTE_KEY" \
```

在响应中,您将获得线程上所有消息的列表。

* 示例响应

```shell
{
    "list": [
        {
            "id": "u8YmkrO4lYZD8r8Nl5cFh",
            "created_at": 1714051597,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "user",
            "content": "教我如何做煎饼。"
        },
        {
            "id": "pJWH0zkmgnQONAHr6bnA4",
            "created_at": 1714050770,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "assistant",
            "content": "比特币是一种去中心化的数字货币,通常被称为加密货币。它于2009年由一个使用化名Satoshi Nakamoto的未知人士创建。比特币交易记录在一个称为区块链的公共账本上,它无需中央权威机构或政府就能运作。比特币可用于在线交易、投资或作为价值储存。它还以提供财务隐私和安全的潜力而闻名。",
            "agent_id": "297c5b234e770dd73713",
            "name": "chat_with_gpt3_5",
            "run_id": "4ed010c66458a2ac738932d950830218a2224e7ba22e12718ad66872be6832e7"
        },
        {
            "id": "iEw3QFJys-zpacEbNgsF1",
            "created_at": 1714050764,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "user",
            "content": "什么是比特币?"
        },
        {
            "id": "xNQZdrCSJkYhM13b25Mhp",
            "created_at": 1714050764,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "assistant",
            "content": "你好,你怎么样?"
        },
        {
            "id": "tfSLCfLflDquhQ7680j8z",
            "created_at": 1714050764,
            "thread_id": "UHSHhnkWGElWShQS5ZtOa",
            "role": "user",
            "content": "你好!"
        }
    ]
}
```

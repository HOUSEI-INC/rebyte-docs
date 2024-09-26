# 消息

## 插入消息

`POST https://rebyte.ai/api/sdk/threads/{threadId}/messages`

在线程中创建一个新消息。

**路径参数**
* thread_id(必需): 一个字符串,包含要为其创建消息的线程ID。

**请求体**
* role(必需): 一个字符串,包含创建消息的实体的角色。目前只支持user。
* content(必需): 一个字符串,包含消息的内容。
* file_ids: 消息应使用的文件ID列表。一条消息最多可以附加10个文件。对于可以访问和使用文件的工具(如检索和代码解释器)很有用。
* metadata: 可以附加到对象的16个键值对集合。这对于以结构化格式存储对象的附加信息很有用。键的最大长度为64个字符,值的最大长度为512个字符。

**请求示例**
```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages' \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $REBYTE_KEY" \
  -d '{
      "role": "user",
      "content": "AI是如何工作的?用简单的术语解释一下。"
    }'
```

**返回**

一个消息对象。

**示例**
```json
{
    "id": "W_DPv1bwUQ50PC52f44Uo",
    "created_at": 1710415825,
    "thread_id": "p_DFiNmczwUWZjcl47U9X",
    "role": "user",
    "content": "AI是如何工作的?用简单的术语解释一下。",
    "metadata": {
        "user": "czy1"
    }
}
```

## 列出消息

`GET https://rebyte.ai/api/sdk/threads/{threadId}/messages`

获取线程中的消息列表。

**路径参数**
* thread_id(必需): 一个字符串,包含要为其创建消息的线程ID。

**查询参数**

* limit: 一个整数,默认为20。限制返回对象的数量。限制范围在1到100之间,默认为20。

* order: 一个字符串,默认为desc。按对象的created_at时间戳排序。asc为升序,desc为降序。

* after: 一个字符串,用于分页的游标。after是定义您在列表中位置的对象ID。例如,如果您发出列表请求并收到100个对象,以obj_foo结束,您的后续调用可以包含after=obj_foo以获取列表的下一页。

* before: 一个字符串,用于分页的游标。before是定义您在列表中位置的对象ID。例如,如果您发出列表请求并收到100个对象,以obj_foo结束,您的后续调用可以包含before=obj_foo以获取列表的上一页。

**请求示例**
```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages'     \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $REBYTE_KEY" \
```

**返回**

返回消息列表。

**示例**
```json
{
    "list": [
        {
            "id": "W_DPv1bwUQ50PC52f44Uo",
            "created_at": 1710415825,
            "thread_id": "p_DFiNmczwUWZjcl47U9X",
            "role": "user",
            "content": "AI是如何工作的?用简单的术语解释一下。",
            "metadata": {
                "user": "czy4"
            }
        }
    ]
}
```

## 获取消息

`GET https://rebyte.ai/api/sdk/threads/{threadId}/messages/{messageId}`

通过ID获取消息。

**路径参数**

* thread_id(必需): 一个字符串,包含此消息所属线程的ID。

* message_id(必需): 一个字符串,包含要检索的消息的ID。

**请求示例**
```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages/{message_id}' \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $REBYTE_KEY" 
```

**返回**

返回一个消息对象。

**示例**
```json
{
    "id": "W_DPv1bwUQ50PC52f44Uo",
    "created_at": 1710415825,
    "thread_id": "p_DFiNmczwUWZjcl47U9X",
    "role": "user",
    "content": "AI是如何工作的?用简单的术语解释一下。",
    "metadata": {
        "user": "czy4"
    }
}
```

## 更新消息

`POST https://rebyte.ai/api/sdk/threads/{threadId}/messages/{messageId}`

通过ID更新消息。

**路径参数**

* thread_id(必需): 一个字符串,包含此消息所属线程的ID。

* message_id(必需): 一个字符串,包含要检索的消息的ID。

**请求体**

* metadata: 一个映射。可以附加到对象的16个键值对集合。这对于以结构化格式存储对象的附加信息很有用。键的最大长度为64个字符,值的最大长度为512个字符。

**请求示例**
```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}/messages/{message_id}' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Bearer REBYTE_KEY" \
  -d '{
     "role": "user",
      "content": "2024年3月14日更新。情人节快乐!",
      "metadata":{
        "user":"czy4"
      }
}'
```

**返回**

返回修改后的消息对象。

**示例**
```json
{
    "id": "W_DPv1bwUQ50PC52f44Uo",
    "created_at": 1710415825,
    "thread_id": "p_DFiNmczwUWZjcl47U9X",
    "role": "user",
    "content": "AI是如何工作的?用简单的术语解释一下。",
    "metadata": {
        "user": "czy4"
    }
}
``` 


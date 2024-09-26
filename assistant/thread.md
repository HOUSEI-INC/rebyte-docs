# 线程

## 创建线程

`POST https://rebyte.ai/api/sdk/threads`

创建一个新的线程。

**请求体**
* messages: 用于启动线程的消息数组。
* metadata: 可以附加到对象的16个键值对集合。这对于以结构化格式存储对象的附加信息很有用。键的最大长度为64个字符,值的最大长度为512个字符。

**请求示例**

```shell
curl 'https://rebyte.ai/api/sdk/threads' \
--H 'Content-Type: application/json' \
--H 'Authorization: Bearer $REBYTE_KEY' \
--H 'Cookie: NEXT_LOCALE=en' \
--data '{
     "metadata": {
        "user": "abc123"
      }
}'
```

**返回**

一个线程对象。

**示例**
```json
{
    "id": "2hWVPNfrHv1IiVN7ia-4P",
    "created_at": 1710481773,
    "metadata": {
        "user": "abc123"
    }
}
```


### 列出线程

`GET https://rebyte.ai/api/sdk/threads`

获取线程列表。

**查询参数**
* limit: 一个整数,表示要返回的最大线程数。默认为20。
* order: 一个字符串,表示返回线程的顺序。默认为desc。
* before: 一个字符串,用作分页的游标。after是定义您在列表中位置的对象ID。
* after: 一个字符串,用作分页的游标。before是定义您在列表中位置的对象ID。

**请求示例**
```shell
curl  'https://rebyte.ai/api/sdk/threads?limit=10&order=desc' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer $REBYTE_KEY' \
-H 'Cookie: NEXT_LOCALE=en'
```

**返回**

线程对象列表。

**示例**
```json
{
    "list": [
        {
            "id": "2hWVPNfrHv1IiVN7ia-4P",
            "created_at": 1710481773,
            "metadata": {
                "user": "abc123"
            }
        },
        {
            "id": "NGXTNrg-34seXYc-PCVFu",
            "created_at": 1710415453,
            "metadata": {
                "user": "abc123"
            }
        },
        {
            "id": "MRlX-SOAo5gAx1mxBe7S4",
            "created_at": 1710407916
        }
    ]
}
```
### **获取线程**

`GET https://rebyte.ai/api/sdk/threads/{thread_id}`

通过ID获取线程。

**路径参数**
* thread_id(必需): 一个字符串,表示要检索的线程的ID。

**请求示例**
```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer $REBYTE_KEY' \
-H 'Cookie: NEXT_LOCALE=en'
```

**返回**
与指定ID匹配的线程对象。

**示例**
```json
{
    "id": "cB1-_3wh5ZWtUPJU4xIuU",
    "created_at": 1710415223,
    "metadata": {
        "user": "czy",
        "modified": "true"
    }
}
```

### **更新线程**

`POST https://rebyte.ai/api/sdk/threads/{thread_id}`

更新线程。

**路径参数**
* thread_id(必需): 一个字符串,表示要检索的线程的ID。

**请求体**
* metadata: 可以附加到对象的16个键值对集合。这对于以结构化格式存储对象的附加信息很有用。键的最大长度为64个字符,值的最大长度为512个字符。

**请求示例**
```shell
curl 'https://rebyte.ai/api/sdk/threads/{thread_id}' \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer $REBYTE_KEY' \
-H 'Cookie: NEXT_LOCALE=en' \
--data ' {
    "metadata": 
    {
        "modified": "true",
        "user": "czy"
    }
 }'
```

**返回**
与指定ID匹配的修改后的线程对象。

**示例**
```json
{
    "id": "cB1-_3wh5ZWtUPJU4xIuU",
    "created_at": 1710415223,
    "metadata": {
        "modified": "true",
        "user": "czy"
    }
}
```
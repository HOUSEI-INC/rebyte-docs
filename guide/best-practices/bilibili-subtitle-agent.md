# Bilibili字幕代理

帮助您获取bilibili字幕并总结内容。


### 在`数据集`中设置测试数据

```json
[
  {
    "role": "user",
    "content": "BV1Lu411J7Z8"
  }
]
```


### 从`代码动作`中提取内容

```js
_fun = (env) => {
  // 使用 `env.state.Action_NAME` 来引用前面动作的输出。
  return env.state.INPUT.messages.slice(-1)[0].content
} 
```

### 使用LLM处理用户的输入

```javascript
_fun = (env) => {
  // 使用 `env.state.Action_NAME` 来引用前面动作的输出。
 return env.state.GET_BV.completion.text
}
```

### 从`代码动作`中提取内容

```javascript
_fun = (env) => {
  // 使用 `env.state.Action_NAME` 来引用前面动作的输出。
 return env.state.GET_BV.completion.text
}
```

### 使用`HTTP请求制作器`请求CID

```javascript
api.bilibili.com/x/player/pagelist?bvid={{BV}}
```

### 从`代码动作`中提取内容

```javascript
_fun = (env) => {
  // 使用 `env.state.Action_NAME` 来引用前面动作的输出。
 return env.state.GET_CID.body.data[0].cid
}
```

### 使用`HTTP请求制作器`请求字幕的URL

```javascript
api.bilibili.com/x/player/v2?bvid={{BV}}&cid={{CID}}
```

### 从`代码动作`中提取内容

```javascript
_fun = (env) => {
  // 使用 `env.state.Action_NAME` 来引用前面动作的输出。
  // const data = JSON.stringify(env.state.GET_URL.body)
  // const regex = /<subtitle>(.*?)<\/subtitle>/;
  // const match = data.match(regex);
  // const subtitleURL = match ? match[1] : "";
  // const obj = subtitleURL.replace(new RegExp("\\\\\"","gm"),"\"")
  // const result = JSON.parse(obj)['subtitles'][0]['subtitle_url'].replace("//", "")
  const url = env.state.GET_URL.body.data.subtitle.subtitles[0].subtitle_url
  const result = url.replace(/\/\//g, "");
  return result
  
}
```

### 使用`HTTP请求制作器`请求字幕

```javascript
{{GET_CC_URL}}
```

### 从`代码动作`中提取内容

```javascript
_fun = (env) => {
  // 使用 `env.state.Action_NAME` 来引用前面动作的输出。
  let arr = []
  for(let i in env.state.GET_CC.body.body) {
    arr.push(env.state.GET_CC.body.body[i].content)
  }
 return arr.join(',')
}
```

### 发送字幕给LLM进行总结
```json
{% if GET_URL.body.data.subtitle.subtitles[0].subtitle_url == "" %}
请用以下短语回复我："抱歉，我无法从您提供的URL获取内容。请验证网址的正确性"

{% else %}
您是一个具有高级理解和总结能力的AI。您的任务是阅读以下段落并提供一个简洁、清晰的总结，捕捉主要观点和关键细节。

段落：
{{CC}}

请提供上述段落的总结并用中文回复我。

{% endif %}
```

### 从`代码动作`中提取内容

```javascript
_fun = (env) => {
  // 使用 `env.state.Action_NAME` 来引用前面动作的输出。
 return {
   role: "assistant",
   content: env.state.OUTPUT_STREAM.completion.text,
   retrievals: env.state.RETRIEVALS
 }
}
```

### 输出最终结果
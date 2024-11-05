# 网页总结代理

帮助您总结网页内容。

### 在`数据集`中设置测试数据

```json
[
  {
    "role": "user",
    "content": "https://rebyte.ai/docs/guide/best-practices/web-page-summary-agent"
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
 return env.state.GET_URL.completion.text
}
```

### 使用`网页爬虫`爬取网页内容

```javascript
{{URL}}
```

### 发送内容给LLM进行总结
```json
您是一个具有高级理解和总结能力的AI。您的任务是阅读以下段落并提供一个简洁、清晰的总结，捕捉主要观点和关键细节。

段落：
{{CRAWL.data[0].results[0].text}}

请提供上述段落的总结并用中文回复我。
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
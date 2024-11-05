# 搜索引擎代理

为您总结网页内容。

### 在`数据集`中设置测试数据

```json
[
  {
    "role": "user",
    "content": "谁赢得了上一届欧冠联赛？"
  },
  {
    "role": "assitant",
    "content": "2022-23赛季的欧冠冠军是曼城。这是他们在该项赛事中的首个冠军。皇家马德里保持着欧冠最多冠军的记录，已经14次夺冠[0][1]。"
  },
  {
    "role": "user",
    "content": "谁打进了制胜球？"
  }
]
```


### 使用`代码动作`获取最后一条消息

```javascript
_fun = (env) => {
  // 使用 `env.state.Action_NAME` 来引用前面动作的输出。
  return env.state.INPUT.messages.slice(-1)[0].content
}
```

### 使用`代码动作`获取聊天历史

```javascript
_fun = (env) => {
  // 使用 `env.state.Action_NAME` 来引用前面动作的输出。
 return env.state.INPUT.messages.slice(0, env.state.INPUT.messages.length - 1).map((m) => m.content).join("\n")
}
```

### 使用`代码动作`提取内容

```txt
{# 在这里写入您的提示，例如：'根据以下内容回答这些问题。' #}
{# 在下面开始您的提示： #}
这是问题：{{EXTRACT_QUESTION}}
这是对话历史：{{HISTORY}}

借助对话历史为问题添加必要的上下文。如果上下文不相关，则不要更改问题。在这里给出问题：
```

### 使用`Google_search`搜索相关内容
```javascript
{{REFINED_QUESTION.completion.text}}
```

### 使用`代码动作`提取内容

```javascript
// 从谷歌搜索的有机结果中提取标题、摘要和链接
// 限制为3个结果
_fun = (env) => {
  if (!env.state.GOOGLE_SEARCH.organic_results) {
    return [
      {
        title: "",
        link: ""
      }
    ]
  }

  return env.state.GOOGLE_SEARCH.organic_results.map((r) => {
    return { title: r.title, link: r.link, snippet: r.snippet };
  }).slice(0, 3);
}
```

### 映射结果以进行并行处理

```javascript
SEARCH_EXTRACT
```

### 使用`WEB_CRAWL`扫描页面
```javascript
{{SEARCH_RESULT_LOOP.link}}
```

### 使用`代码动作`提取内容
```javascript
// 对每个链接，爬取其内容并限制在2000字节
_fun = (env) => {
  return {
    content: env.state.WEB_CRAWL_1.data ? env.state.WEB_CRAWL_1.data[0].results[0].text.slice(0, 2000) : "",
  };
} 
```

### 使用LLM分析内容
```json
{# 在这里写入您的提示，例如：'根据以下内容回答这些问题。' #}
{# 在下面开始您的提示： #}

给定以下问题：
"""
{{EXTRACT_QUESTION}}
"""

从以下内容中提取与问题相关的文本并进行总结：
"""
{# {{GOOGLE_REFERENCES.content}} #}
{{SEARCH_RESULT_LOOP.snippet}}
"""

提取的总结内容：
"""
```

### 使用`代码动作`提取内容
```javascript
_fun = (env) => {
  return {
    summary: env.state.MODEL_SUMMARIZE.completion.text.trim(),
    link: env.state.SEARCH_RESULT_LOOP.link
  };    
}
```

使用`代码动作`提取内容并制作提示
```javascript
const _example = (example) => {
  // prompt = `问题：${example.question}\n`;
  let prompt = "内容：\n";
  prompt += '"""\n';
  example.forEach((d, i) => {
    if (i > 0) {
      prompt += '\n';
    }
    prompt += `链接 [${i}]: ${d.link}\n`;
    prompt += `内容: ${d.summary.replaceAll('\n', ' ')}\n`;
  });
  prompt += '"""\n';
  console.log(prompt)
  return prompt;
}

_fun = (env) => {
  prompt = '根据以下问题、参考链接和相关内容，创建一个带有引用的最终答案。如果部分答案可以用表格格式呈现，请使用表格格式。答案应准确简洁。\n\n 永远不要告诉我"作为一个语言模型..."或"作为一个人工智能..."，我已经知道你是LLM了。直接告诉我答案。\n\n';
  // env.state.EXAMPLES.forEach((e) => {
  // prompt += _example(e);
  // prompt += `最终答案：\n"""\n${e.final}\n"""\n`;
  // prompt += "\n";
  // });
  prompt += "问题：" + env.state.EXTRACT_QUESTION + "\n";
  prompt += _example(env.state.FORMAT_SUMMARY);

  prompt += `最终答案：\n"""\n`;

  return { prompt }
}
```

### 将提示发送给LLM
```json
{{FINAL_PROMPT.prompt}}
```
### 提取`OUTPUT_STREAM`作为输出
```json
{{FINAL_PROMPT.prompt}}
```


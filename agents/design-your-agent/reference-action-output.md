# 参考输出格式

### 有两种方式可以引用前面动作的输出，具体取决于动作类型。

## 普通 JavaScript 语法

使用 `env.state` 对象来访问前面动作的输出。例如，如果您想访问 `INPUT` 动作的输出，可以使用 `env.state.INPUT`。

```javascript   
const llmOutput = env.state.LLM_CALL;
```

这种语法用于所有支持 JavaScript 的字段。

## 提示模板语言

这种语法用于支持提示模板语言的其他字段。您可以使用 `{{}}` 语法来访问前面动作的输出。例如，如果您想访问 `INPUT` 动作的输出，可以使用 `{{INPUT}}`。

例如，如果您想访问 `INPUT` 动作的第一条消息，可以使用 `{{INPUT.messages[0].content}}`。
```markup
{{INPUT.messages[0].content}}
```

提示模板语言是一种简单的语言，允许您创建可用于生成 LLM 模型提示的模板。提示模板语言是 [Jinja](https://jinja.palletsprojects.com/en/3.1.x/) 模板语言的一个子集。以下是一些使用提示模板语言的示例，有关语法的更多信息，请参见 [Jinja 文档](https://jinja.palletsprojects.com/en/3.1.x/templates/)。

使用 \{\{ 和 \}\} 表示表达式

```
{{ 1 + 1 }}
```

引用变量

```
{{ variable_name }}
```

for 语句

```markup
{% raw %}
{% for i in range(10) %}
    {{ i }}
{% endfor %}
{% endraw %}
```

{# 和 #} 用于注释。要注释模板的某个部分，将其包装在 {# #} 中。这些标签之间的任何内容都不会被渲染。

```
{# 这是一条注释 #}
```

可以使用点号(.)访问结构和属性，如 \{\{ product.name \}\}。数组或元组的特定成员可以使用 .i 表示法访问，其中 i 是从零开始的索引。在点表示法中，点号后面不能使用变量。

```
{{ product.name }}
{{ product[0] }}
```

测试可以用于检查表达式的某些条件，在 if 块中使用 is 关键字进行测试。例如，要测试一个表达式是否为奇数，您可以这样写：

```markup
{% raw %}
{% if number is odd %}
    这是一个奇数
{% endif %}
{% endraw %}
```

测试也可以取反：

```markup
{% raw %}
{% if number is not odd %}
    这不是一个奇数
{% endif %}
{% endraw %}
```
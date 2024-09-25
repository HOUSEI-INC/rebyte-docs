# 有两种方式可以引用之前操作的输出，具体取决于操作类型。

## 普通 JavaScript 语法

使用 `env.state` 对象来访问之前操作的输出。例如，如果你想访问 `INPUT` 操作的输出，可以使用 `env.state.INPUT`。

```javascript   
const llmOutput = env.state.LLM_CALL;
```

<<<<<<< Updated upstream
This syntax is used in all fields that support javascript.

## Prompt template language

This syntax is used in other fields that support the prompt template language. You can use the `{{}}` syntax to access the output of previous actions. For example, if you want to access the output of the `INPUT` action, you can use `{{INPUT}}`.

for example, if you want to access the first message of the `INPUT` action, you can use `{{INPUT.messages[0].content}}`.
=======
这种语法用于所有支持 JavaScript 的字段。

## 提示模板语言

这种语法用于支持提示模板语言的其他字段。你可以使用 `{{}}` 语法来访问之前操作的输出。例如，如果你想访问 `INPUT` 操作的输出，可以使用 `{{INPUT}}`。

比如，如果你想访问 `INPUT` 操作的第一条消息，可以使用 `{{INPUT.messages[0].content}}`。
>>>>>>> Stashed changes
```markup
{{INPUT.messages[0].content}}
```

<<<<<<< Updated upstream
The Prompt Template Language is a simple language that allows you to create a prompt template that can be used to generate prompts for your LLM models. The Prompt Template Language is a subset of the [Jinja](https://jinja.palletsprojects.com/en/3.1.x/) templating language. Here are some examples of how you can use the Prompt Template Language, for more information on the syntax, see the [Jinja documentation](https://jinja.palletsprojects.com/en/3.1.x/templates/).

\{\{ and \}\} for expressions
=======
提示模板语言是一种简单的语言，允许你创建可用于为 LLM 模型生成提示的模板。提示模板语言是 [Jinja](https://jinja.palletsprojects.com/en/3.1.x/) 模板语言的一个子集。以下是一些使用提示模板语言的例子，有关语法的更多信息，请参阅 [Jinja 文档](https://jinja.palletsprojects.com/en/3.1.x/templates/)。

\{\{ 和 \}\} 用于表达式
>>>>>>> Stashed changes

```
{{ 1 + 1 }}
```

<<<<<<< Updated upstream
For referencing variables
=======
用于引用变量
>>>>>>> Stashed changes

```
{{ variable_name }}
```

<<<<<<< Updated upstream
for statements
=======
for 语句
>>>>>>> Stashed changes

```markup

{% raw %}
{% for i in range(10) %}
    {{ i }}
{% endfor %}
{% endraw %}
<<<<<<< Updated upstream

```

{# and #} for comments To comment out part of the template, wrap it in {# #}. Anything in between those tags will not be rendered.

```
{# This is a comment #}
```

Construct and attributes can be accessed by using the dot (.) like \{\{ product.name \}\}. Specific members of an array or tuple are accessed by using the .i notation, where i is a zero-based index. In dot notation variable can not be used after the dot (.).
=======
```

{# 和 #} 用于注释。要注释掉模板的一部分，将其包裹在 {# #} 中。这些标签之间的任何内容都不会被渲染。

```
{# 这是一条注释 #}
```

可以使用点 (.) 访问构造和属性，如 \{\{ product.name \}\}。数组或元组的特定成员可以使用 .i 表示法访问，其中 i 是从零开始的索引。在点表示法中，变量不能在点 (.) 之后使用。
>>>>>>> Stashed changes

```
{{ product.name }}
{{ product[0] }}
```

<<<<<<< Updated upstream
Tests can be used against an expression to check some condition on it and are made in if blocks using the is keyword. For example, you would write the following to test if an expression is odd:
=======
测试可以用于检查表达式的某些条件，在 if 块中使用 is 关键字进行测试。例如，你可以这样写来测试一个表达式是否为奇数：
>>>>>>> Stashed changes

```markup

{% raw %}
{% if number is odd %}
<<<<<<< Updated upstream

    This is an odd number

=======
    这是一个奇数
>>>>>>> Stashed changes
{% endif %}
{% endraw %}

```

<<<<<<< Updated upstream
Tests can also be negated:

```

{% raw %}
{% if number is not odd %}

    This is not an odd number

=======
测试也可以被否定：

```
{% raw %}
{% if number is not odd %}
    这不是一个奇数
>>>>>>> Stashed changes
{% endif %}
{% endraw %}
```
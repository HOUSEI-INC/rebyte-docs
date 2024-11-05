# 提示模板语言

提示模板语言是一种简单的语言，允许您创建可用于生成LLM模型提示的提示模板。提示模板语言是[Jinja](https://jinja.palletsprojects.com/en/3.1.x/)模板语言的一个子集。以下是一些使用提示模板语言的示例，有关语法的更多信息，请参见[Jinja文档](https://jinja.palletsprojects.com/en/3.1.x/templates/)。

\{\{ 和 \}\} 用于表达式

```
{{ 1 + 1 }}
```

用于引用变量

```
{{ variable_name }}
```

for语句

```markup
{% raw %}
{% for i in range(10) %}
    {{ i }}
{% endfor %}
{% endraw %}
```

{# 和 #} 用于注释。要注释模板的某个部分，将其包装在{# #}中。这些标签之间的任何内容都不会被渲染。

```
{# 这是一条注释 #}
```

可以使用点号(.)访问结构和属性，如\{\{ product.name \}\}。数组或元组的特定成员可以使用.i表示法访问，其中i是从零开始的索引。在点表示法中，点号后面不能使用变量。

```
{{ product.name }}
{{ product[0] }}
```

测试可以用于检查表达式的某些条件，在if块中使用is关键字进行测试。例如，要测试一个表达式是否为奇数，您可以这样写：

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

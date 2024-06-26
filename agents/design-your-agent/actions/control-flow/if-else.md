# If Else（条件分岐）

`If Else`アクションを使用すると、条件に基づいてアクションを実行できます。

## 使用方法

* エージェントに`If Else`アクションを追加すると、同じ名前の2つのブロック（例えば "IF_ELSE_1"）がアクションに追加されます。

<figure><img src="../../../../images/if.png"></figure>

* 条件をJavaScript形式で入力します。この関数はブール値を返す必要があります。

<figure><img src="../../../../images/if-2.png"></figure>

* 実行中にシステムは条件が真かどうかを判断します。もし条件が真であれば、最初の`If_Else`ブロックと2番目の`If_Else`ブロックの間のアクションが実行されます。そうでない場合、実行は2番目の`If_Else`ブロックの後にジャンプします。

* **注意**: `If Else`アクションの結果は配列です。`env.state.LOOP_1[0]`や`{{LOOP_1[0]}}`のような形式を使用してください。

## エージェントの例

* [If Else エージェント](https://rebyte.ai/p/21b2295005587a5375d8/callable/f6f55d6029c8a0aedd53/editor)
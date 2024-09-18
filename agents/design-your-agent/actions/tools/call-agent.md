# Call Another Tool

`Call Another Tool` アクションを提供しており、エージェント内で他のエージェントをアクションとして呼び出すことができます。

## 使用方法

- エージェントに `Call Another Tool` アクションを追加します。

<figure><img src="../../../../images/call-agent-1.png"></figure>

- 呼び出したいエージェント（ここでは **"エージェント B"** とします）を選択し、適切なバージョンを選択します。

<figure><img src="../../../../images/call-agent-2.png"></figure>

<figure><img src="../../../../images/call-agent-3.png"></figure>

- エージェント B の「Input Args」を入力します。エージェント B の出力はこのアクションの出力となります。

<figure><img src="../../../../images/call-agent-4.png"></figure>

- **注意**: 「Input Args」 を入力する前に、エージェント B の入力形式を十分に理解してください。そうでないと、システムがエラーをスローします。

- 「Block Configs」を使用して、エージェント B のアクションを構成します。

## 出力

このアクションの出力は以下のようになります:

<figure><img src="../../../../images/call-agent-5.png"></figure>

JSON

| パラメーター | タイプ | 説明                             |
| ------------ | ------ | -------------------------------- |
| status.run   | object | 呼び出しの結果（成功または失敗） |
| results      | object | レスポンス                       |
| others       | object | 呼び出されたエージェントの状態         |

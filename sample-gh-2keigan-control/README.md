# sample-gh-2keigan-control

* gh から 2 台つないだ KeiganMotor をつないだ Node-RED を動かす仕組みです。
* gh から degree1 degree2 という角度情報を `{"degree1":180,"degree2":60}` という JSON データで送って、Keigan をつないだ Node-RED で 1 台目は KeiganMotor が 180 度動き、2 台目は KeiganMotor が 60 度動くという仕組みです。
* sample-gh-keigan-nodered のサンプルが動かせている前提で、進めましょう。

## 事前準備

[KeiganMotorを複数接続する場合の注意点 – 株式会社Keigan－KeiganMotor ドキュメント](https://docs.keigan-motor.com/keiganpi/two_or_more)

こちらを注意しつつ、必ず、事前に、2 台の KeiganMotor を Raspberry Pi につないでから作業を始めましょう。

## Node-RED

[node-red-flow.json](node-red-flow.json) をインポートします。

![image](https://i.gyazo.com/4269a9e4145f7e27a9f620b0f4c97caa.png)

Node-RED を起動している IP アドレスを確認します。

## 2 つの KeiganMotor の指定を AutoDetect から切り替える

通常、1台であれば AutoDetect で自動認識されますが、2台の場合は、デバイス名を名指しして挙動を分けます。

![image](https://i.gyazo.com/21c97cf0a329044528cc136de50b9df2.png)

こちらを設定します。

![image](https://i.gyazo.com/02d98ce03144cbb8965297965c38d95e.png)

まず、1 台目のノードをダブルクリックしましょう。

![image](https://i.gyazo.com/f62bc91be9779f92e0def04b00a61c63.png)

再スキャンで 2 台ぶん認識されたら、AutoDetect から 1 台目のデバイス名に切り替えます。

![image](https://i.gyazo.com/9c09baae7becccc15da9b70b5a96bb6e.png)

このように切り替えます。

![image](https://i.gyazo.com/6248330d38f34bdc36788f0677857a62.png)

この操作を 2 台目のノードの方にも設定を行います。

![image](https://i.gyazo.com/a3ebf869919f6d148a4b461fd7bbbd2d.png)

こちらをデプロイして反映します。

![image](https://i.gyazo.com/5f18dc1bc958ac273887687130729311.png)

テストで試してみましょう。

## Grasshopper http-2keigan-degree-data-request.gh

![image](https://i.gyazo.com/be31b894d997bdd43e7a21f9a9eeb6a8.png)

[http-2keigan-degree-data-request.gh](./http-2keigan-degree-data-request.gh) を開きます。

![image](https://i.gyazo.com/b8966dfca2808a0070d663a951697870.png)

2つのスライダを動かして Keigan を連動させてみましょう。

![image](https://i.gyazo.com/0ec54aefda6e3033a1217d91ddb6c943.png)

Node-RED がデータを受け取ります。上記の 2 つのスライダの最後の値がうまく反映されています。
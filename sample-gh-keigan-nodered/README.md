# sample-gh-keigan-nodered

* gh から 1 台つないだ KeiganMotor をつないだ Node-RED を動かす仕組みです。
* たとえば、gh から degree という角度情報を `{"degree":30}` という JSON データで送って、KeiganMotor をつないだ Node-RED で 30 度 KeiganMotor が動くという仕組みです。
* sample1 のサンプルが動かせている前提で、進めましょう。

## Node-RED

[node-red-flow.json](node-red-flow.json) をインポートします。

![image](https://i.gyazo.com/d57fc925070cb8692d9bba54c29ea150.png)

Node-RED を起動している IP アドレスを確認します。

## Grasshopper http-degree-data-request.gh

![image](https://i.gyazo.com/c93572c548179c40a9f4d6cbbeb20cef.png)

`http-degree-data-request.gh` を開く。

![image](https://i.gyazo.com/4fbb0fc7fbbc5c0dde24ef60287e9022.png)

スライダを動かして Keigan を連動させてみましょう。
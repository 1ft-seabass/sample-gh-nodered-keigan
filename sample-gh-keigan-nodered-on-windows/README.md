# sample-gh-keigan-nodered-on-windows

## 注意 : Windows 専用です

[sample-gh-keigan-nodered](../sample-gh-keigan-nodered/README.md) が Raspberry Pi で動くものなので、同じような仕組みを Windows で動くようにしたものです。

- 2022/02/13 時点で、[node-red-contrib-keigan-motor-sequencer](https://flows.nodered.org/node/node-red-contrib-keigan-motor-sequencer) は Windows にインストールできません
- そのため [Keigan ローレベル API](https://docs.keigan-motor.com/software_dev/lowapis/lowlevel_api_summary) で、直接シリアルポートに命令する形で実現しています。

もしかすると Mac でもイケるかもしれないです。

## Raspberry Pi でやりたい方は

素直に [sample-gh-keigan-nodered](../sample-gh-keigan-nodered/README.md) で設定を行いましょう。

## この仕組みについて

* gh から 1 台つないだ KeiganMotor をつないだ Node-RED を動かす仕組みです。
* たとえば、gh から degree という角度情報を `{"degree":30}` という JSON データで送って、KeiganMotor をつないだ Node-RED で 30 度 KeiganMotor が動くという仕組みです。
* sample1 のサンプルが動かせている前提で、進めましょう。

## 動かすために必要な情報

- Node-RED を動かしている Windows PC の IP アドレス
  - GH から HTTP アクセスするために必要です。
  - Node-RED を動かしている Windows PC のコマンドプロンプトで `ipconfig` コマンドで IP アドレスを把握します
    - 参考: [ipconfig　～Windowsのネットワーク設定を確認する：ネットワークコマンドの使い方 - ＠IT](https://atmarkit.itmedia.co.jp/ait/articles/0109/29/news005.html)
  - GH と Node-RED が同じ PC である場合は、localhost か 127.0.0.1 でアクセスできます。
- Node-RED を動かしている Windows PC がつなげている Keigan モーターのシリアルポートのアドレス
  - `COM1` のような `COM` + `数字` という形で把握しましょう
  - まず、[LED 接続チェック sample-connectivity-check-on-by-led-windows](../sample-connectivity-check-on-by-led-windows/README.md) でシリアルポートの把握に慣れておきましょう。

## Node-RED

[node-red-flow.json](node-red-flow.json) をインポートします。

![image](https://i.gyazo.com/2b8b5d480474bb18933fb7310315af87.png)

Node-RED を起動している IP アドレスを確認します。

![image](https://i.gyazo.com/0099ef1898085b6a8d362b8ec071f16d.png)

COM4 と書いてある serialport ノードをダブルクリックしてプロパティ設定を表示します。

![image](https://i.gyazo.com/44788ed5f4d2e9185e14448b3ce8a9a1.png)

鉛筆ボタンをクリックしてシリアルポート設定に移動します。

![image](https://i.gyazo.com/1324ebfb35b1dfb804ab780b0e217c4e.png)

虫眼鏡ボタンで、`Node-RED を動かしている Windows PC がつなげている Keigan モーターのシリアルポートのアドレス` が出てきたらクリックして設定します。

更新ボタンをクリックして、シリアルポート設定画面から serial out ノードを編集画面に戻り、完了ボタンをクリックしてプロパティ設定を完了します。

![image](https://i.gyazo.com/b98fa4abca71ee00245921b4f770d94b.png)

デプロイしたら設定完了です。

## Grasshopper http-degree-data-request.gh

![image](https://i.gyazo.com/c93572c548179c40a9f4d6cbbeb20cef.png)

`http-degree-data-request.gh` を開く。

![image](https://i.gyazo.com/4fbb0fc7fbbc5c0dde24ef60287e9022.png)

スライダを動かして Keigan を連動させてみましょう。
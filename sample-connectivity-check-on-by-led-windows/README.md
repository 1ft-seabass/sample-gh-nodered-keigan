## 注意 : Windows 専用です

[sample-gh-keigan-nodered](../sample-gh-keigan-nodered/README.md) が Raspberry Pi で動くものなので、同じような仕組みを Windows で動くようにしたものです。

- 2022/02/13 時点で、[node-red-contrib-keigan-motor-sequencer](https://flows.nodered.org/node/node-red-contrib-keigan-motor-sequencer) は Windows にインストールできません
- そのため [Keigan ローレベル API](https://docs.keigan-motor.com/software_dev/lowapis/lowlevel_api_summary) で、直接シリアルポートに命令する形で実現しています。

もしかすると Mac でもイケるかもしれないです。

## Raspberry Pi でやりたい方は

素直に [sample-gh-keigan-nodered](../sample-gh-keigan-nodered/README.md) で設定を行いましょう。

## この仕組みについて

- Windows PC において、その PC にインストールした Node-RED と、おなじく、その PC に USB シリアル接続した Keigan モーターの接続チェックをするものです。

## 動かすために必要な情報

- Node-RED を動かしている Windows PC がつなげている Keigan モーターのシリアルポートのアドレス
  - `COM1` のような `COM` + `数字` という形で把握しましょう
  - [[sample] Windows C# による KeiganMotor 制御 > シリアルポートの確認](https://docs.keigan-motor.com/software_dev/windows-c/windows-c-sharp-net#i-3) でKeiganMotor を接続し、シリアルポートの確認を行って下さい。シリアルポートの番号は、Windows の [デバイスマネージャ] > [ポート] から確認できます。

## Node-RED

![image](https://i.gyazo.com/1bcb031e65634e9755d8d2e41201852c.png)

[node-red-flow.json](node-red-flow.json) をインポートします。

![image](https://i.gyazo.com/18ed6fd8dd0245c0d57c8e20d799d78d.png)

COM4 と書いてある serialport ノードをダブルクリックしてプロパティ設定を表示します。

![image](https://i.gyazo.com/44788ed5f4d2e9185e14448b3ce8a9a1.png)

鉛筆ボタンをクリックしてシリアルポート設定に移動します。

![image](https://i.gyazo.com/1324ebfb35b1dfb804ab780b0e217c4e.png)

虫眼鏡ボタンで、`Node-RED を動かしている Windows PC がつなげている Keigan モーターのシリアルポートのアドレス` が出てきたらクリックして設定します。

更新ボタンをクリックして、シリアルポート設定画面から serial out ノードを編集画面に戻り、完了ボタンをクリックしてプロパティ設定を完了します。

![image](https://i.gyazo.com/b98fa4abca71ee00245921b4f770d94b.png)

デプロイしたら設定完了です。

![image](https://i.gyazo.com/0406a02678f24d0405416e6247ec3bfd.png)

R , G , B と書いてある inject ノードからデータを送って、 Keigan モーターの LED のカラーが変更されたら接続成功です。
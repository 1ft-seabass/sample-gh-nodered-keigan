# sample-gh-2keigan-nodered-on-windows

## 注意 : Windows 専用です

[sample-gh-keigan-nodered](../sample-gh-keigan-nodered/README.md) が Raspberry Pi で動くものなので、同じような仕組みを Windows で動くようにしたものです。

- 2022/02/13 時点で、[node-red-contrib-keigan-motor-sequencer](https://flows.nodered.org/node/node-red-contrib-keigan-motor-sequencer) は Windows にインストールできません
- そのため [Keigan ローレベル API](https://docs.keigan-motor.com/software_dev/lowapis/lowlevel_api_summary) で、直接シリアルポートに命令する形で実現しています。

もしかすると Mac でもイケるかもしれないです。

## Raspberry Pi でやりたい方は

素直に [sample-gh-keigan-nodered](../sample-gh-keigan-nodered/README.md) で設定を行いましょう。

## この仕組みについて

- gh から 1 台つないだ KeiganMotor をつないだ Node-RED を動かす仕組みです。
- たとえば、gh から degree という角度情報を `{"degree":30}` という JSON データで送って、KeiganMotor をつないだ Node-RED で 30 度 KeiganMotor が動くという仕組みです。
- Windows PC において、[LED による Keigan 疎通確認 sample-connectivity-check-on-by-led-windows](../sample-connectivity-check-on-by-led-windows/README.md) と [1 台の Keigan モーターでの操作 sample-gh-keigan-nodered-on-windows](../sample-gh-keigan-nodered-on-windows/README.md) が、ちゃんと成功してから、この手順に着手しましょう。
  - いきなり着手すると、チェックすべき項目がかなりあるので、むちゃくちゃハマると思います。着実に行きましょう。

## 動かすために必要な情報

- Node-RED を動かしている Windows PC の IP アドレス
  - GH から HTTP アクセスするために必要です。
  - Node-RED を動かしている Windows PC のコマンドプロンプトで `ipconfig` コマンドで IP アドレスを把握します
    - 参考: [ipconfig　～Windowsのネットワーク設定を確認する：ネットワークコマンドの使い方 - ＠IT](https://atmarkit.itmedia.co.jp/ait/articles/0109/29/news005.html)
  - GH と Node-RED が同じ PC である場合は、localhost か 127.0.0.1 でアクセスできます。
- Node-RED を動かしている Windows PC がつなげているシリアルポートのアドレス
  - 1 台目の Keigan モーターのシリアルポートのアドレス
  - 2 台目の Keigan モーターのシリアルポートのアドレス

## Node-RED

[node-red-flow.json](node-red-flow.json) をインポートします。


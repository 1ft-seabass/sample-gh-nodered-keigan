# sample-gh-nodered-keigan

## 事前準備

[KeiganPi Node\-RED チュートリアル – 株式会社Keigan－KeiganMotor ドキュメント](https://docs.keigan-motor.com/keiganpi/keiganpi-tutorial)

を見て、Raspberry Pi の Node-RED で、KeiganMotor を操作できるようにしていきましょう。

## 接続時のトラブルシューティング

はじめの接続時に詰まるポイントが多く、以下のチェックを行っていくと良いです。

Keigan モーターにモバイルバッテリーから電源がつながっている？

* https://docs.keigan-motor.com/basic/power
* 付属のUSBケーブルでつなぐと成功率が高い
* モバイルバッテリーはバッテリー給電性能に影響するので選定注意
* ティーチングプレイバックを単体で試してみましょう
* https://docs.keigan-motor.com/basic/motion 
* これで動くと単体ではバッテリー込みで大丈夫

コネクタカバーを開けてシリアル接続用の micro USB が見えている？

* 部品図
  * https://docs.keigan-motor.com/readmefirst/partnames 
* 開け方
  * https://docs.keigan-motor.com/software_dev/ports_on_wire 
  * ＋ドライバーが必要なので、手元にない場合は難しいかも（詰まるポイント）

シリアル接続用の micro USB に、通信用 USB ケーブルを差し込んでいる？

* この時点で、付属のUSBケーブルで給電していて消費している。なので別に、シリアル接続用の micro USB に、通信用 USB ケーブルを用意する。
* 充電用 USB ケーブル挿してしまうとデータのやり取りができず動かない。さらに見た目から間違っていることに気づくのに時間がかかるので注意。

シリアル接続用の micro USB した通信用 USB ケーブルが Raspberry Pi のUSBポートにつながっている？

* この段階で改めて、 1. の給電部分が Raspberry Pi のUSBポートから行われていないことを確認する。（行われていないことが正解）

Node-RED に node-red-contrib-keigan-motor-sequencer をインストールできている？

* https://flows.nodered.org/node/node-red-contrib-keigan-motor-sequencer

以下のチュートリアル初動で Keigan モーターを回転できている？

* https://docs.keigan-motor.com/keiganpi/keiganpi-tutorial  


## 接続確認をします sample1

準備ができたら、最初に [sample1](./sample1/README.md) で、gh と Node-RED の接続を確認します。

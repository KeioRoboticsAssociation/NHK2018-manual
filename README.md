# gamepad-receiver-f446
USB HIDゲームパッド（いわゆるDirectInput対応ゲームパッド）の入力をNucleo F446-REで受けてCANで送信します

[Download](https://github.com/KeioRoboticsAssociation/gamepad-receiver-f446/releases)

## 対応機種
標準的なUSB HID(DirectInput)ゲームパッド

### 動作確認済み
* [ELECOM JC-U2410T](http://www2.elecom.co.jp/peripheral/gamepad/jc-u2410t/)
* [Buffalo BSGP1204](http://buffalo.jp/product/input/gamepad/bsgp1204/)
* [Logicool F710](https://gaming.logicool.co.jp/ja-jp/product/f710-wireless-gamepad)

### 不具合あり
* [Logicool F310](https://gaming.logicool.co.jp/ja-jp/product/f310-gamepad)

## 仕様
### 接続
|Nucleo F446-RE|      |
|:------------:|:----:|
|PA12(CN10-12) |USB D+|
|PA11(CN10-14) |USB D-|
|PB9(CN10-5)   |CAN Tx|
|PB8(CN10-3)   |CAN Rx|

### フレーム
|速度|形式|ID|
|:-----:|:------:|:-----:|
|500kbps|Standard|`0x334`|

### データ
|byte|name|type  |range   |
|:--:|:--:|:----:|:------:|
|1   |LX  |int8_t|-100~100|
|2   |LY  |int8_t|-100~100|
|3   |RX  |int8_t|-100~100|
|4   |RY  |int8_t|-100~100|
|5   |number of buttons|uint8_t|17~24|
|6~8 |button[number of buttons]|bool(1bit)|0~1|

ボタンは最低17bit、最大24bit連続し、不足分及びバイトアライメントに到達しない分は0埋め

ボタン配置は[W3C Standard Gamepad](https://w3c.github.io/gamepad/#remapping)を参照(機種によって若干変わります))

### シリアル通信（動作確認用）
115200bps

## 実装例
CAN機能付きmbed向け[実装例](example)（TODO: C++11を前提としたコードのため、オンラインコンパイラ使用時は適宜修正してください）

## ビルド
Makefile見て察してくだしあ

# 良くある質問と回答

CHIRIMEN Raspi3 を利用していて良くある質問や回答のメモページです。利用上のテクニックや知っておくと良いことは [TIPS ページ](tips.md) に、デバッグの仕方や良くあるエラーメッセージに対応は [デバッグページ](debug.md) に書いているので、そちらも合わせてご覧ください。

## できること・できないこと

### CHIRIMEN Raspi3 では何が出来ますか？

CHIRIMEN Raspi3 は一般的な Web アプリケーションの開発環境に、GPIO と I2C という IoT プロトタイピングなどでよく使われるハードウェアインターフェイスを [Web GPIO API](http://browserobo.github.io/WebGPIO/) と [WebI2C API](http://browserobo.github.io/WebI2C/) を用いてウェブブラウザの JavaScript から直接制御可能にしたものです。

デスクトップの Web アプリで出来ることは全て同じようにして実装可能ですし、Web アプリで出来ないことはローカルのサーバと通信させたり拡張機能を作って通信させたりして他のコンテキストや言語の環境で実行させることもあります。いろいろな応用の仕方は [TIPS ページ](tips.md) も参考にしてください。

GPIO, I2C 以外によく見聞きするハードのインターフェイスについては次の通りです:

* UART
  * MIDI であれば WebMIDI からコントロール可能です。それ以外はローカルにサーバを立ててサーバ側で処理するなどしてください。
* PWM
  * [CHIRIMEN Examplesに掲載されているI2C PWMコントローラ PCA9685](http://chirimen.org/chirimen-raspi3/gc/top/examples/)を使って、サーボ・DCモーター・さらにLEDのPWM制御ができます。
  * それ以外はローカルにサーバを立ててサーバ側で処理するか Arduino を組み合わせるなどして制御します。いずれの場合もデバイスの仕様 (データシート) をしっかり確認してから使ってください。対応する周波数以外の信号を送るとデバイスにロックがかかったり発熱して故障したりする原因となります。
* SPI
  * クロック、入力、出力の 3 本で双方向通信を行う機能です。CHIRIMEN では現在の所 SPI を JavaScript から直接制御する API を実装していません。SPI を利用したい場合はローカルにサーバを立ててサーバ側で処理するか Arduino を組み合わせるなどして制御します。
  

また、GPIO, I2Cに対しては以下の制限があります。
* GPIO
  * 概ね50ms以下の周期で細かくHigh/Lowを切り替える必要があるもの（例えばステッピングモータを高速に動かしたいなど）や、概ね50ms以上の精度を必要とするも、複数のGPIO端子を同様な高精度で同期させる必要があるものは困難です。
  * ハードウェア上で用意されている本数以上のGPIOを用いるもの（I2C接続のGPIOマルチプレクサを使うことでI2C経由で対応可能と思われますが未検証です)
* I2C
  * 標準モード以外のモードで動作するもの
  * ハードウェア上で用意されている本数以上のI2Cバスの本数が必要なもの

## 動作環境

### Raspberry Pi 3 Model A+ はサポートしないの？

理論的には移植可能と考えられますが、本ページの執筆時点では技適通過モデルの販売が開始されておらず、未検証です。Model B, Model B++ と比べると Model A+ ではメモリ容量が半分となるため、Chromium 以外に多くのアプリケーションを同時に起動すると処理が重たくなることが予想されます。

### Raspberry Pi Zero はサポートしないの？

論理的には移植可能と考えられますが、未検証・未対応です。

### Raspberry Pi 以外のボードでは動作しないの？

CHRIMEN コミュニティで公式にサポートしている環境はありませんが、Chrome (Chromium) や Firefox のようなブラウザが動作し、Node サーバなどがインストールできる環境であればほぼ同様にして動作するように移植可能と考えられます (実際いくつかのボードで試して使っているコミュニティメンバーもいます)。

もちろん、ポート番号など物理配線が違う場合はそれに合わせてコードを書き換える必要があることには注意が必要です。

## 採用事例

### CHIRIMEN Raspi3 の採用事例は？

CHIRIMEN Raspi3 と本チュートリアル教材は例えば以下のような場所で学生や若者などを対象として、IoT システム開発やプロトタイピング、アイデアを実現・改良していくプロセスを学ぶ教材として利用されています。

- 総務省主催「[Web×IoT メイカーズチャレンジ](https://webiotmakers.github.io/)」(一部の地域)
- [Mozilla Festival でのワークショップ](https://www.webdino.org/updates/blog/201811281246/)
- 慶應義塾大学 環境情報学部の「オープンデザイン実践」
- 中央大学の「オープンプロジェクト演習」

もちろん、オープンソースで公開されており自由に使われているため、これらは CHIRIMEN コミュニティに利用報告やフィードバックがあった一例に過ぎず、コミュニティの知らないところでも利用が広がっています (広がっていくことを期待しています)。

CHIRIMEN Raspi3 を採用されている大学その他の教育関係者、イベント主催者、企業などで採用事例として掲載を希望される方は [本ページの Github リポジトリのファイル](https://github.com/chirimen-oh/tutorials/blob/master/raspi3/ja/faq.md) に対して追記するプルリクエストを頂くか、コミュニティの

## サポート

### サポート窓口・お問い合わせ窓口は何処ですか？
### CHIRIMEN Raspi3 に関して質問がしたい

CHIRIMEN Raspi3 は特定の企業・法人によって開発されているものではなく、その活動を支援する個人・法人が有志で集まるコミュニティによって開発が続けられています。従って、サポートサービスなどは提供されていません。ご利用になる皆さん自身もコミュニティの一員としてご利用頂くこととなり、不明点や質問などについてはコミュニティ内での相互サポートをご利用ください。

具体的には以下の方法でコミュニティ内でのコミュニケーション・問い合わせ・相互サポートが可能です:

* [CHIRIMEN コミュニティ Slack](https://chirimen-oh.slack.com/) - [Slack への参加用リンク](https://docs.google.com/forms/d/1GzkGfCcsRn4A6-uHPsLu2LszkqKcNJ3sFI4XRishHsE/viewform)
* [CHIRIMEN コミュニティの GitHub](https://github.com/chirimen-oh/) 配下の各リポジトリの Issues
* コミュニティに参加しているメンバーに個人的に問い合わせる

## サービス連携

### メールを送信したい

スパム対策などもあり、ローカルのメールサーバなどからの送信は正しく配信されないことがあるため、Gmail などのメールサービスを利用して送信することが望ましいです。Gmail などのメール送信 API を利用するための認証などの実装が面倒な場合は IFTTT のトリガーとして [Webhook](https://ifttt.com/maker_webhooks) を、アクションとして [Gmail](https://ifttt.com/gmail) を利用するなどすれば比較的簡単にメールの送信が可能です。

### LINE, Slack その他のサービスと連携したい

IFTTT のトリガーとして [Webhook](https://ifttt.com/maker_webhooks) を利用すると簡単に様々なサービスとの連携が可能です。Webhook 用の URL や使い方は IFTTT にログインしてから [Webhook](https://ifttt.com/maker_webhooks) ページからリンクされている documents ページや [Webhooks settings ページ](https://ifttt.com/services/maker_webhooks/settings) をご覧ください。

IFTTT では応答性が悪い (トリガーをキックしてからアクションまでの待ち時間が長すぎる) 場合は連携先のサービスの API を使って自分で直接各サービスとの連携を実装してください。

## 他のプログラムとの連携

CHIRIMEN ではブラウザ上の JavaScript だけでハードウェア制御を可能にしていますが、様々な理由で C, Python, Node, シェルスクリプトなどで書かれたコードと連携したいことがあります。そのような場合はブラウザの JavaScript とバックエンドのコードとの間を WebSocket で接続して通信させながら動作させてください (非常に高速な通信が必要な場合は除く)。

例えば Node で WebSocket サーバを作る場合はこのように index.js ファイルを作成し

```javascript
// Node で実行する JavaScript (index.js)
var WebSocketServer = require('ws').Server;
var wss = new WebSocketServer({ port:8080 });

wss.on('connection', function(ws) {
    // ブラウザからメッセージを受信した時の処理
    ws.on('message', function(message) {
        console.log("Message Received: " + message);
    });

    // ブラウザにメッセージを送信する時の処理
    wss.clients.forEach(function(client){
        client.send("A message from server");
    });
});
```

次のように ws モジュールのインストールと node サーバの実行をすればサーバが起動します。

```sh
// ws モジュールを現在のディレクトリにインストール (初回一度だけ必要)
npm install ws
// index.js を node で実行する:
node index.js
```

この Node サーバにブラウザ側からは次のようにメッセージの送受信が可能です。

```javascript
// ブラウザで実行する JavaScript
var ws = new WebSocket('ws://localhost:8080');
ws.addEventListener('open', function(event){
    console.log('WebSocket 接続完了');

    // サーバからメッセージを受け取ったときの処理
    ws.addEventListener('message',function(e){
        console.log("Message Recieved: " + e.data);
    });
    
    // サーバにデータを送信するときの処理
    ws.send("A message from browser");
});
```

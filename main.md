# はじめてのWebサーバ構築

## はじめに
みなさんが普段何気なくWebブラウザで見ているWebページ，一体どのように表示されているのでしょうか？
表示されて仕組みを説明できるようになっていただくのが本講座の目的です．何かわからないことがありましたら近くの講師に気軽に声をかけていただければと思います．

### Webページを構成するための技術
[第1回イベント](https://gdsc.community.dev/events/details/developer-student-clubs-national-institute-of-technology-kosen-kumamoto-college-presents-di-1hui-hazimetenowebtogit/)に参加された方は，なんとなく覚えているかもしれません．
- Webページはハイパーテキストを記述するための言語**HTML**によって書かれていること
- Webページの見栄えを**CSS**によって決めていること
- Webページの動きの部分を作る役割を担う言語として**JavaScript**がよく使われていること
Webページはこのような技術によって作られています．
### Webサーバとは
しかしWebページを作っても自分のコンピュータでしか表示できないのでは意味がありません．ほかのコンピュータからも見れるようにしたいですよね．そこで必要となるのが「Webサーバ」です．
Webブラウザからの要求があると，ネットワークを通して必要なコンテンツをWebブラウザに送信する役割をもつのが**Webサーバ**です．本講座ではWebサーバをRaspberry Piで動かすことをゴールとして進めていきます．

## Linuxをコマンドで操作しよう
世界中で稼働している多くのWebサーバはLinuxというOSをインストールしたコンピュータが使われています (TEやHIの皆さんが授業でTeraTermなどを使って接続しているサーバもLinuxです)．しかし皆さんが持っているノートパソコンのOSはWindowsかmacOSです (例外あり)．また今回のように自分の知らない技術を試す際はいつも使っている環境とは別の環境を用いることで気兼ねなく試すことができるというメリットがあります ．仮想マシンを皆さんのノートパソコンの中で動かすという方法もありますが今回は時間の制約もありますのでRaspberry Piを使うことにしました．LinuxはWindowsやmacOSと同じようにGUIで使うこともできますが，リモート接続して使用する場合はCUIで使うことが基本ですので，Linuxのコマンドを知る必要があります．この章ではサーバを動かすための最低限のLinuxコマンドを説明します．

### インターネットに接続しているか確認
Webサーバとして公開するためにはインターネットに接続している必要があります．まずは接続を確認しようと思います．
`ping`コマンドは，相手先ホストへの到達可能性を確認するために使用されます．`ping ホスト名`や`ping IPアドレス`と入力します (このままだと無限に出力し続けるため`-c 4`とつけて4回で終わるようにしています)．
```
ping -c 4 google.com
```
このコマンドを実行すると
```
pi@raspberrypi:~ $ ping -c 4 google.com
PING google.com (172.217.31.174) 56(84) bytes of data.
64 bytes from nrt12s22-in-f14.1e100.net (172.217.31.174): icmp_seq=1 ttl=118 time=19.3 ms
64 bytes from nrt12s22-in-f14.1e100.net (172.217.31.174): icmp_seq=2 ttl=118 time=21.2 ms
64 bytes from nrt12s22-in-f14.1e100.net (172.217.31.174): icmp_seq=3 ttl=118 time=141 ms
64 bytes from nrt12s22-in-f14.1e100.net (172.217.31.174): icmp_seq=4 ttl=118 time=19.8 ms

--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 19.336/50.415/141.307/52.480 ms
pi@raspberrypi:~ $
```
このように出力されたときGoogleのWebサーバと疎通が取れていますので，このRaspberry Piはインターネットに接続されていると考えてよいでしょう．

### 割り振られているIPアドレスを確認

#### IPアドレスとは
ネットワークに接続されているすべてのホストの中から，通信を行う宛先を識別するときに使用するのが，**IPアドレス**です．要するに「インターネットにおける住所」です．IPアドレスにはいくつかの種類があります．

#### `ip a`コマンド

### ユーザとファイルのアクセス権

#### ユーザとは
使用しているコンピュータのメモリやファイルなどの様々な資源を利用するために**ユーザ**という最小単位で権限を定義します．
では今Raspberry Piでは何のユーザでログインしているのでしょうか．
ターミナルを起動するとこのような文字が表示されると思います．
```
pi@raspberrypi:~ $
```
`pi`がユーザ名です．ちなみに`raspberrypi`はホスト名，このコンピュータの名前です (変更可能です)．

#### rootユーザ

#### `adduser`コマンド

#### `su`コマンド

#### `cat`コマンド

#### ファイルのアクセス権

#### `chmod`コマンド

### SSHしよう

#### SSHとは

#### `mkdir`コマンド

### まとめ
Linuxについてしっかりと理解したい方は，[Linux標準教科書](https://linuc.org/textbooks/linux/)が無料で読めるのでおすすめです．もっといろいろなことを知りたい方はマサチューセッツ工科大学で行われているコンピュータサイエンスの授業の準備となるシェルやVim/Git/デバッグなどの便利なツールについて知ることができる[The Missing Semester of Your CS Educationの日本語版 (有志が作成)](https://missing-semester-jp.github.io/) なども面白いかもしれません．

## 実際にWebサーバを動かそう

### `index.html`をほかの人にも見てもらいたい

### Webサーバについて

#### `apt`コマンド

#### Nginxのインストール

### `index.html`を配置

#### `wget`コマンド
```
wget https://raw.githubusercontent.com/gdsc-nitk/hands-on/main/index.html
```

#### ファイルを配置する場所を検討

### まとめ

## 終わりに
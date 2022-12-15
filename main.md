# はじめてのWebサーバ構築

## はじめに
みなさんが普段何気なくWebブラウザで見ているWebページ，一体どのように表示されているのでしょうか？
表示されて仕組みを説明できるようになっていただくのが本講座の目的です．何かわからないことがありましたら近くの Core-Member に気軽に声をかけていただければと思います．

### Webページを構成するための技術
[第1回イベント](https://gdsc.community.dev/events/details/developer-student-clubs-national-institute-of-technology-kosen-kumamoto-college-presents-di-1hui-hazimetenowebtogit/)に参加された方は，なんとなく覚えているかもしれません．
- Webページはハイパーテキストを記述するための言語**HTML**によって書かれていること
- Webページの見栄えを**CSS**によって決めていること
- Webページの動きの部分を作る役割を担う言語として**JavaScript**がよく使われていること
Webページはこのような技術によって作られています．
### Webサーバとは
しかしWebページを作っても自分のコンピュータでしか表示できないのでは意味がありません．ほかのコンピュータからも見れるようにしたいですよね．そこで必要となるのが**Webサーバ**です．
Webサーバは，Webブラウザからの要求があると，ネットワークを通して必要なコンテンツをWebブラウザに送信する役割をもつのです．本講座ではWebサーバをRaspberry Piで動かすことをゴールとして進めていきます．

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
皆さんはChromeなどのブラウザのアドレスバーに`google.com`と入力すると思います．ではWebサーバを公開してから，ほかの人はどのようにアドレスバーに入力してあなたのWebサーバにアクセスするのでしょうか．そこで必要となるのが**IPアドレス**です．

#### IPアドレスとは
そもそもIPアドレスとは一体何なのでしょうか．IPアドレスとは，ネットワークに接続されているすべてのホストの中から，通信を行うときの発送元と発送先の場所を表すものです．要するに「インターネットにおける住所」です．IPアドレスにはいくつかの種類があります．
- **プライベートIPアドレス**
ローカルなネットワーク (外部から利用できない社内LAN/学内LANなど) のアドレスとして使うために予約されたIPアドレス
- **グローバルIPアドレス**
インターネットに接続されているコンピュータや通信機器を個々に特定するための一意で割り当てられたIPアドレス
今回はこちらで用意したローカルなネットワークに皆さんのRaspberry Piを接続しています．今からそれぞれのRaspberry Piに割り当てられたプライベートIPアドレスを確認していきます．グローバルIPアドレスが割り当てられていないとインターネットに接続できないのではという疑問を持った方はぜひ**NAT**について調べてみてください．

#### `ip`コマンド
IPアドレスの確認は`ip`コマンドを使います．以下のように入力します．
```
ip a
```
このコマンドを実行すると以下のような出力になると思います．
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast state DOWN group default qlen 1000
    link/ether b8:27:eb:ea:77:63 brd ff:ff:ff:ff:ff:ff
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether b8:27:eb:bf:22:36 brd ff:ff:ff:ff:ff:ff
    inet 192.168.10.105/24 brd 192.168.10.255 scope global dynamic noprefixroute wlan0
       valid_lft 86336sec preferred_lft 75536sec
    inet6 fe80::c76d:ed48:fa20:71cf/64 scope link
       valid_lft forever preferred_lft forever
```
色々表示されていて訳がわからないと思います．次の節で細かく見ていきましょう．

####  ネットワークインタフェースとは
ネットワークへアクセスするためにネットワークインターフェースが必要です．わかりやすい例だとLANポートがあります．先ほど実行した`ip a`コマンドではラズパイが認識しているネットワークインターフェースをすべて表示します．今回の環境では以下のネットワークインターフェースが表示されると思います．
| 表示名  | 説明                         |
| ------- | ---------------------------- |
| `lo`    | ループバックインターフェース |
| `eth0`  | 有線接続用のインターフェース |
| `wlan0` | 無線接続用のインターフェース |

##### ループバックインターフェースとは
機器が正常に稼働しているか確認するためにデータを送って試すループバックテストなどに利用されます．今回はあまり重要はないので，理解していなくても問題ありません．

#### あなたのRaspberry PiのIPアドレスを確認しよう
というわけで自分のIPアドレスは確認できましたか？このあとの節でそのアドレスは使用しますので，メモアプリなどに控えておきましょう．わからない人へのヒントとして，今回Raspberry Piはネットワークに無線接続しています．それでもわからない場合は Core-Member に聞いてみてください．

### ユーザとファイルのアクセス権

#### ユーザとは
使用しているコンピュータのメモリやファイルなどの様々な資源を利用するために**ユーザ**という最小単位で権限を定義します．
では今Raspberry Piではどのユーザでログインしているのでしょうか．
ターミナルを起動するとこのような文字が表示されると思います．
```
pi@raspberrypi:~ $
```
`@`より前がユーザ名ですので`pi`ユーザであることがわかります (ちなみに`raspberrypi`はホスト名，すなわちこのコンピュータの名前です．これはRaspberry Pi OSインストール時のデフォルト設定でこのようになっているだけなので変更可能です) ．

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
LinuxやLinuxコマンドについてしっかりと理解したい方は，[Linux標準教科書](https://linuc.org/textbooks/linux/)が無料で読めるのでおすすめです．もっといろいろなことを知りたい方はマサチューセッツ工科大学で行われているコンピュータサイエンスの授業の準備となるシェルやVim/Git/デバッグなどの便利なツールについて知ることができる[The Missing Semester of Your CS Educationの日本語版 (有志が作成)](https://missing-semester-jp.github.io/) なども面白いかもしれません．

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
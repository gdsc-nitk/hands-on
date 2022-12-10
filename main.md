# はじめてのWebサーバ構築

## はじめに
みなさんが普段何気なくWebブラウザで見ているWebページ，一体どのように表示されているのでしょうか？
表示されて仕組みを説明できるようになっていただくのが本講座の目的です．何かわからないことがありましたら近くの講師に気軽に声をかけていただければと思います．

### Webページを構成するための技術
[第1回イベント](https://gdsc.community.dev/events/details/developer-student-clubs-national-institute-of-technology-kosen-kumamoto-college-presents-di-1hui-hazimetenowebtogit/)に参加された方は，なんとなく覚えているかもしれません．
- Webページはハイパーテキストを記述するための言語**HTML**によって書かれていること
- Webページの見栄えを**CSS**によって決めていること
- Webページの動きの部分を作る役割を担う言語として**JavaScript**がよく使われていること

### Webサーバとは
Webブラウザからの要求があると，ネットワークを通して必要なコンテンツをWebブラウザに送信する役割をもつのが**Webサーバ**です．

## Linuxをコマンドで操作しよう

### コマンドで操作するとは一体何なのか
コマンドの入力を受け付けて，そのコマンドを実行し，入力したユーザに対しその結果を返す役割をもつのが**シェル**です．

### インターネットに接続しているか確認
`ping`コマンドは，ネットワークの疎通（繋がっているか）を確認するために使用されます．
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

### 割り振られているIPアドレスを確認

#### IPアドレスとは

#### `ip a`コマンド

### ユーザとファイルのアクセス権

#### ユーザとは
使用しているコンピュータのメモリやファイルなどの様々な資源を利用するために**ユーザ**という最小単位で権限を定義します．
では今Raspberry Piでは何のユーザでログインしているのでしょうか．
ターミナルを起動するとこのような文字が表示されると思います．
```
pi@raspberrypi:~ $
```
`pi`がユーザ名です．ちなみに`raspberrypi`はホスト名，このコンピュータの名前です（変更可能です）．

### まとめ

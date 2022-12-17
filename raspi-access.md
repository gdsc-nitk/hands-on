## Raspberry Piにリモート接続しよう
普段パソコンを操作するときはマウスなどで操作することがほとんどだと思います．  
しかしサーバは基本的にリモートでアクセスしてコマンドだけで操作することがほとんどです．  
この章では実際にRaspberry Piにリモートでアクセスしてみます．

### IPアドレスを調べる
リモートで接続するとき，全員が同じネットワークにRaspberry Piを接続しているので，どのようにして自分の使っているRaspberry Piを区別すればよいでしょうか．  
そのときに必要となってくるのが**IPアドレス**です．IPアドレスは「ネットワークの中での住所」であり，重複しないようになっています．  
自分のRaspberry Piに割り当てられているIPアドレスを調べる際は`ip a`コマンドを使います．  

1. 以下のコマンドをRaspberry Piのターミナルアプリケーションで実行してください．
```
ip a
```

2. 出力された文字列の中から，以下に該当する行を探します．
```
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether b8:27:eb:bf:22:36 brd ff:ff:ff:ff:ff:ff
    inet 192.168.10.105/24 brd 192.168.10.255 scope global dynamic noprefixroute wlan0
```

`3: wlan0`という項目の`inet`のあとに，`XXX.XXX.XXX.XXX/24`といった形式の数字があると思います．  
それがあなたのRaspberry PiのIPアドレスです．

### 疎通を確認
IPアドレスが割り当てられているということは，ネットワークに接続されているということですが，  
自分のノートパソコンから本当にRaspberry Piに対して通信が行えるかを確認してみます．  
相手先のコンピュータへの到達可能性を確認する際には`ping`コマンドを使用します．  
`ping {ホスト名}`や`ping {IPアドレス}`と入力します． 

1. 自分のノートパソコンが`knct:wireless`ではなく`準備中`のWi-Fiに接続しているか確認します．

2. Windowsを使用している方はPowerShell，macOS/Linuxを使用している方はターミナルアプリケーションを起動してください．

3. 以下のコマンドを実行します．  
macOS/Linuxの方は4行程度出力されたら`Ctrl`キーを押しながら`C`を押してください． 
また`{ `や` }`は不要です．
```
ping {Raspberry PiのIPアドレス}
```
4. 以下のような出力になった場合，失敗していますので以下のことを確認してください．
- `ping {IPアドレス}`で正しいIPアドレスを入力していますか．
- `ip a`コマンドを実行して，自分のRaspberry Piに割り当てられているIPアドレスを正しく読み取りましたか．

それでもうまくいかない場合は近くの Core Member に質問していただければと思います．

#### Windowsの場合
```
PS C:\Users\hi18iwano> ping {Raspberry PiのIPアドレス}

{Raspberry PiのIPアドレス} に ping を送信しています 32 バイトのデータ:
{自分のノートパソコンのIPアドレス} からの応答: 宛先ホストに到達できません。
{自分のノートパソコンのIPアドレス} からの応答: 宛先ホストに到達できません。
{自分のノートパソコンのIPアドレス} からの応答: 宛先ホストに到達できません。
{自分のノートパソコンのIPアドレス} からの応答: 宛先ホストに到達できません。

{Raspberry PiのIPアドレス} の ping 統計:
    パケット数: 送信 = 4、受信 = 4、損失 = 0 (0% の損失)、
PS C:\Users\hi18iwano>
```

#### macOSの場合
```
hi18iwano@MacBook ~ % ping {Raspberry Piのアドレス}
PING {Raspberry Piのアドレス} ({Raspberry Piのアドレス}): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1
Request timeout for icmp_seq 2
Request timeout for icmp_seq 3
^C
--- {Raspberry Piのアドレス} ping statistics ---
5 packets transmitted, 0 packets received, 100.0% packet loss
hi18iwano@MacBook ~ % 
```

### リモート接続しよう
自分のRaspberry PiのIPアドレスを確認できましたので，実際にリモート接続を行います．  
以下のコマンドを実行してください．
```
ssh pi@{Raspberry Piのアドレス}
```

実行すると以下のように出力されますので，`yes`と入力します．
```
The authenticity of host '{Raspberry Piのアドレス} ({Raspberry Piのアドレス})' can't be established.
ECDSA key fingerprint is SHA256:HDwDGDI9Bs4TT8YSAggTw9efiel5CgRqKZtPlsQxaE8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
```
そしてパスワードを入力します．  
以下のように表示されたらリモート接続完了です．
```
Linux raspberrypi 5.15.61-v7+ #1579 SMP Fri Aug 26 11:10:59 BST 2022 armv7l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Sun Dec 11 12:15:39 2022
pi@raspberrypi:~ $
```
この章はこれで終わりです．次の章では実際にWebサーバを動かしてみます．  
[次のページ](web-server.md)
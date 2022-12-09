# オプション講座 - セキュリティコース

## はじめに

本講座では，基礎講座で製作したWebサーバをよりセキュアにするためにはどうするとよいかを示します．

## パッケージの更新・自動化

### ソフトウェアのアップデート

基礎講座でWebサーバ"Nginx"をインストールして用いたように，OSの中では様々なソフトウェアが動作しています．  
これらのソフトウェアは，単なる機能追加・改善のほか，脆弱性に対処するためなどの目的で日々新たなバージョンが公開されます．  
まずは実際にアップデートをかけてみましょう．

1. はじめに，各ソフトウェアについて最新の情報を取得します．

```
sudo apt update
```

2. 1.で得た情報をもとに，新たなバージョンが配信されているソフトウェアをアップデートします．  
初回あるいは久しぶりに実行する場合，たくさんのソフトウェアについて更新が行われるため相応の時間を要します．

```
sudo apt upgrade -y
```

これでアップデートが完了しました．

### アップデートの自動化

既知の脆弱性を悪用されないためには，できるだけ速やかにアップデートを適用する必要があります．  
しかし，サーバ管理者が24時間365日常に見張り続けることは現実的ではありません．  
そこで，アップデートを自動的に実施するように設定してみましょう．

1. まずは自動アップデート用のパッケージをインストールします．

```
sudo apt install unattended-upgrades -y
```

2. Raspberry Pi 用の設定に書き換えます．  
以下のコマンドで，設定ファイルをnanoというエディタを使って開きます．  
(ご存じの方は，vi/vim/emacs/edなどをご利用いただいても構いません．)

```
sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```

こういった行がありますので，
```
//      "origin=Debian,codename=${distro_codename}-updates";
//      "origin=Debian,codename=${distro_codename}-proposed-updates";
        "origin=Debian,codename=${distro_codename},label=Debian";
        "origin=Debian,codename=${distro_codename},label=Debian-Security";
        "origin=Debian,codename=${distro_codename}-security,label=Debian-Security";
```
以下のように書き換えてください．
```
//      "origin=Debian,codename=${distro_codename}-updates";
//      "origin=Debian,codename=${distro_codename}-proposed-updates";
//      "origin=Debian,codename=${distro_codename},label=Debian";
//      "origin=Debian,codename=${distro_codename},label=Debian-Security";
//      "origin=Debian,codename=${distro_codename}-security,label=Debian-Security";
        "o=*,a=*";
```
編集を終えたら，`Ctrl`キーを押しながら`X`を押します．  
すると保存するのかと聞かれますので，`Y`を押して`Enter`キーを押してください．  
これでnanoエディタが終了し，もとのシェルの画面に戻ったはずです．

以上で自動アップデートの設定は終了です．

#### 補足

ソフトウェアをアップデートすると，何らかの事情でシステムがうまく動作しなくなることも稀にあります．  
よって，手動でのアップデート前に悪意のあるユーザからゼロデイ攻撃を受けるリスクと，
自動アップデート時に何らかの不具合が発生して正常な動作を停止するリスクを天秤にかけて比較検討する必要があります．

例えば，金融系・医療系などのミッションクリティカルなシステムの場合，どんな事情であれ停止することは許されません．  
アップデートの前に試験環境で動作を確認し，問題がなかった場合に本番環境へ手動でアップデートを適用するといった運用が想定されます．  
動作を確認するためにアップデートの適用が遅れますので，その分を他の対策によって攻撃から防御できるように設計されています．

一方で，我々一般ユーザが使用するシステムの場合，バージョンアップが提供されるたびに逐一試験環境で動作を確認することは現実的ではありません．  
よって自動アップデートを有効にしますが，その代わり万が一アップデート時に不具合が発生したときのため，定期的にバックアップをとっておくことが大変重要となります．

参考：「[3-2-1バックアップ](https://gigazine.net/news/20211129-data-survive-3-2-1-backup-rule/)」

## SSHポートの変更

### ポートとは
ポートの説明，well-known port

### sshdの設定
/etc/ssh/sshd_config  
他の設定箇所を変更することでよりセキュアに

## ファイアウォールの利用

### ファイアウォールとは
概要

### ufwの設定
80, 22(あるいは変更後のもの)

### ufwの起動
start, enable
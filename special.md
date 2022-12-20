# 応用講座

## はじめに

本講座では，予め用意した全てのコンテンツを終了した方向けの情報を記載します． 

なお，Raspberry Piは通常のコンピュータと比べると非常に性能が低いです．  
ものによってはインストールに非常に時間がかかったり，正常動作しないことも考えられます．  
期待通りに動かない場合など，ぜひ遠慮なく近くの Core-Member にお声掛けください．

## 注意

**[ネットワークコース](opt-network.md)を修了し，ngrokを有効化している方へ**  
`sudo reboot`を実行してOSごと再起動し，ngrokサービスを確実に停止してください．

**[セキュリティコース](opt-security.md)を修了し，ufwを有効化している方へ**  
随時必要なポートを開放するか，`sudo ufw disable`を実行して一時的にファイアウォールを停止してください．  

## コンテンツ
以下に掲載している各コンテンツは，それぞれ独立しています．  
順番もありませんので，興味のあるものから試してみてください．

### (a) WordPressの利用 (on Raspberry Pi)

世界中で公開されているWebサイトの約43%は，「WordPress」というCMSを用いて制作されています．  
([熊本高専のWebサイト](https://kumamoto-nct.ac.jp)や[K-Pass](https://k-pass.net)，[電波祭Webサイト](http://denpasai.com)などもWordPressを利用しています．)

これを，Raspberry Pi上に構築してみましょう．  
php，MySQL(or MariaDB)で作られています．

例) https://www.ingenious.jp/articles/howto/raspberry-pi-howto/wordpress-server-setup/

### (b) クラウドサービスの利用 (on Your PC)

Googleが提供するパブリッククラウド「Google Cloud Platform」を使ってみましょう．  
たくさんのサービスが提供されていますが，このうち**Compute Engine**を使用すると，クラウド上に任意のサーバを構築できます．

なお，課金が発生する可能性もあります．  
ページに記載の内容をしっかり読んで，不安なときは近くのCore Membersにお声掛けくださいね．  
(各々の責任でお試しください．)

例) https://qiita.com/Brutus/items/22dfd31a681b67837a74

### (c) ハイパーバイザ型仮想化技術の利用 (on Your PC)

自身の所有するPCの中に，仮想的にサーバを構築してみましょう．  

以下に大まかな手順を示します．  
詰まったときはまずGoogleなどで検索して，5分ほど調べても求める情報が得られなかったら近くのCore Memberに声をかけてください．

制御情報システム工学科に所属する方は，すでに導入されているかもしれません．  

**(注)**  
メモリ8GB以下，ストレージ(HDD/SSD)の空き容量32GB以下の場合は動作しない可能性があります．  
当てはまる場合は，下にある **(d) コンテナ型仮想化技術の利用**  に進んでください．  

1. 仮想化ソフトウェアの導入  
Windows 10/11 Home：[VirtualBox](https://www.virtualbox.org/wiki/Downloads)  
Windows 10/11 Pro/Edu/Enterprise：[Hyper-V](https://4thsight.xyz/26358)  
Intel Mac：[VMware Fusion](https://aireblog.com/vmware-fusion-download-free-license/)  
M1/M2 Mac：[VirtualBox](https://www.virtualbox.org/wiki/Downloads) (Developer preview for macOS / Arm64 (M1/M2) hosts)  

2. OSイメージ(ISO)の入手  
今回は，サーバOSとして世界シェアNo.1のUbuntuを利用します．  
[Ubuntu](https://jp.ubuntu.com/download#:~:text=22.10%20release%20notes-,Ubuntu%20Server,-%E3%82%B7%E3%83%B3%E3%83%97%E3%83%AB%E3%81%AA%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB)を開き，下部にある **Ubuntu Server 22.04.1 LTS** をダウンロードしてください．  
ファイルサイズは1.4GBです．

3. OSのインストール  
インストールした仮想化ソフトウェアを開き，手順に従ってOSのインストールを進めてください．  

4. SSHの利用，Webサーバのセットアップ，etc.  
[メイン講座・オプション講座](README.md)の手順に従って，利用できるか試してみてください．

### (d) コンテナ型仮想化技術の利用 (on Your PC)

サーバOSの仕組みを学ぶには，実機と同じように構成されたハイパーバイザ型仮想化を利用することが望ましいです．  
一方で，手軽にサーバ周りのソフトウェアを試したいという状況においては，コンテナ型仮想化が適しています．  

詳しい仕組みについては，[こちら](https://www.itmedia.co.jp/enterprise/articles/1612/19/news041.html)を参照してください．

ここでは，Dockerを利用します．  
以下にドキュメントを示しますので，頑張って挑戦してみてください．

[Windows](https://docs.docker.com/desktop/install/windows-install/)  
[Mac](https://docs.docker.com/desktop/install/mac-install/)

インストールを終えたら，試しにNginxイメージを利用してみることにします．

1. Nginxイメージを取得します．
```
docker pull nginx
```

2. 数十秒ほど待機します．

3. Nginxイメージを，"nginx"という名前で起動します． 
このとき，コンテナの80番ポートを端末の8080番ポートに転送します．
```
docker run -p 8080:80 --name nginx nginx
```

4. 普段使用しているブラウザを開き，`http://localhost:8080`にアクセスしてください．  
`Welcome to Nginx!` と書かれたテストページが表示されれば，正しく動作しています．

### **(おまけ)** CUIで用いる便利なソフトウェアの紹介
著者が個人的に使用しているソフトウェアのうち，広くおすすめできるものを以下に紹介します．  
いずれも，`apt install ~~~~`でインストールすることができます．  
ただし，各ソフトウェアの正常性を保証するものではありません．各々の責任で調査し，ご利用ください．

#### 実用的なもの
- **fish**  
コマンドの補完機能などが優秀な，大変使いやすいシェル
- **bat**  
catにシンタックスハイライトをプラス
- **exa**  
lsの進化版
- **tree**  
フォルダ構造を容易に可視化
- **ripgrep**  
grepの進化版
- **htop**  
topの進化版
- **dog**  
dig(nslookup)の進化版
- **fd**  
findの進化版
- **tldr**  
各コマンドの使用例を表示
- **iperf3**  
帯域測定に利用
- **ffmpeg**  
映像/音声ファイルの変換，編集，配信
- **byobu**  
tmuxをかんたんに．

#### 実用的(?)なもの
- **asciiquarium**  
いつでもどこでも水族館
- **cowsay**  
牛がしゃべる
- **nyancat**  
もはやスクリーンセーバー
- **figlet**  
アスキーコードジェネレーター

## おわりに

今回の演習，お楽しみいただけましたでしょうか．  

もし本日尋ねられなかったことがありましたら，GDSC熊本高専チャプターのTeamsやDiscordなどでいつでもお問い合わせください．  

みなさんがより広く深い知識や技能を身に着け，さらに高いところへ羽ばたいてゆけることを願っています．
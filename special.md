# 応用講座

## はじめに

本講座では，予め用意した全てのコンテンツを終了した方向けのの情報を記載します． 

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

### WordPressの利用

世界中で公開されているWebサイトの約43%は，「WordPress」というCMSを用いて制作されています．  
([熊本高専のWebサイト](https://kumamoto-nct.ac.jp)や[K-Pass](https://k-pass.net)，[電波祭Webサイト](https://denpasai.com)などもWordPressです．)

これを，Raspberry Pi上に構築してみましょう．  
php，MySQL(or MariaDB)で作られています．

例) https://www.ingenious.jp/articles/howto/raspberry-pi-howto/wordpress-server-setup/

### クラウドサービスの利用

Googleが提供するパブリッククラウド「Google Cloud Platform」を使ってみましょう．  
たくさんのサービスが提供されていますが，このうち**Compute Engine**を使用すると，クラウド上に任意のサーバを構築できます．

なお，課金が発生する可能性もあります．  
ページに記載の内容をしっかり読んで，不安なときは近くのCore Membersにお声掛けくださいね．  
(各々の責任でお試しください．)

例) https://qiita.com/Brutus/items/22dfd31a681b67837a74

### (現在作成中...)

## おわりに

<!-- 
締めの言葉 
　+
本ページに記載の内容を終えた学生が，講座終了後さらに学習を進められるようなコンテンツを提示
-->
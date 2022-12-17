## Webサーバを構築しよう
Webサーバとは，Webブラウザからの要求があると，ネットワークを通して必要なコンテンツをWebブラウザに送信する役割を持ちます．  
WebサーバのアプリケーションをRaspberry Piにインストールして実際に自分のノートパソコンのブラウザからWebページが見ることができるようにします．


### ソースのダウンロード
まずは表示するHTMLファイルを用意します．こちらで用意したものがありますので，以下のコマンドを実行して取得してください．

```
wget https://raw.githubusercontent.com/gdsc-nitk/hands-on/main/index.html
```

### Webページを構成する技術
ここではWebページはどのように作られているか簡単に解説します．  
[第1回のGDSCイベント](https://gdsc.community.dev/e/mpsaja/)に参加した方や4,5年生は知っている内容も含まれると思いますので，読み飛ばしていただいてかまいません．

### Webサーバのインストール

```
sudo cp index.html /var/www/html/
```

[次のページ](final.md)
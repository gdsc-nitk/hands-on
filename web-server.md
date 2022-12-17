## Webサーバを構築しよう
みなさんがWebページを開いた時，ブラウザはWebサーバに要求を送ります．  
Webサーバはこれを受けて，ページを表示するためのファイルを送信します．  
実際にRaspberry PiをWebサーバにしてみましょう．  
  
[前のページ](raspi-access.md)でRaspberry Piにリモートでアクセスできるようになっていることが前提で話を進めます．  
以降は，Raspberry Pi直結のキーボードではなくご自身のノートパソコンで入力してください．  
先ほど使用したPowerShellもしくはターミナルを用いて，ネットワーク越しにRaspberry Piをリモートで操作します．  

### ソースのダウンロード
まずは表示するHTMLファイルを用意します．こちらで用意したものがありますので，以下のコマンドを実行してHTMLファイルをダウンロードしてください．

```
wget https://raw.githubusercontent.com/gdsc-nitk/hands-on/main/index.html
```
`ls`コマンドを実行して`index.html`があるかどうか確認します．

### Webページを構成する技術
ここではWebページはどのように作られているか簡単に解説します．  
[第1回のGDSCイベント](https://gdsc.community.dev/e/mpsaja/)に参加した方や4,5年生は知っている内容も含まれると思いますので，読み飛ばしていただいてもかまいません．  
  
[**Webページ**](https://developer.mozilla.org/ja/docs/Learn/Common_questions/Pages_sites_servers_and_search_engines)はブラウザで表示することができる簡単な文書です．  
文書は [**HTML**](https://developer.mozilla.org/ja/docs/Glossary/HTML) 言語で書かれています．  
HTML関連する他の技術として，Webページの表示や表現を記述するための [**CSS**](https://developer.mozilla.org/ja/docs/Web/CSS) ，機能や振る舞いを記述する [JavaScript](https://developer.mozilla.org/ja/docs/Web/JavaScript) があります．


### Webサーバのインストール
Webサーバのソフトウェアはいくつか種類がありますが，その中でもよく使われている**Nginx**を今回は使用します．    
インストールには，ソフトウェアを管理する`apt`というコマンドを使用します．  

1. まずは`apt`でインストール可能なソフトウェアの最新情報を取得します．

```
sudo apt update
```

2. Nginxをインストールします．

```
sudo apt install nginx -y
```

3. このコマンドを実行すると，インストールと同時にNginxが自動的に開始されます．  
以下のコマンドでNginxが動いているか確認します．

```
systemctl status nginx
```

以下のように`Active: active (running)`と出力されれば正しく動作しています．
```
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2022-12-17 17:24:38 JST; 10min ago
```

4. 先ほどダウンロードした`index.html`を所定の位置に配置します．

```
sudo cp index.html /var/www/html/
```

### ブラウザで実際にアクセスしてみる
以上でWebサーバを立ち上げることができました．  
普段使用しているブラウザを開き，アドレスバーにRaspberry PiのIPアドレスを入力してみてください．  
すごそうなWebページが表示されていれば，正しく動作しています．  
  
[次のページ](final.md)
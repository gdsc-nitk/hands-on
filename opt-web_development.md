# オプション講座 - Web開発コース

## はじめに

本講座では，基礎講座で製作したWebサーバにおいてWeb開発を行う方法を示します.  
To DoリストWebアプリを作成します．制作物を<a href="https://gdsc-nitk.github.io/hands-on/web-dev-project/" target="_blank">こちら</a>から参考にしてください．

まずは，サンプルプログラムを手元のWebサーバにダウンロードしましょう．
```
cd /var/www/html
sudo mkdir todo
cd todo
sudo wget https://raw.githubusercontent.com/gdsc-nitk/hands-on/main/web-dev-project/index.html
sudo wget https://raw.githubusercontent.com/gdsc-nitk/hands-on/main/web-dev-project/style.css
sudo wget https://raw.githubusercontent.com/gdsc-nitk/hands-on/main/web-dev-project/script.js
```

ブラウザで`http://{Raspberry PiのIPアドレス}/todo/index.html`を開ければOKです．

ソースファイルと以下資料とを見比べるか，
```
cat index.html
cat style.css
cat script.js
```
実際に編集しながら確認してみてください．
```
sudo nano index.html
sudo nano style.css
sudo nano script.js
```

## 内容
- [HTML](#html)  
  - [HTMLの構成](#htmlの構成)
  - [HTMLのタグまとめ](#htmlのタグ)
- [CSS](#css)
  - [CSSの構成](#cssの構成)
  - [CSSを適用する方法](#cssを適用する方法)
  - [CSSの例](#cssの例)
- [JavaScript](#javascript)
  - [JavaScriptを適用する方法](#javascriptを適用する方法)
  - [JavaScriptの基礎](#javascriptの基礎)

## HTML
HyperText Markup Languageの略であり，Webページの構成を決めるために用いられます．
### HTMLの構成
HTMLは，基本的に以下の4つの要素（以下タグ）で構成されています．
```
<!-- DOCTYPEはファイルがhtmlであるということを示す宣言 -->
<!DOCTYPE html> 

<!-- htmlタグの中に書かれているものがhtmlのコードだと判断 -->
<html>

    <head>
      <!-- 実際のページには表示されないHTML自身に関する情報 -->
    </head>

    <body>
      <!-- 実際に見える部分，ページのコンテンツの情報 -->
    <body>

</html>
```

### HTMLのタグ  
以下に普段使われるHTMLタグを示します．
```
<!DOCTYPE html> 
<html>

  <!-- 実際のページには表示されないHTML自身に関する情報 -->
  <head>
      
      <!-- ページの文字コードがutf-8である -->　
      <meta charset="UTF-8"> 

      <!-- ページのタイトル -->
      <title>Document</title>

  </head>

  <!-- 実際に見える部分，ページのコンテンツの情報 -->
  <body> 

      <!-- 見出しタグ -->
      <h1>見出し１</h1>
      <h2>見出し２</h2>
      ⋮
      <h6>見出し６</h6>

      <!-- パラグラフタグ -->
      <p>GDSCのイベントの参加していただき，ありがとうございます！</p>

      <!-- ハイパーリンクタグ -->
      <a href="他ページへのURL">表示するテキスト</a>
      
      <!-- 画像タグ -->
      <img src="画像のリンク" alt="画像の代替テキスト" />

      <!-- リストタグ（ul: unordered list） -->
      <ul>
        <li>アイテム１</li>
        <li>アイテム２</li>
        <li>アイテム３</li>
      </ul>

      <!-- リストタグ（ol: ordered list） -->
      <ol>
        <li>アイテム１</li>
        <li>アイテム２</li>
        <li>アイテム３</li>
      </ol>

      <!-- 要素をグループ化するタグ -->
      <div>
        <h1>GDSCとは</h1>
        <p>
          <a href="https://developers.google.com/community/gdsc" target="_blank">
          Google Developer Student Clubs（GDSC）
          </a>プログラムは，Google のテクノロジーに関心のある学生向けのコミュニティです．
        </p>
      </div>
  </body>
</html>
```

## CSS
HTMLで表現するタグを，どのように装飾するかを決める役割を果たします．

### CSSの構成
```
タグ {
  スタイル: 値;
}

.クラス名 {
  スタイル: 値;
}

#id名 {
  スタイル: 値;
}
```

### CSSを適用する方法

1. `<style>`要素で文書単位に適用する
```
<html>
  <head>
    <style>
      body {
        background-color: red;
      }
    <style>
  <head>

  <body>
  <body>
</html>
```

2. 要素にstyle属性を追加して局所的に適用する
```
<body>
  <p style="color:blue;">文章</p>
</body>
```

3. HTMLの`<link>`タグで外部 .CSSファイル を呼び出して適用する
```
<html>
  <head>
    <link rel="stylesheet" src="cssファイルへのリンク">
  <head>

  <body>
  <body>
</html>
```  

### CSSの例

```
body {
  margin: 0;                /* 隣り合った要素（兄弟間）の余白はmargin */
  padding: 0;               /* 親要素と子要素の間（親子間）の余白はpadding */
  background-color: red;    /* バックグラウンドの色 */
  font-size: 20px;          /* フォントのサイズ */
  font-family: sans-serif;  /* フォントの種類 */
  height: 100%;             /* 縦幅 */
  width: 70vh;              /* 横幅 */
  color: rgb(255, 0, 0);    /* フォントの色 */
}

a {
  text-decoration: underline;       /* テキストに下線 */
  transform: translate(50%, 50%);   /* 水平方向や垂直方向に移動 */
}

div {
  text-align: center;     /* 中央寄せ */
}
```

## JavaScript
アニメーションや情報のやりとりなどを実装するために用いられます．

### JavaScriptを適用する方法

1. `<script>`要素で文書単位に適用する
```
<script>  //head内やbody内の最下部に記す
  console.log("Hello, World!")  // メッセージをウェブコンソールに出力する
</script>
```

2. `<script>`タグで外部 .jsファイル を呼び出して適用する
```
<script src="main.js"></script>
```

### JavaScriptの基礎
ゲーム，ボタンを押したときの反応，フォームへのデータ入力，動的なスタイル付け，アニメーション，HTMLの内容を更新など様々なことができます．
```
const myHeading = document.querySelector('h1');   // 見出しタグをmyHeading変数に格納
myHeading.textContent = 'Hello world!';           // 見出しの内容を更新

// 見出しをクリックすると，通知が表示される
document.querySelector('h1').addEventListener('click', function () {
  alert('痛っ! つつかないで!');
}); 

// if elseの使い方
if (hour < 18) {
  greeting = "こんにちは！";
} else {
  greeting = "こんばんは！";
}

// for文の使い方
const webLangs = ["HTML", "CSS", "JavaScript"];
for (let i = 0; i < webLangs.length; i++) {
  document.write(webLangs[i]);
}
```
## おわりに

<!-- 
締めの言葉 
　+
本ページに記載の内容を終えた学生が，講座終了後さらに学習を進められるようなコンテンツを提示
-->

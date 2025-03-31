# PHPの書き方⑤

PHPには以下の2種類の関数があります。

1. 組み込み関数　・・・　プログラム言語としてPHPであらかじめ用意されている関数
1. ユーザー定義関数　・・・　ユーザー（プログラマー）が自分で作成する関数

## ユーザー定義関数

ユーザー定義関数とは、ユーザー（プログラマー）自身が作成する関数です。
ユーザー定義関数の基本文法は以下のとおりです。

```php
function  関数名 ( 引数リスト ) {
    具体的な処理を記述
    return  戻り値; // 戻り値がある場合（なければ記述不要）
}
```

戻り値がない関数

```php
function  func1 ( $a, $b ) { // func1( )関数を呼び出すだけで計算結果を表示する
    echo  $a . ' + ' . $b . ' = ' . ( $a + $b );
}
```

戻り値がある関数

```php
function  func2 ( $a, $b ) { // func2( )関数を呼び出すと計算結果が戻り値として返ってくる
    return  $a + $b;
}
```

【使用例】

```php
<?php

// 関数func1( )の定義
function  func1 ( $a, $b ) {
    echo  $a . ' + ' . $b . ' = ' . ( $a + $b );
}

// 関数func2( )の定義 
function  func2 ( $a, $b ) {
    return  $a + $b;
}

$a = 10; $b = 25;
// 関数func1( )を呼び出す
func1( $a, $b); // 10 + 25 = 35　が計算され「35」が表示される

// 関数func2( )を呼び出す
$c = func2($a, $b); // $c に戻り値である「35」 が代入される
echo  $a . ' + ' . $b . ' = ' . $c; // 「10 + 25 = 35」と表示される
?>
```

「組み込み関数」の`htmlspecialchars`にて、実際のWebアプリケーション作成時には、送信されてきたデータをブラウザに表示する場合にはセキュリティ対策として必ず実行すると紹介しました。

しかし、関数が長いので、記述するのが面倒という欠点があります。
そのような場合、以下のように、この関数をユーザー定義関数として簡略化することで、欠点を補う方法がとられます。

```php
<?php

function  h ( $data ) { // 関数h を定義
    return  htmlspecialchars ( $data,  ENT_QUOTES,  "UTF-8"); 
}

echo  h ( $_POST['name'] ); // 関数hを実行、つまりhtmlspecialschars( )関数を実行

?>
```

## エスケープ処理のサンプルコード

ここからは、エスケープ処理を通して、組み込み関数(`htmlspecialchars`)とユーザー定義関数を実装します。

### エスケープ処理なしの場合

1. `public`ディレクトリに、`unescape.html` と `unescape.php` を作成してください。<br>

`unescape.html`

```php
<!DOCTYPE html>
<html lang="ja">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>unescape.html</title>
</head>

<body>
  氏名を送信する。<br>
  <form method="POST" action="unescape.php">
    氏名：<input type="text" name="name"><br>
    <input type="submit" value="送信">
  </form>
</body>

</html>
```

`unescape.php`

```php
<!DOCTYPE html>
<html lang="ja">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>unescape.php</title>
</head>

<body>
  <p>送られてきた氏名は「<?php echo $_POST['name']; ?>」です。</p>
  <a href="unescape.html">戻る</a>
</body>

</html>
```

1. ブラウザで `unescape.html` にアクセスし、氏名として次の２つの値を入力し、送信します。

- 神戸電子
- `<body  onload="alert('Hack, Now!!');">`

<br>

「神戸電子」を送信した場合
![](./images/unescape_html_display_text.png)
![](./images/unescape_php_display_text.png)

<br>

「`<body  onload="alert('Hack, Now!!');">`」を送信した場合<br>
![](./images/unescape_html_display_html.png)<br><br>
![](./images/unescape_php_display_dialog.png)<br><br>
**HTMLのコードが実行されてしまいます。** ここでは、単にダイアログを表示しているだけですが、これを悪用すると不正プログラムの感染、ユーザを騙す表示によるフィッシング詐欺、クッキー情報の取得によるセッションハイジャック、情報詐取、他の不正サイトへの誘導、などの被害に繋がります。

OKをクリックすると以下の画面が表示されます。HTMLはプログラムなので、画面にはなにも表示されていないことがわかります。
![](./images/unescape_php_display.png)<br>

この画面の余白部分で右クリックし、「ページのソースを表示」でソースコードを確認すると、入力されたHTMLが埋め込まれているのがわかります。

![](./images/unescape_php_display_source.png)<br>

このようにして、エスケープ処理をしていないと、アプリケーション開発者の意図に反した、HTMLのプログラムが実行されてしまいます。

### エスケープ処理ありの場合

そこで、HTMLのコードが実行されないように修正します。以下の `escape.html` と `escape.php` を作成します。

`escape.html`

```php
<!DOCTYPE html>
<html lang="ja">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>escape.html</title>
</head>

<body>
  氏名を送信する。<br>
  <form method="POST" action="escape.php"> <!-- action="escape.php"に修正 -->
    氏名：<input type="text" name="name"><br>
    <input type="submit" value="送信">
  </form>
</body>

</html>
```

`escape.php`

```php
<!DOCTYPE html>
<html lang="ja">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>escape.php</title>
</head>

<body>
  <?php
  function h($data)
  {
    return htmlspecialchars($data, ENT_QUOTES, "UTF-8");
  }
  ?>
  <p>送られてきた氏名は「<?php echo h($_POST['name']); ?>」です。</p>
  <a href="escape.html">戻る</a> <!-- href="escape.html"に修正 -->
</body>

</html>
```

ブラウザで `escape.html` にアクセスし、`<body  onload="alert('Hack, Now!!');">` を入力し送信します。<br>
![](./images/escape_html_display.png)<br>
![](./images/escape_php_display.png)<br>
**HTMLのコードが実行されずに、テキストして画面に表示されています。** この画面の何も書かれていない場所で右クリックし、「ページのソースを表示」させた画面が以下です。

![](./images/escape_php_display_source.png)<br>

エスケープ処理されたHTMLのコードが確認できます。エスケープ処理された特殊文字については、以下の表を参照してください。<br>

|変換前|変換後|
| - | - |
|& （アンパサンド）|`&amp;`|
|" （ダブルクォート）|`&quot;`|
|' （シングルクォート）|`&#039;`または `&apos;`|
|< （小なり）|`&lt;`|
|> （大なり）|`&gt;`|

**本章の「関数」では課題の提出はございません。**
# PHPの基本

[こちら]()のページからソースコードを`C:¥web_app_dev`へcloneしてください。



## 演算子

PHPで主に使う演算子は次のとおり。

|演算子|意味|
| - | - |
|\*\*|べき乗　$a \*\* $b  で aのb乗 を計算する（PHP5.6より）|
|++&nbsp;&nbsp;&nbsp;&nbsp;--|インクリメント（１を加算）、デクリメント（１を減算）|
|!|論理（否定）|
|\*&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;%|乗算、　除算、　剰余|
|+&nbsp;&nbsp;&nbsp;&nbsp;- &nbsp;&nbsp;&nbsp;&nbsp;.(ドット)|加算、　減算、　文字列の結合|
|<&nbsp;&nbsp;&nbsp;&nbsp;<=&nbsp;&nbsp;&nbsp;&nbsp;>&nbsp;&nbsp;&nbsp;&nbsp;>=|比較（より小さい、　以下、　より大きい、　以上）|
|==&nbsp;&nbsp;&nbsp;&nbsp;!=&nbsp;&nbsp;&nbsp;&nbsp;===|比較（等しい、　等しくない、　データ型も含め等しい）|
|&&|論理（かつ）|
|\|\||論理（または）|

## 条件分岐

### if 文

```PHP
if (  条件式　)  {
    条件式がTrue（真）の場合の処理;
} else {
    条件式がFalse（偽）の場合の処理; 
}
```

#### 具体例

```PHP
if ( $a  ==  $b ) {
    echo ' $a == $b'; 
} else {
    echo '$a != $b'; 
}
```

### switch文

```PHP
switch ( 式 ) {
    case  値１：
        式の値が「値１」の場合の処理;
        break;

    case  値２：
        式の値が「値２」の場合の処理;
        break;

・・・
    default:
        式の値がいずれの値でもない場合の処理; 
        break;
}
```

#### 具体例

```PHP

switch ( $a ) {
    case  '和食':
        echo 'うどん';
        break;
    case  '洋食':
        echo 'スパゲッティ';
        break;
    default: 
        echo 'ラーメン'; 
        break;
}
```

## 繰り返し

### for 文

```PHP
for ( 開始処理；　条件式；　更新処理 ) {
    繰り返し処理;
} 
```

#### 具体例

```PHP
for ( $i = 0;  $i < 10;  $i++ ) {
    繰り返し処理； echo  $i;
}
```

### while文

```PHP
while ( 条件式 ) {
    繰り返し処理;
}

```

#### 具体例

```PHP
while ( $a <= 10 ) {
    繰り返し処理； echo '10以下'; 
}
```

## 配列

### 定義

```PHP
配列名 = [ 値１, 値２, ．．．];
配列名 = array ( 値１, 値２, ．．． );
```

#### 具体例

```PHP
$fruits = [ 'リンゴ',  'ミカン',  'バナナ' ];
$fishes = array ( '鯛',  '鯖',  '鰤' ); //たい、さば、ぶり
```

### 要素の取り出し

```PHP
$fruits = [ 'リンゴ',  'ミカン',  'バナナ' ];
for ( $i = 0; $i < count($fruits); $i++) { //count($fruits) で配列$fruitsの要素数を返す
    echo  $fruits [ $i ]  . "<br>";
}
```

```PHP
$fishes = array ( '鯛',  '鯖',  '鰤' );
foreach ( $fishes  as  $fish ) { 　//配列$fishes の要素を $fish として繰り返し処理内で使用する
    echo  $fish . "<br>" ;
}

// PHPでは、基本的に「foreach（フォーイーチ）文」を使用する。
```

### 連想配列

PHPの配列は、「連想配列」の機能を備えていて、「キー」と「値」のペアでデータを格納することができる。

```PHP
配列名 = [ キーA => 値A,  キーB=>値B,  キーC=>値C, ．．．];
（「=>」は、「=」と「>」の２つの記号を用いて記述する。読み方は「ダブルアロー」）
```

#### 具体例

```PHP
$area =    [ '神戸'=>'078',  '大阪'=>'06',  '京都'=>'075' ];
foreach ( $area  as  $key  =>  $value ) { // 配列$area のキーを$key、値を$valueで処理する
    echo   $key . '市の市外局番は、' . $value . 'です。<br>'; 
}
```

## サンプル

`sample2.php`

```php
<!DOCTYPE html>
<html lang="ja">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>サンプル2</title>
</head>

<body>
    <?php
    $fruits = ['リンゴ', 'ミカン', 'バナナ'];
    echo '配列$fruitsには次の要素が格納されている。<br>';
    for ($i = 0; $i < count($fruits); $i++) {
        echo  $fruits[$i]  . "<br>";
    }
    $fishes = array('鯛', '鯖', '鰤'); // タイ、サバ、ブリ
    echo '配列$fishesには次の要素が格納されている。<br>';
    foreach ($fishes  as  $fish) {
        echo  $fish . "<br>";
    }
    $area = ['神戸' => '078',  '大阪' => '06',  '京都' => '075'];
    echo  '配列$areaには次のキーと値が格納されている。<br>';
    foreach ($area  as  $key  =>  $value) {
        echo   $key . '市の市外局番は、' . $value . 'です。<br>';
    }
    ?>
    <hr>
    <h4>0J0X0XX神戸電子</h4> <!-- 注意：クラス、番号、氏名は自分のものに変更すること！ -->
</body>

</html>
```

1. 先ほどの[ブラウザ上での確認](#ブラウザ上での確認)と同様の操作を行い、アドレスの末尾に `/sample2.php` と入力すると次のように表示されます。

![](./images/sample2_display.png)

**ここまでの資料はサンプルです。本章「PHPの基本」の課題は後日公開します。**

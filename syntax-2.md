---
sort: 2
---
# PHPの書き方②

## 演算子

PHPで主に使う演算子は以下のとおりです。

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

## if文

```PHP
if (  条件式　)  {
    条件式がTrue（真）の場合の処理;
} else {
    条件式がFalse（偽）の場合の処理; 
}
```

### ◆具体例(if文)

```PHP
if ( $a  ==  $b ) {
    echo ' $a == $b'; 
} else {
    echo '$a != $b'; 
}
```

## switch文

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

### ◆具体例(switch文)

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

## for文

```PHP
for ( 開始処理；　条件式；　更新処理 ) {
    繰り返し処理;
} 
```

### ◆具体例(for文)

```PHP
for ( $i = 0;  $i < 10;  $i++ ) {
    繰り返し処理； echo  $i;
}
```

## while文

```PHP
while ( 条件式 ) {
    繰り返し処理;
}

```

### ◆具体例(while文)

```PHP
while ( $a <= 10 ) {
    繰り返し処理； echo '10以下'; 
}
```

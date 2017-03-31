/\* 目次 \*/

---
 - 目次

1. [bp()](#bp)
2. [breakMax()](#breakMax)
3. [breakMin()](#breakMin)
4. [fsvw()](#fsvw)
5. [fa()](#fa)
6. [im()](#im)
7. [tri-xx()](#tri-xx)

---
## bp()
---
Break Pointを管理する関数です。<br>
関数は第三引数まで用意されております。

@mixin bp ( $type: min, $num1: false, $num2: false )

$type...minまたはmaxを指定します。minにすると<br>
        and (min-width: $num1)で吐き出されます。<br>
        初期値はminですが入力してください。<br>
$num2...ブレイクポイントの値2を指定します。<br>
$num1...ブレイクポイントの値1を指定します。<br>

$num1,$num2の順番に指定はないです。

また、この関数はcssの値を引き継ぐことができます。

コンパイル前
~~~css
html {
  @include bp( min, 100px) {
    background: red;
  }
  @include bp( min, 100px, 150px) {
    background: green;
  }
  @include bp( min, 200px, 100px) {
    background: pink;
  }
  @include bp( max, 100px) {
    background: #FFF;
  }
  @include bp( max, 100px, 150px) {
    background: #666;
  }
  @include bp( max, 200px, 100px) {
    background: #000;
  }
}
~~~

コンパイル後
~~~css
@media screen and (min-width: 100px) {
  html {
    background: red;
  }
}

@media screen and (min-width: 100px) and (max-width: 150px) {
  html {
    background: green;
  }
}

@media screen and (min-width: 100px) and (max-width: 200px) {
  html {
    background: pink;
  }
}

@media screen and (max-width: 100px) {
  html {
    background: #FFF;
  }
}

@media screen and (min-width: 100px) and (max-width: 150px) {
  html {
    background: #666;
  }
}

@media screen and (min-width: 100px) and (max-width: 200px) {
  html {
    background: #000;
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#huvrid用テンプレートファイルの説明)
<br><br><br>

---
## breakMax()
---
bp()の旧式になります。<br>
@mediaのmax-widthが設定できます。<br>
関数は第二引数まで用意されております。

@mixin breakMax ( $max, $min )

$max...ブレイクポイントの最大値を指定します。<br>
$min...ブレイクポイントの最小値を指定します。<br>

bp()と違い<br>
$max,$minの順番で指定してください。

順番を入れ替えると<br>
意図した順番に吐き出されないかもしれないので気を付けてください。

アップデートの予定はなく、<br>
しばらくしたら削除する予定です。

コンパイル前
~~~css
html {
  @include breakMax( 100px) {
    background: red;
  }
  @include breakMax( 100px, 150px) {
    background: green;
  }
  @include breakMax( 200px, 100px) {
    /* error */
    background: pink;
  }
}
~~~

コンパイル後
~~~css
@media screen and (max-width: 100px) {
  html {
    background: red;
  }
}

@media screen and (max-width: 100px) and (min-width: 150px) {
  html {
    background: green;
  }
}

@media screen and (max-width: 200px) and (min-width: 100px) {
  html {
    /* error */
    background: pink;
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#huvrid用テンプレートファイルの説明)
<br><br><br>

---
## breakMin()
---
bp()の旧式になり、<br>
breakMax()とは逆にmin-widthを設定できます。<br>
関数は第二引数まで用意されております。

@mixin breakMin ( $min, $max )

$min...ブレイクポイントの最小値を指定します。<br>
$max...ブレイクポイントの最大値を指定します。<br>

bp()と違い<br>
$min,$maxの順番で指定してください。

順番を入れ替えると<br>
意図した順番に吐き出されないかもしれないので気を付けてください。

アップデートの予定はなく、<br>
しばらくしたら削除する予定です。

コンパイル前
~~~css
html {
  @include breakMin( 100px) {
    background: red;
  }
  @include breakMin( 100px, 150px) {
    background: green;
  }
  @include breakMin( 200px, 100px) {
    /* error */
    background: pink;
  }
}
~~~

コンパイル後
~~~css
@media screen and (min-width: 100px) {
  html {
    background: red;
  }
}

@media screen and (max-width: 150px) and (min-width: 100px) {
  html {
    background: green;
  }
}

@media screen and (max-width: 100px) and (min-width: 200px) {
  html {
    /* error */
    background: pink;
  }
}
~~~

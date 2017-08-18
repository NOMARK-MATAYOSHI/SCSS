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
8. [linear-gradient()](#linear-gradient)

---
## bp()
---
Break Pointを管理する関数です。<br>
関数は第三引数まで用意されております。

@mixin bp ( $type: min, $num1: false, $num2: false )

$type...minまたはmaxを指定します。minにすると<br>
        and (min-width: $num1)で吐き出されます。<br>
        初期値はminですが入力してください。<br>
$num1...ブレイクポイントの値1を指定します。<br>
$num2...ブレイクポイントの値2を指定します。<br>

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
<br><br><br>
 - [上部へ戻る](#huvrid用テンプレートファイルの説明)
<br><br><br>

---
## fsvw()
---
<b>開発途中</b>
フォントサイズのvwで文字サイズを調整した際に最小サイズを固定するための関数。<br>

<br><br><br>
 - [上部へ戻る](#huvrid用テンプレートファイルの説明)
<br><br><br>

---
## fa()
---
[Font Awesome](http://fontawesome.io/icons/)で使用するiconのIDを使用しやすくするための関数。<br>
Font Awsomeのiconを疑似要素で使用する前提で作っているので『::before』または『::after』内で呼び出します。<br>

@mixin fa( $fontCode )

$fontCode...Font AwesomeのUnicodeを入れます。<br>

コンパイル前
~~~css
html {
  &:before {
    @include fa('\f2c8');
  }
  &:after {
    @include fa(\f2c8);
  }
  &:after {
    @include fa(f2c8);
  }
}
~~~

コンパイル後
~~~css
html:before{
  content:"\"; /* 一部テキストエディタでは文字化けするがブラウザ上では問題ない */
  font-family:FontAwesome;
  line-height:1;
}
html:after{
  content:"\f2c8";
  font-family:FontAwesome;
  line-height:1;
}
html:after{
  content:"\f2c8";
  font-family:FontAwesome;
  line-height:1;
}
~~~
<br><br><br>
 - [上部へ戻る](#huvrid用テンプレートファイルの説明)
<br><br><br>

---
## im()
---
[icomoon](https://icomoon.io/app/#/select)で使用するiconのIDを使用しやすくするための関数。<br>
icomoonのiconを疑似要素で使用する前提で作っているので『::before』または『::after』内で呼び出します。<br>

@mixin im( $fontCode )

$fontCode...icomoonのUnicodeを入れます。<br>

コンパイル前
~~~css
html {
  &:before {
    @include im('\e900');
  }
  &:after {
    @include im(\e900);
  }
  &:after {
    @include im(e900);
  }
}
~~~

コンパイル後
~~~css
html:before{
  content:"\"; /* 一部テキストエディタでは文字化けするがブラウザ上では問題ない */
  font-family:icomoon;
  line-height:1;
}
html:after{
  content:"\e900";
  font-family:icomoon;
  line-height:1;
}
html:after{
  content:"\e900";
  font-family:icomoon;
  line-height:1;
}
~~~
<br><br><br>
 - [上部へ戻る](#huvrid用テンプレートファイルの説明)
<br><br><br>

---
## tri-xx()
---
cssで三角形を作るための関数。<br>
tri-xx()の『xx』部分で頂点の方向を指定します。（計8パターン）<br>

@mixin tri-xx( $color, $width, $height: false )

$color...rgb(),rgba(),#FFF等で色を指定します。<br>
$width...幅を指定します。<br>
$height...高さを指定します指定しない場合は$widthと同じ値になります。<br>

コンパイル前
~~~css
body {
  &:before {
    content: '';

    // top
    @include tri-t( #000, 5px );

    // right
    @include tri-r( #FFF, 10px, 5px );

    // bottom
    @include tri-b( red, 20em );

    // left
    @include tri-l( rgb( 255, 255, 0 ), 3px );

    // top right
    @include tri-tr( rgba( 0, 0, 0,.5 ), 5px, 80em );

    // bottom right
    $width: 5px;
    @include tri-br( #000, $width, 0px );

    // bottom left
    $height: 300px;
    @include tri-bl( pink, 20px, $height / 5 );

    // top left
    @include tri-tl( black, 10px, 10px );
  }
}
~~~

コンパイル後
~~~css
html:before{
  content: '';

  // top
  display: block;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 0 2.5px 5px 2.5px;
  border-color: transparent transparent #000 transparent;

  // right
  display: block;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 2.5px 0 2.5px 10px;
  border-color: transparent transparent transparent #FFF;

  // bottom
  display: block;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 20em 10em 0 10em;
  border-color: red transparent transparent transparent;

  // left
  display: block;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 1.5px 3px 1.5px 0;
  border-color: transparent yellow transparent transparent;

  // top right
  display: block;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 0 5px 80em 0;
  border-color: transparent rgba(0, 0, 0, 0.5) transparent transparent;

  // bottom right
  display: block;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 0 0 0px 5px;
  border-color: transparent transparent #000 transparent;

  // bottom left
  display: block;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 60px 0 0 20px;
  border-color: transparent transparent transparent pink;

  // top left
  display: block;
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 10px 10px 0 0;
  border-color: black transparent transparent transparent;
}
~~~
<br><br><br>
 - [上部へ戻る](#huvrid用テンプレートファイルの説明)
<br><br><br>

---
## linear-gradient()
---
cssでグラデーションパターンを作るための関数。<br>
単調なグラデーションは作成できます。<br>

@mixin linear-gradient($direction, $args)

$direction...方向を指定します。<br>
型は 'Num(deg付き)' または 'String' となっています。<br>
'String'の場合は下記で指定してください。<br>
 - top ( または to bottom )
 - right ( または to left )
 - bottom ( または to top )
 - left ( または to right )
 - bottom right ( または to top left )
 - bottom left ( または to top right )
 - top left ( または to bottom right )
 - top right ( または to bottom left )
 - right bottom ( または to left top )
 - left bottom ( または to right top )
 - left top ( または to right bottom )
 - right top ( または to left bottom )

$args...連想配列になります。<br>
keyに反映したい位置、valueにカラーが入ります。<br>
keyに入れる値は%で指定してください。<br>
例 : $args : ( 0% : red, 50% : rgba( 0, 0, 0, .3 ), );

~~~css
body {
  $args : (
    0% : #000,
    10% : pink,
    50% : rgba( 0, 0, 0, .3 ),
    70% : rgb( 0, 255, 0 ),
    75% : transparent,
    100% : #FFF,
  );

  @include linear-gradient( 'top', $args );
  &:before {
    content: '';
    display: block;
    padding-top: 200px;
    @include linear-gradient( 30deg, $args );
  }
}
~~~

コンパイル後
~~~css
html {
  /* Old browsers */
  background: #000;
  /* FF3.6-15 */
  background: -moz-linear-gradient("top", #000 0%, pink 10%, rgba(0, 0, 0, 0.3) 50%, lime 70%, transparent 75%, #FFF 100%);
  /* Chrome10-25,Safari5.1-6 */
  background: -webkit-linear-gradient("top", #000 0%, pink 10%, rgba(0, 0, 0, 0.3) 50%, lime 70%, transparent 75%, #FFF 100%);
  /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
  background: -webkit-gradient(linear, left top, left bottom, from(#000), color-stop(10%, pink), color-stop(50%, rgba(0, 0, 0, 0.3)), color-stop(70%, lime), color-stop(75%, transparent), to(#FFF));
  background: -webkit-linear-gradient(top, #000 0%, pink 10%, rgba(0, 0, 0, 0.3) 50%, lime 70%, transparent 75%, #FFF 100%);
  background: -o-linear-gradient(top, #000 0%, pink 10%, rgba(0, 0, 0, 0.3) 50%, lime 70%, transparent 75%, #FFF 100%);
  background: linear-gradient(to bottom, #000 0%, pink 10%, rgba(0, 0, 0, 0.3) 50%, lime 70%, transparent 75%, #FFF 100%);
  /* IE6-9 */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#000', endColorstr='#FFF',GradientType=0 );
}

html:before {
  content: '';
  display: block;
  padding-top: 200px;

  /* Old browsers */
  background: #000;
  /* FF3.6-15 */
  background: -moz-linear-gradient(60deg, #000 0%, pink 10%, rgba(0, 0, 0, 0.3) 50%, lime 70%, transparent 75%, #FFF 100%);
  /* Chrome10-25,Safari5.1-6 */
  background: -webkit-linear-gradient(60deg, #000 0%, pink 10%, rgba(0, 0, 0, 0.3) 50%, lime 70%, transparent 75%, #FFF 100%);
  /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
  background: -o-linear-gradient(60deg, #000 0%, pink 10%, rgba(0, 0, 0, 0.3) 50%, lime 70%, transparent 75%, #FFF 100%);
  background: linear-gradient(30deg, #000 0%, pink 10%, rgba(0, 0, 0, 0.3) 50%, lime 70%, transparent 75%, #FFF 100%);
  /* IE6-9 */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#000', endColorstr='#FFF',GradientType=1 );
}
~~~

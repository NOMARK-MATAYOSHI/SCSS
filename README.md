/\* 目次 \*/

---
 - 目次

1. [@function unit_delete()](#mixin-unit_delete)
1. [@mixin bp()](#mixin-bp)
1. [@mixin hack()](#mixin-hack)
1. [@function vw_sp()](#function-vw_sp)
1. [@mixin vw_sp()](#mixin-vw_sp)
1. [@function vw_pc()](#function-vw_pc)
1. [@mixin vw_pc()](#mixin-vw_pc)
1. [@function per_sp()](#function-per_sp)
1. [@mixin per_sp()](#mixin-per_sp)
1. [@function per_pc()](#function-per_pc)
1. [@mixin per_pc()](#mixin-per_pc)
1. [@function ls()](#function-ls)
1. [@mixin ls()](#mixin-ls)
1. [@function lh_er()](#function-lh_er)
1. ~~[@function fsvw()](#function-fsvw)~~ delete v2.7.0
1. [@mixin fa()](#mixin-fa)
1. [@mixin fa4()](#mixin-fa4)
1. [@mixin fa5()](#mixin-fa5)
1. [@mixin im()](#mixin-im)
1. [@mixin tri-xx()](#mixin-tri-xx)
1. [@mixin linear-gradient()](#mixin-linear-gradient)
1. ~~[radial-gradient()](#radial-gradient)~~ Unimplemented
1. [@function repeating-linear()](#function-repeating-linear)
1. [@function repeating-radial()](#function-repeating-radial)
1. [@mixin text-border()](#mixin-text-border)
1. [@mixin leader()](#mixin-leader)
1. [@mixin break-leader()](#mixin-break-leader)
1. [@mixin column()](#mixin-column)
1. [@mixin grid()](#mixin-grid)
1. [@mixin absolute()](#mixin-absolute)
1. [@mixin placeholder()](#mixin-placeholder)
1. [@function sin()](#function-sin)
1. [@function cos()](#function-cos)
1. [@function tan()](#function-tan)

---
## @function unit_delete()
---
単位を削除する関数です。<br>
引数は第一引数のみです。

@function unit_delete( $num )

$num...単位付きの数字、単位なしの数字<br>

コンパイル前
~~~css
.fs {
  $fs: 5px;
  font-size: $fs;
  
  @media screen and (max-width: 600px) {
    font-size: calc( unit_delete( $fs ) / 600 * 100vw );
  }
}
~~~

コンパイル後
~~~css
.fs {
  font-size: 5px;
}

@media screen and (max-width: 600px) {
  .fs {
    font-size: calc( 5 / 600 * 100vw );
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin bp()
---
Break Pointを管理する関数です。<br>
関数は第三引数まで用意されております。

@mixin bp ( $type: min, $num1: false, $num2: false )

$type...minまたはmaxを指定します。<br>
        minにすると and (min-width: $num1) で吐き出されます。<br>
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
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin hack()
---
引数で渡した対象のブラウザハックを行う関数。<br><br>

@mixin hack( $support )
$support...'Chrome', 'Safari', 'Firefox', 'Edge', 'IE' の何れか。

コンパイル前
~~~css
body {
  @include hack( IE ) {
    background: pink;
  }
}
~~~

コンパイル後
~~~css
_:-ms-lang( x )::-ms-backdrop, body {
  background: pink;
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function vw_sp()
---
デザインのSP幅(750px)に対してどれぐらいの比率のvwになるかを計算する関数。<br><br>

@function vw_sp( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  @include bp( max, 600px ) {
    font-size: vw_sp( 36 );     // -> 36 / 750 * 100vw
    margin-bottom: vw_sp( 44 ); // -> 44 / 750 * 100vw
  }
}
~~~

コンパイル後
~~~css
@media screen and ( max-width: 600px ) {
  html {
    font-size: 4.8vw;         // -> 36 / 750 * 100vw
    margin-bottom: 5.86667vw; // -> 44 / 750 * 100vw
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin vw_sp()
---
デザインのSP幅(750px)に対してコンテンツがどれぐらいの比率のvwになるかを計算し幅を設定する関数。<br><br>

@mixin vw_sp( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  @include bp( max, 600px ) {
    @include vw_sp( 500 );
  }
}
~~~

コンパイル後
~~~css
@media screen and ( max-width: 600px ) {
  html {
    width: 66.66667vw;
    max-width: 500px;
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function vw_pc()
---
デザインのPC幅(1200px)に対してどれぐらいの比率のvwになるかを計算する関数。<br><br>

@function vw_pc( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  @include bp( max, 1200px ) {
    font-size: vw_pc( 36 );     // -> 36 / 1200 * 100vw
    margin-bottom: vw_pc( 44 ); // -> 44 / 1200 * 100vw
  }
}
~~~

コンパイル後
~~~css
@media screen and ( max-width: 1200px ) {
  html {
    font-size: 3vw;           // -> 36 / 1200 * 100vw
    margin-bottom: 3.66667vw; // -> 44 / 1200 * 100vw
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin vw_pc()
---
デザインのPC幅(1200px)に対してコンテンツがどれぐらいの比率のvwになるかを計算し幅を設定する関数。<br><br>

@mixin vw_sp( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  @include bp( max, 1200px ) {
    @include vw_pc( 500 );
  }
}
~~~

コンパイル後
~~~css
@media screen and ( max-width: 1200px ) {
  html {
    width: 41.66667vw;
    max-width: 500px;
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function per_sp()
---
デザインのSP幅(750px)に対してどれぐらいの比率（%）になるかを計算する関数。<br>※ただし『%』は親と相対的な計算になるため使用には注意すること<br><br>

@function per_sp( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  @include bp( max, 600px ) {
    font-size: per_sp( 36 );     // -> 36 / 750 * 100%
    margin-bottom: per_sp( 44 ); // -> 44 / 750 * 100%
  }
}
~~~

コンパイル後
~~~css
@media screen and ( max-width: 600px ) {
  html {
    font-size: 4.8%;         // -> 36 / 750 * 100%
    margin-bottom: 5.86667%; // -> 44 / 750 * 100%
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin per_sp()
---
デザインのSP幅(750px)に対してコンテンツがどれぐらいの比率（%）になるかを計算する関数。<br>※ただし『%』は親と相対的な計算になるため使用には注意すること<br><br>

@mixin per_sp( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  @include bp( max, 600px ) {
    @include per_sp( 500 );
  }
}
~~~

コンパイル後
~~~css
@media screen and ( max-width: 600px ) {
  html {
    width: 66.66667%;
    max-width: 500px;
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function per_pc()
---
デザインのPC幅(1200px)に対してどれぐらいの比率（%）になるかを計算する関数。<br>※ただし『%』は親と相対的な計算になるため使用には注意すること<br><br>

@function per_pc( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  @include bp( max, 1200px ) {
    font-size: per_pc( 36 );     // -> 36 / 1200 * 100%
    margin-bottom: per_pc( 44 ); // -> 44 / 1200 * 100%
  }
}
~~~

コンパイル後
~~~css
@media screen and ( max-width: 1200px ) {
  html {
    font-size: 3%;
    margin-bottom: 3.66667%;
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin per_pc()
---
デザインのPC幅(1200px)に対してコンテンツがどれぐらいの比率（%）になるかを計算する関数。<br>※ただし『%』は親と相対的な計算になるため使用には注意すること<br><br>

@mixin per_sp( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  @include bp( max, 1200px ) {
    @include per_pc( 500 );
  }
}
~~~

コンパイル後
~~~css
@media screen and ( max-width: 1200px ) {
  html {
    width: 41.66667%;
    max-width: 500px;
  }
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function ls()
---
PhotoShop上で表記されているletter-spacing値を変換する関数。<br><br>

@function ls( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  letter-spacing: ls( 200 );
}
~~~

コンパイル後
~~~css
html {
  letter-spacing: .2em;
}
~~~

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin ls()
---
PhotoShop上で表記されているletter-spacing値を変換する関数。<br><br>

@mixin ls( $num )
$num...数字。単位はつけない。

コンパイル前
~~~css
html {
  @include ls( 200 );
}
~~~

コンパイル後
~~~css
html {
  letter-spacing: .2em;
}
~~~

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function lh_er()
---
line-hightで伸びた高さを算出する関数。<br>
margin値の調整などに使用<br><br>

@function lh_er( $lh, $fs: false )
$lh...line-hightの大きさ。
$fs...フォントサイズ。単位は必須。単位がない場合は数値が返ります。（省略可）

コンパイル前
~~~css
html {
  margin-top: lh_er( 2, 16px );
  margin-top: lh_er( 3.2, 16 );
  margin-top: lh_er( 2 ) * -1;
}
~~~

コンパイル後
~~~css
html {
    margin-top: 8px;
    margin-top: 17.6;
    margin-top: -.5em;
}
~~~

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function fsvw()
---
フォントサイズのvwで文字サイズを調整した際に最小サイズを固定するための関数。<br>
<b>※v2.7.0から削除</b>

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin fa()
---
[Font Awesome](https://fontawesome.io/icons/)で使用するiconのIDを使用しやすくするための関数。<br>
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
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin fa4()
---
[Font Awesome v4.x](https://fontawesome.com/v4.7.0/)用

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin fa5()
---
[Font Awesome v5.x](https://fontawesome.io/icons/)用
`@mixin fa()`と違い`font-weight: 900;`で固定のため揺らぎに注意。

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin im()
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
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin tri-xx()
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
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin linear-gradient()
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
body {
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

body:before {
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
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function repeating-linear()
---
パターン作成用の関数。<br>
使用用途はまとめておりますので後日。

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function repeating-radial()
---
パターン作成用の関数。<br>
使用用途はまとめておりますので後日。

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin text-border()
---
cssでテキストにボーダーを付けるための関数。<br>
使用できる最大の太さは5px前後かと思います。<br>

@mixin text-border($width, $color)

$width...太さを指定します。単位は外してください。<br>
$color...色を指定します。<br>
~~~css
ｐ {
  @include text-border( 3, #FFF );
}
~~~

コンパイル後
~~~css
p {
  text-shadow: #FFF -3px 0px, #FFF -2px -1px, #FFF -1px -2px, #FFF 0px -3px , #FFF 0px -3px, #FFF 1px -2px, #FFF 2px -1px, #FFF 3px 0px , #FFF 3px 0px, #FFF 2px 1px, #FFF 1px 2px, #FFF 0px 3px , #FFF 0px 3px, #FFF -1px 2px, #FFF -2px 1px, #FFF -3px 0px;
}
~~~
※補足<br>
$widthの設定値分、上下左右にずらし<br>
その後その点を結ぶように影の位置をずらしています。<br>
また、文字とずらした位置の補完を完全には行っていません。<br><br>
なので$widthの設定値を大きくすると<br>
穴の開いた菱型のようになりborderとはとても言えなくなりますのであしからず。。。
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin leader()
---
cssで再現する三点リーダー用のアセット。<br>
`@content`を入れているので上書き可能になっております。<br>

~~~css
h1 {
  @include leader();
}
ｐ {
  @include leader() {
    display: inline-block; /* add */
  };
}
~~~

コンパイル後
~~~css
h1 {
  overflow: hidden;
  display: block;
  width: 100%;
  max-width: 100%;
  white-space: nowrap;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
}
p {
  overflow: hidden;
  display: block;
  width: 100%;
  max-width: 100%;
  white-space: nowrap;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;

  display: inline-block; /* add */
}
~~~
<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin break-leader()
---
`@mixin leader()`をリセットするために作成<br>
。。。がうまく効いていないようなので確認中。

~~~css
h1 {
  @include break-leader();
}
ｐ {
  @include break-leader() {
    display: inline-block; /* add */
  };
}
~~~

コンパイル後
~~~css
h1 {
  overflow: visible;
  width: auto;
  max-width: none;
  white-space: normal;
  text-overflow: clip;
}
p {
  overflow: visible;
  width: auto;
  max-width: none;
  white-space: normal;
  text-overflow: clip;

  display: inline-block; /* add */
}
~~~

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin column()
---
折り返し対応の等倍コンテンツを簡単な形式で作成します。<br><br>
HTMLとの連携が必要で、<br>
親コンテンツに対し、対象となるクラス（`.任意`）、列指定クラス（`.任意--N`）を付与、<br>
子コンテンツに`.任意__item`を付与し作成してください。<br>
この際、列指定クラスで指定した`N個の子コンテンツ`を作成してください<br>

@mixin column( $length, $margin )

$length...列数<br>
$margin...余白値<br>

~~~html
---例---

対象となるクラスを.colとした場合

<div class="col col--2">
  <div class="col__item"></div>
  <div class="col__item"></div>
</div>
~~~

~~~css
.col {
  $length: 2;
  $margin: 5px;

  @include column( $i, $margin );
  @include bp( max, 600px ) {
    @include column( $i, vw_sp( unit_delete( $margin ) ) );
  }
}
~~~

コンパイル後
~~~css
.col--2 {
  display: flex;
  flex-wrap: wrap;
  margin-top: -5px;
  margin-left: -5px;
}
.col--2 .col__item {
  width: calc((100% - 5px) / 2);
  margin-top: 5px;
  margin-left: 5px;
}

@media screen and (max-width:600px) {
  .col--2 {
    display: flex;
    flex-wrap: wrap;
    margin-top: -1.3333333333vw;
    margin-left: -1.3333333333vw;
  }
  .col--2 .col__item {
    width: calc((100% - 2.6666666666vw) / 2);
    margin-top: 1.3333333333vw;
    margin-left: 1.3333333333vw;
  }
}
~~~

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin grid()
---
折り返し対応の等比コンテンツを簡単な形式で作成します。<br>
HTMLとの連携が必要で、<br>
親となるコンテンツに対し、対象となるクラス（`.任意`）、列指定クラス（`.任意--N`）を付与、<br>
子となるコンテンツに`.任意__item`、`.任意__item--n`を付与し作成してください。<br>
この際、`.任意__item--n`のサイズは親に対し`n/N`となります。<br>


@mixin grid( $length )

$length...列数<br>

~~~html
---例---

対象となるクラスを.gridとした場合
下記のようなHTMLが作成できます。

<div class="grid grid--4">
  <div class="grid__item grid__item--1">1/4</div>
  <div class="grid__item grid__item--1">1/4</div>
  <div class="grid__item grid__item--1">1/4</div>
  <div class="grid__item grid__item--1">1/4</div>
</div>

<div class="grid grid--4">
  <div class="grid__item grid__item--1">1/4</div>
  <div class="grid__item grid__item--1">1/4</div>
  <div class="grid__item grid__item--2">1/2</div>
</div>

<div class="grid grid--4">
  <div class="grid__item grid__item--1">1/4</div>
  <div class="grid__item grid__item--3">1/3</div>
</div>
~~~

~~~css
.grid {
  $length: 1;

  @include grid( $length );
}
~~~

コンパイル後
~~~css
.grid {
  display: flex
}

.grid.grid--4 .grid__item--1 {
  width: calc(100% * 1 / 4)
}

.grid.grid--4 .grid__item--2 {
  width: calc(100% * 2 / 4)
}

.grid.grid--4 .grid__item--3 {
  width: calc(100% * 3 / 4)
}

.grid.grid--3 .grid__item--1 {
  width: calc(100% * 1 / 3)
}

.grid.grid--3 .grid__item--2 {
  width: calc(100% * 2 / 3)
}

.grid.grid--2 .grid__item--1 {
  width: calc(100% * 1 / 2)
}

.grid.grid--1 .grid__item--1 {
  width: calc(100% * 1 / 1)
}

.grid.grid--1 .grid__item--0 {
  width: calc(100% * 0 / 1)
}

.grid__item {
  flex: 1 1 auto
}
~~~

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin absolute()
---
`position: absolute;`と`transform`を使用し、強制的に真ん中に配置する方法。<br>
第一引数を『true』にすることで左右が、<br>
第二引数を『true』にすることで上下の位置が真ん中になります。<br>

@mixin absolute( $horizontal: false, $vertical: false )

$horizontal...左右の真ん中揃えを有効にするか<br>
$vertical...上下の真ん中揃えを有効にするか<br>

~~~css
p {
  @include absolute();
}
p {
  @include absolute( true, false );
}
p {
  @include absolute( true, true );
}
p {
  @include absolute( false, true );
}
~~~

コンパイル後
~~~css
p {
  position: absolute;
}
p {
  position: absolute;
  right: 50%;
  transform: translate( 50%, 0 );
}
p {
  position: absolute;
  right: 50%;
  bottom: 50%;
  transform: translate( 50%, 50% );
}
p {
  position: absolute;
  bottom: 50%;
  transform: translate( 0, 50% );
}
~~~

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @mixin placeholder()
---
placeholderのcollarを指定する関数。<br>

@mixin placeholder( $color )

$color...rgb(),rgba(),#FFF等で色を指定します。<br>

~~~css
textarea {
  @placeholder( #333 );
}
~~~

コンパイル後
~~~css
textarea::placeholder {
  color: #333;
}
textarea&:-ms-input-placeholder {
  color: #333;
}
textarea::-ms-input-placeholder {
  color: #333;
}
~~~

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function sin()
---
三角関数のsinです。<br>

@function sin( $angle )

$angle...角度。'deg' or 'rad'。<br>

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function cos()
---
三角関数のcosです。<br>

@function cos( $angle )

$angle...角度。'deg' or 'rad'。<br>

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>

---
## @function tan()
---
三角関数のtanです。<br>

@function tan( $angle )

$angle...角度。'deg' or 'rad'。<br>

<br><br><br>
 - [上部へ戻る](#readme)
<br><br><br>
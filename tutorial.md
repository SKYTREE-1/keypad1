# micro:bit × NeoPixel（4球 I型）チュートリアル# micro:bit × NeoPixel（8球 I型）チュートリアル
```package
neopixel=github:microsoft/pxt-neopixel
keypad=github:lioujj/pxt-keypad
```

## keypadを利用してライトバーの色を変えよう@showdialog
この活動では、「カラフル・ライトバーをつくろう」で学習したLEDとkeypad を組み合わせて、指定した色に切り替えるプログラムを作ってみよう」

<!--![メインイメージ](https://www.kodai.uec.ac.jp/sk/make-code/np/img_neopixel.png)-->

---

## 1. 接続しよう@showdialog

まず、テープLED と keypad を micro:bit に接続しましょう。

**配線1**
- micro:bit → テープLED（NeoPixel）  
  - 3V → +5V
  - P12 → DIN
  - GND → GND

👉 接続部分を上にして左から+5V, DIN, GND。（黄色の線は信号、赤/白はモジュールごとに違うので注意‼）。  

![配線図１](https://www.kodai.uec.ac.jp/sk/make-code/np/img_wiring_uecsc.png)
  写真では、真ん中の線（DIN）をP0に接続するように書いてありますが、P12に接続してください。

## 1. 接続しよう@showdialog

まず、テープLED と keypad を micro:bit に接続しましょう。

**配線2**
- micro:bit → keypad
  - P0 → R1
  - P1 → R2
  - P2 → R3
  - P8 → R4
  - P13 → C1
  - P14 → C2
  - P15 → C3
  - P16 → C4

👉 kiypad を上にして、左から番号を振っています。

![配線図2](https://github.com/SKYTREE-1/keypad1/blob/7da951ecda1ca0e339f5be36227d626886317810/images/wiring-diagram_keypad.png?raw=true)
  写真では、真ん中の線（DIN）をP0に接続するように書いてありますが、P12に接続してください。

## テープLEDを光らせよう1　LEDの個数の設定
1. テープLEDの点灯テスト

はじめに、テープLEDを光らせるテストをします。
``||neopixel: NeoPixel ||`` にある ``||variables:変数 strip を〜||``を``||basic:最初だけ||``にいれて``||neopixel: 端子P0に接続しているLED24個の〜 ||``の「24」を「8」にかえます。  

   ```blocks
   let strip = neopixel.create(DigitalPin.P0, 8, NeoPixelMode.RGB)
   ```

## テープLEDを光らせよう2　全部赤で光らせる
``||input:入力||``から``||input:ボタンAが押されたとき||``をだして、``||neopixel:strip を赤色に点灯する||``をいれる。

   ```blocks
   input.onButtonPressed(Button.A, function () {
    strip.showColor(neopixel.colors(NeoPixelColors.Red))
})

  let strip: neopixel.Strip = null
   ```


## テープLEDを光らせよう3　テスト@showdialog
ここまでのプログラムができたら、micro:bit にダウンロードして動かしてみよう。

   ```blocks
   input.onButtonPressed(Button.A, function () {
    strip.showColor(neopixel.colors(NeoPixelColors.Red))
    })
    let strip: neopixel.Strip = null

  ```



## 2.状態（モード）の設定（導入） @showdialog
2. 状態（モード）についての説明

これから作るプログラムでは、プログラムでは 次の2つの状態（モード） を考えます。

 - 待機モード（Standby）
    - 何も入力を受け付けない状態です。ボタンが押されるまで待っています。
 - 入力受付モード（Input）
    - ボタンやセンサーからの入力を受け付ける状態です。入力があると処理を実行したり、データを記録したりできます。


ポイント：
プログラムはこの モードの切り替え によって「今何をしているか」を判断します。

## 2.状態（モード）の設定（導入２） @showdialog
モードの状態は 変数 mode で管理します。

- mode = 0  … 待機モード(standby)
- mode = 1 … 入力受付モード（input）

この変数によって、プログラムが動作を変えます。

モードの切り替えには、Aボタンを割り当て、待機モード ⇄ 入力受付モード というように切り替えるようにします。

では、プログラムを作りましょう。

## 2. 状態（モード）の設置（変数の作成）
``||variables:変数||`` の``||variables:変数を追加する...||``で、新しい変数 **mode** を作成します。
また、最初だけに ``||variables:変数 mode を 0 にする||`` をセットします。

```blocks
let mode = 0
```

## 2. 状態（モード）の設置（modeの切り替え）
``||input:ボタンAが押されたとき||`` をだします。
``||logic:論理||`` にある、フォークの形のブロックを``||input:ボタンAが押されたとき||`` にセットして、条件のところが **mode = 0** となるようにブロックをセットします。

```blocks
input.onButtonPressed(Button.A, function () {
    strip.showColor(neopixel.colors(NeoPixelColors.Red))
    if (mode == 0) {
    	
    } else {
    	
    }
})
let strip: neopixel.Strip = null
```
## 2. 状態（モード）の設置（modeの切り替え）
``||input:ボタンAが押されたとき||`` のなかの条件分岐の **mode = 0**  後に ``||variables:変数||``から、``||variables:変数 mode を 0 にする||`` をセットして、0を１に変えます。
その後に、``||basic:基本||`` にある``||basic:数を表示（　）||`` を入れ、0の部分に`||variables:mode||`` をあてはめます。
また、``||neopixel:strip を赤色に点灯する||````を、``||basic:数を表示（　）||``の下に移動します。

```blocks
input.onButtonPressed(Button.A, function () {
    if (mode == 0) {
        mode = 1
        basic.showNumber(mode)
        strip.showColor(neopixel.colors(NeoPixelColors.Red))
    } else {

    }
})
let strip: neopixel.Strip = null
```

## 2. 状態（モード）の設置（modeの切り替え）
``||input:ボタンAが押されたとき||``のなかの条件分岐の **でなければ**の後に、``||variables:変数 mode を 0 にする||``をセットします。
その後に、``||basic:基本||`` にある``||basic:数を表示（　）||`` 追加して、0の部分に`||variables:mode||`` をあてはめます。
また、``||neopixel:strip をblackに点灯する||````を、``||basic:数を表示（　）||``の下に追加します。

```blocks
input.onButtonPressed(Button.A, function () {
    if (mode == 0) {
        mode = 1
        basic.showNumber(mode)
        strip.showColor(neopixel.colors(NeoPixelColors.Red))
    } else {
        mode = 0
        basic.showNumber(mode)
        strip.showColor(neopixel.colors(NeoPixelColors.Black))
    }
})
let strip: neopixel.Strip = null
```

## 2. 状態（モード）の設置（テスト） @showdialog
ここまでのプログラムです。


```blocks

input.onButtonPressed(Button.A, function () {
    if (mode == 0) {
        mode = 1
        basic.showNumber(mode)
        strip.showColor(neopixel.colors(NeoPixelColors.Red))
    } else {
        mode = 0
        basic.showNumber(mode)
        strip.showColor(neopixel.colors(NeoPixelColors.Black))
    }
})
let mode = 0
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 8, NeoPixelMode.RGB)
mode = 0
let color = ""
basic.forever(function () {
	
})

```
## 状態（モード）の設置（テスト） 
micro:bit にダウンロードして実際に動かしてみましょう。
A ボタンを押すことで、モードの表示が切り替わることが確認できたら、次へ進みましょう。

## 3.キー入力を受け取る @showdialog
待機モード(0)と入力受付モード(1)の切り替えができたら、入力受付モードの時に、
キーパッドからの数の入力を受け取って変数 **color** に代入するようプログラムをします。
キーパッドから入力した数は、文字列型で渡されるので、必要に応じて、数値に変換して利用します。

## 3.キー入力を受け取る（変数の作成）
``||variables:変数||`` の``||variables:変数を追加する...||``で、新しい変数 **color** を作成します。
そして、最初だけに ``||variables:変数 mode を 0 にする||`` をセットして、``||advanced:高度なブロック||``の``||text:文字列||``の一番上にある``||text:" "||``を

```blocks
let c = ""
```


## もっとテープLEDを光らせよう 5　ポーズ
``||basic:一時停止（　）ミリ秒||``ブロックを使って、0.2秒ほど、そのまま待機するようにプログラムを変更します。
``||neopixel:strip を赤色に点灯する||`` と ``||neopixel:strip をblack色に点灯する||`` の後に、それぞれ、``||basic:基本||`` の``||basic:一時停止（ミリ秒） 100||`` をいれ、「100」 を「200」にかえます。必ず２箇所にいれてください。

```blocks
input.onButtonPressed(Button.A, function () {
    for (let index = 0; index < 10; index++) {
        strip.showColor(neopixel.colors(NeoPixelColors.Red))
        basic.pause(200)
        strip.showColor(neopixel.colors(NeoPixelColors.Black))
        basic.pause(200)
    }
})
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 4, NeoPixelMode.RGB)
```

## もっとテープLEDを光らせよう 6 テスト @showdialog
ここまでのプログラムです。

```blocks
input.onButtonPressed(Button.A, function () {
    for (let index = 0; index < 10; index++) {
        strip.showColor(neopixel.colors(NeoPixelColors.Red))
        basic.pause(200)
        strip.showColor(neopixel.colors(NeoPixelColors.Black))
        basic.pause(200)
    }
})
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 4, NeoPixelMode.RGB)
```

## もっとテープLEDを光らせよう 6 テスト 
ここまでできたら、micro:bit にダウンロードして実際に動かしてみましょう。
ついたり、きえたりすることを確認したら、早く点滅させたり、ゆっくり点滅させたり、点滅の回数を増やしたりしてみてください。

## ライトウェーブ（説明）　 @showdialog

### 🌀 光の流れを操れ！

この活動では、micro:bitとNeoPixel（8個）を使って、光が流れるように見える「ライトウェーブ」を作ります。
✨スピードを変えたり、色を変えたり、リズムに合わせて光らせるても楽しいです。

はじめに、LEDの番号について確認しましょう。以下のように、micro:bit に近い方から、0番目、1番目、...のように数えます。


![LEDの数え方](https://www.kodai.uec.ac.jp/sk/make-code/np/img_neopixel_uecsc.png)

## ライトウェーブ１
``||input:入力||`` から ``||input:ゆさぶられたとき||`` をだして、``||neopixel:NeoPixel||`` のその他にある ``||neopixel:strip の（0）番目を[赤]色に設定する||`` を、いれる。０番目は、一番 micro:bit に近いLEDのことです。（色は自由に変更していいです。）

```blocks
input.onGesture(Gesture.Shake, function () {
    strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
})
let strip: neopixel.Strip = null
```


## ライトウェーブ２
同じように``||neopixel:strip の（0）番目を[赤]色に設定する||`` を使って、１番目～７番目のLEDの色を設定してください。色は自由に決めてください。

```blocks
input.onGesture(Gesture.Shake, function () {
    strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
    strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Orange))
    strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Yellow))
    strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Green))
    strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Blue))
    strip.setPixelColor(5, neopixel.colors(NeoPixelColors.Indigo))
    strip.setPixelColor(6, neopixel.colors(NeoPixelColors.Purple))
    strip.setPixelColor(7, neopixel.colors(NeoPixelColors.White))
})
let strip: neopixel.Strip = null
```

## ライトウェーブ3
４つのLEDの色を設定したら、``||neopixel:NeoPixel||``　の ``||neopixel:strip を設定した色で点灯する||`` を``||input:ゆさぶられたとき||`` の一番下に追加する。

```blocks
input.onGesture(Gesture.Shake, function () {
    strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
    strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Orange))
    strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Yellow))
    strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Green))
    strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Blue))
    strip.setPixelColor(5, neopixel.colors(NeoPixelColors.Indigo))
    strip.setPixelColor(6, neopixel.colors(NeoPixelColors.Purple))
    strip.setPixelColor(7, neopixel.colors(NeoPixelColors.White))
    strip.show()
})
let strip: neopixel.Strip = null
```
## ライトウェーブ4 テスト @showdialog
ここまででのプログラムです。

```blocks
input.onButtonPressed(Button.A, function () {
    for (let index = 0; index < 10; index++) {
        strip.showColor(neopixel.colors(NeoPixelColors.Red))
        basic.pause(200)
        strip.showColor(neopixel.colors(NeoPixelColors.Black))
        basic.pause(200)
    }
})
input.onGesture(Gesture.Shake, function () {
    strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
    strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Orange))
    strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Yellow))
    strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Green))
    strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Blue))
    strip.setPixelColor(5, neopixel.colors(NeoPixelColors.Indigo))
    strip.setPixelColor(6, neopixel.colors(NeoPixelColors.Purple))
    strip.setPixelColor(7, neopixel.colors(NeoPixelColors.White))
    strip.show()
})
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 8, NeoPixelMode.RGB)
```
## ライトウェーブ4 テスト 
micro:bit にダウンロードして実際に動かしてみましょう。
設定した色で光らせることができたら、次へ進みます。


## ライトウェーブ5
次は、設定した色を順番に変えていきます。
``||input:ゆさぶられたとき||`` の一番下に　``||loops:ループ||`` の ``||loops:くりかえし（4）回||`` をいれる。
```blocks
input.onGesture(Gesture.Shake, function () {
    strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
    strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Orange))
    strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Yellow))
    strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Green))
    strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Blue))
    strip.setPixelColor(5, neopixel.colors(NeoPixelColors.Indigo))
    strip.setPixelColor(6, neopixel.colors(NeoPixelColors.Purple))
    strip.setPixelColor(7, neopixel.colors(NeoPixelColors.White))
    strip.show()
    for (let index = 0; index < 4; index++) {
       
    }
})
```

## ライトウェーブ6
追加した  ``||loops:くりかえし（4）回||`` の中に ``||neopixel:NeoPixel||``　の ``||neopixel:strip に設定されている色をLED（1）個分ずらす（ひとまわり）||`` と``||neopixel:strip を設定した色で点灯する||`` をいれる。

```blocks
input.onGesture(Gesture.Shake, function () {
    strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
    strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Orange))
    strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Yellow))
    strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Green))
    strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Blue))
    strip.setPixelColor(5, neopixel.colors(NeoPixelColors.Indigo))
    strip.setPixelColor(6, neopixel.colors(NeoPixelColors.Purple))
    strip.setPixelColor(7, neopixel.colors(NeoPixelColors.White))
    strip.show()
    for (let index = 0; index < 4; index++) {
        strip.rotate(1)
        strip.show()
    }
})
let strip: neopixel.Strip = null
```
## ライトウェーブ7
追加した  ``||loops:くりかえし（4）回||`` の中の一番下に、``||basic:一時停止（ミリ秒） 100||`` をいれ、「100」 を「200」にかえる。

```blocks
input.onGesture(Gesture.Shake, function () {
    strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
    strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Orange))
    strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Yellow))
    strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Green))
    strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Blue))
    strip.setPixelColor(5, neopixel.colors(NeoPixelColors.Indigo))
    strip.setPixelColor(6, neopixel.colors(NeoPixelColors.Purple))
    strip.setPixelColor(7, neopixel.colors(NeoPixelColors.White))
    strip.show()
    for (let index = 0; index < 4; index++) {
        strip.rotate(1)
        strip.show()
        basic.pause(200)
    }
})
let strip: neopixel.Strip = null
```
## ライトウェーブ4 テスト @showdialog
ここまででのプログラムです。

```blocks
input.onGesture(Gesture.Shake, function () {
    strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Yellow))
    strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Green))
    strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Blue))
    strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Violet))
    strip.show()
    for (let index = 0; index < 4; index++) {
        strip.rotate(1)
        strip.show()
        basic.pause(500)
    }
})
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 4, NeoPixelMode.RGB)
```

## ライトウェーブ4 テスト 
ここまでできたら、micro:bit にダウンロードして実際に動かしてみましょう。
光の色が動くことを確認できたら、色を変えたり、動くスピードを変えて自由に光らせてみよう。

## 💡 点滅（交互に光る）@showdialog

次の３つのプログラムは交互にLEDを光らせるプログラムです。
プログラムを理解したら、どれか１つを実際に打ち込んでみてください。

### 参考：ひとつおきに、を交互に光らせる。（ひとつずつ、色を決める。）

![交互点滅のイメージ](https://www.kodai.uec.ac.jp/sk/make-code/np/img_blink_uecsc.png)

```blocks
input.onGesture(Gesture.ScreenDown, function () {
    for (let index = 0; index < 10; index++) {
        strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Blue))
        strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Black))
        strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Blue))
        strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Black))
        strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Blue))
        strip.setPixelColor(5, neopixel.colors(NeoPixelColors.Black))
        strip.setPixelColor(6, neopixel.colors(NeoPixelColors.Blue))
        strip.setPixelColor(7, neopixel.colors(NeoPixelColors.Black))
        strip.show()
        basic.pause(200)
        strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Black))
        strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Blue))
        strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Black))
        strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Blue))
        strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Black))
        strip.setPixelColor(5, neopixel.colors(NeoPixelColors.Blue))
        strip.setPixelColor(6, neopixel.colors(NeoPixelColors.Black))
        strip.setPixelColor(7, neopixel.colors(NeoPixelColors.Blue))
        strip.show()
        basic.pause(200)
    }
})
let strip: neopixel.Strip = null
```

```blocks
input.onGesture(Gesture.ScreenDown, function () {
    for (let index = 0; index < 10; index++) {
        for (let カウンター = 0; カウンター <= 7; カウンター++) {
            if (カウンター % 2 == 0) {
                strip.setPixelColor(カウンター, neopixel.colors(NeoPixelColors.Blue))
            } else {
                strip.setPixelColor(カウンター, neopixel.colors(NeoPixelColors.Black))
            }
        }
        strip.show()
        basic.pause(200)
        for (let カウンター = 0; カウンター <= 7; カウンター++) {
            if (カウンター % 2 == 1) {
                strip.setPixelColor(カウンター, neopixel.colors(NeoPixelColors.Blue))
            } else {
                strip.setPixelColor(カウンター, neopixel.colors(NeoPixelColors.Black))
            }
        }
        strip.show()
        basic.pause(200)
    }
})
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 8, NeoPixelMode.RGB)
```

```blocks
input.onGesture(Gesture.ScreenDown, function () {
    for (let カウンター = 0; カウンター <= 7; カウンター++) {
        if (カウンター % 2 == 0) {
            strip.setPixelColor(カウンター, neopixel.colors(NeoPixelColors.Blue))
        } else {
            strip.setPixelColor(カウンター, neopixel.colors(NeoPixelColors.Black))
        }
    }
    for (let index = 0; index < 20; index++) {
        strip.show()
        basic.pause(200)
        strip.rotate(1)
    }
})
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 8, NeoPixelMode.RGB)
```
## 💡 点滅（交互に光る）

点滅するプログラムを作成してみましょう。
💡 をクリックすると、３番目のプログラムが確認できます。
プログラムが完成したら、micro:bit にダウンロードして実際に動かしてみてください。

```blocks
input.onGesture(Gesture.ScreenDown, function () {
    for (let カウンター = 0; カウンター <= 7; カウンター++) {
        if (カウンター % 2 == 0) {
            strip.setPixelColor(カウンター, neopixel.colors(NeoPixelColors.Blue))
        } else {
            strip.setPixelColor(カウンター, neopixel.colors(NeoPixelColors.Black))
        }
    }
    for (let index = 0; index < 20; index++) {
        strip.show()
        basic.pause(200)
        strip.rotate(1)
    }
})
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 8, NeoPixelMode.RGB)
```


## 🌈 発展：色を自由に決める@showdialog
ここまで、ブロックに登録されている色を選んで色を決めてきましたが、色を「赤・緑・青（RGB）」の三原色の組み合わせで自由に指定できます。
RGBはそれぞれ0から255までの数値で光の強さを表し、三つの光を同時に混ぜることで一つの色を作ります。
たとえば、赤だけを最大値にすると(255,0,0)で純粋な赤、赤と緑を混ぜると(255,255,0)で黄色になります。
青を弱めると紫、すべて同じ値にすると白やグレーになります。
この仕組みにより、単に「赤」「青」と決まった色を選ぶだけでなく、自分の好きな色や明るさを細かく調整できます。プログラムの中で数値を変えれば、点滅するたびに色が変わるようなアニメーションも作れるため、表現の幅が大きく広がります。

![色](https://www.kodai.uec.ac.jp/sk/make-code/np/img_color.png)

### サンプルプログラム
```blocks
input.onButtonPressed(Button.B, function () {
    n = 255/ 7
    for (let カウンター = 0; カウンター <= 7; カウンター++) {
        strip.setPixelColor(カウンター, neopixel.rgb(0 + n * カウンター, 255 - n * カウンター, 255))
    }
    strip.show()
})
let n = 0
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 8, NeoPixelMode.RGB)
```
## 発展：色を自由にきめる

サンプルプログラムを参考に、RGBを指定してLEDの色を決めて光らせるプログラムを作成してみてください。
RGBのブロックは、``||neopixel:neopixel||``の ``||neopixel:...その他||``にあります。
💡 をクリックすると、前のページのサンプルと、Aボタンを押した時にstrip全体に青が点灯するプログラムが見られます。


```blocks
input.onButtonPressed(Button.A, function () {
    strip.showColor(neopixel.rgb(0, 0, 255))
})
input.onButtonPressed(Button.B, function () {
    n = 255 / 7
    for (let カウンター = 0; カウンター <= 7; カウンター++) {
        strip.setPixelColor(カウンター, neopixel.rgb(0 + n * カウンター, 255 - n * カウンター, 255))
    }
    strip.show()
})
let n = 0
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 8, NeoPixelMode.RGB)
```
## 4. もっと工夫しよう（自由な活動・15分）@showdialog

さいごは、じぶんのすきな色や光りかたをつかって、じゆうにあそんでみよう！

たとえば…

🔄「じゅんばんに色がかわるライト」 　→ 赤→青→みどり→黄色…と、色がながれるように光らせるよ！

🎵「おんがくにあわせて光るライト」 　→ すきなうたにあわせて、ピカピカ光るようにしてみよう！

💬「メッセージライト」 　→ うれしい気もちのときはピンク、がんばるぞ！のときは赤など、気もちを色であらわしてみよう！

🌀「まほうのライト」 　→ ボタンをおすと、ひみつの色が出てくる！どんな色になるかはおたのしみ♪

自由に色やうごきをえらんで、オリジナルのライトをつくると、まるで光のアーティストみたい✨ 作品を見せあったり、いっしょにアイデアを出しあって、いろいろな表現にチャレンジしてください！

![子どもたちが活動している](https://www.kodai.uec.ac.jp/sk/make-code/np/img_presentation.png)

---

## 5. まとめ（5分）

* 今日できたこと：

  * NeoPixelを「つないだ」
  * 色を「自由に変えた」
  * 「順番や点滅」で動きを作った
  * オリジナルパターンを作った
* 次の発展例：

  * LEDを増やして光らせる
  * 音やセンサーと組み合わせる

![まとめのイラスト](https://www.kodai.uec.ac.jp/sk/make-code/np/img_summary.png)

<script src="https://cdn.jsdelivr.net/gh/jp-rad/pxt-ubit-extension@0.5.0/.github/statics/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", ["neopixel=github:microsoft/pxt-neopixel",]);</script>

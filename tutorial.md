# micro:bit × NeoPixel（4球 I型）チュートリアル# micro:bit × NeoPixel（8球 I型）チュートリアル
```package
neopixel=github:microsoft/pxt-neopixel
keypad=github:lioujj/pxt-keypad
```

## keypadを利用してライトバーの色を変えよう@showdialog
この活動では、「カラフル・ライトバーをつくろう」で学習したLEDとkeypad を組み合わせて、指定した色に切り替えるプログラムを作ってみよう」

<!--![メインイメージ](https://www.kodai.uec.ac.jp/sk/make-code/np/img_neopixel.png)-->

---

## 1. 接続しよう1@showdialog

まず、テープLED と keypad を micro:bit に接続しましょう。

**配線1**
- micro:bit → テープLED（NeoPixel）  
  - 3V → +5V
  - P12 → DIN
  - GND → GND

👉 接続部分を上にして左から+5V, DIN, GND。（黄色の線は信号、赤/白はモジュールごとに違うので注意‼）。  

![配線図１](https://www.kodai.uec.ac.jp/sk/make-code/np/img_wiring_uecsc.png)
  写真では、真ん中の線（DIN）をP0に接続するように書いてありますが、P12に接続してください。

## 1. 接続しよう2 @showdialog

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
 

## 1. 接続しよう2（キーパッドの初期化） @showdialog
キーパッドを接続したら、``||keypad:KeyPad||``にある``||keypad:set 4*4 KeyPad〜||``を``||basic:最初だけ||`` にセットして、次のようにセットします。

  - pin1（R1）→ P0
  - pin2（R2）→ P1
  - pin3（R3）→ P2
  - pin4（R4）→ P8
  - pin5（C1）→ P13
  - pin6（C2）→ P14
  - pin7（C3）→ P15
  - pin8（C4）→ P16

```blocks

keypad.setKeyPad4(
DigitalPin.P0,
DigitalPin.P1,
DigitalPin.P2,
DigitalPin.P8,
DigitalPin.P13,
DigitalPin.P14,
DigitalPin.P15,
DigitalPin.P16
)

```

## テープLEDを光らせよう1　LEDの個数の設定
1. テープLEDの点灯テスト

はじめに、テープLEDを光らせるテストをします。
``||neopixel: NeoPixel ||`` にある ``||variables:変数 strip を〜||``を``||basic:最初だけ||``にいれて``||neopixel: 端子P0に接続しているLED24個の〜 ||``の「24」を「8」にかえます。  

   ```blocks
   let strip = neopixel.create(DigitalPin.P12, 8, NeoPixelMode.RGB)
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
strip = neopixel.create(DigitalPin.P12, 8, NeoPixelMode.RGB)
mode = 0
let color = ""
basic.forever(function () {
	
})

```
##  2.状態（モード）の設置（テスト） 
micro:bit にダウンロードして実際に動かしてみましょう。
A ボタンを押すことで、モードの表示が切り替わることが確認できたら、次へ進みましょう。

## 3.キー入力を受け取る @showdialog
待機モード(0)と入力受付モード(1)の切り替えができたら、入力受付モードの時に、
ードが「入力受付モード」になったら、``||basic:ずっと||`` の中でキー入力を受け付けるようにします。
つまり、モードが「入力受付モード（``||variables:mode=1||``）」の時だけ、キー操作による入力処理が実行されるようにします。

キーパッドから受け取った数は、変数 **color** に代入するようプログラムをします。
ここで受け取った数は、文字列型で渡されるので、必要に応じて、数値に変換して利用します。


## 3.キー入力を受け取る（変数の作成）
``||variables:変数||`` の``||variables:変数を追加する...||``で、新しい変数 **color** を作成します。
そして、最初だけに ``||variables:変数 mode を 0 にする||`` をセットして、``||advanced:高度なブロック||``の``||text:文字列||``の一番上にある``||text:" "||``をセットして、半角の1を書き入れます。
（1は文字列として扱われます。）

```blocks
let color = "1"
```

## 3.キー入力を受け取る（入力の受付1）
``||basic:ずっと||`` に、``||logic:論理||``にあるフォークの形の``||logic:もし〜なら||``ブロックをセットして、
条件の部分を``||variables:mode||`` =  1　とします。

```blocks
basic.forever(function () {
    if (mode == 1) {
    	
    } else {
    	
    }
})
```

## 3.キー入力を受け取る（入力の受付2）
``||logic:もし〜なら||``ブロックの ``||variables:mode||`` =  1　の下に、``||variables:colorを（　）にする||``をセットします。 

```blocks
basic.forever(function () {
    if (mode == 1) {
        color = 0
    } else {
    	
    }
})

```

## 3.キー入力を受け取る（入力の受付3）
``||variables:colorを 0 にする||`` の 0 の部分に、``||keypad:KeyPad value(string)||``をいれます。
代入のブロックの後に、``||basic:一時停止（ミリ秒）||``を入れます。時間は300ミリ秒にしてください。


```blocks
basic.forever(function () {
    if (mode == 1) {
        color = keypad.getKeyString()
        basic.pause(300)
    } else {
    	
    }
})

```

## 3.キー入力を受け取る（入力の受付4）
``||basic:一時停止（ミリ秒）||``の後に、``||basic:文字列を表示（　）||`` に ``||variables:color||`` をセットして代入した文字列を表示します。


```blocks
basic.forever(function () {
    if (mode == 1) {
        color = keypad.getKeyString()
        basic.pause(300)
        basic.showString(color)
    } else {
    	
    }
})

```

## 3.キー入力を受け取る（テスト） @showdialog
ここまでのプログラムです。
キー入力の後に一時停止を入れるのは、連続して同じ入力が何度も処理されてしまうのを防ぐためです。

micro:bitなどではループがとても速く回るため、ボタンが押されたままの一瞬の間にも、同じ入力が何十回も検出されてしまいます。
少し待ち時間を入れることで、**「1回の押下＝1回の入力」**として安定した動作にできます。

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
strip = neopixel.create(DigitalPin.P12, 8, NeoPixelMode.RGB)
mode = 0
let color = "1"
basic.forever(function () {
    if (mode == 1) {
        color = keypad.getKeyString()
        basic.pause(300)
        basic.showString(color)
    } else {
    	
    }
})
```

## 3.キー入力を受け取る（テスト） 
ここまでできたら、micro:bit にダウンロードして実際に動かしてみましょう。
キーパッドは、平らなところにおいて、ゆっくり押さえるようにしてください。


## 4. LEDを光らせる @showdialog

ここでは、入力受付モードで入力した値（変数 color）が確定したら、LEDを点灯するプログラムを作ります。

（ボタン操作についての確認）
- これまでに、モードが「入力受付モード」のときにキー入力ができるようになりました。
- 入力した数字（例：1, 2, 3）を color に保存します。
- colorの表示をしたら、color の値に応じてLEDの色を変えて点灯します。

💡 ポイント：入力（キーパッド）を終えて、画面で色番号を確認したら点灯のコマンドを実行します。


## 4. LEDを光らせる１
``||basic:ずっと||`` の``||logic:もし〜なら||``ブロックの**mode=1**の一番下に、
新しく``||logic:もし〜なら||``ブロック（フォークみたいな形のもの）を追加してます。
左下にある ** + ** を２回押して、条件を３種類かけるように増やします。

```blocks
basic.forever(function () {
    if (mode == 1) {
        color = keypad.getKeyString()
        basic.pause(300)
        basic.showString(color)
        if (true) {
        	
        } else if (false) {
        	
        } else if (false) {
        	
        } else {
        	
        }
    } else {
    	
    }
})
let strip: neopixel.Strip = null
```

## 4. Aボタンで決定してLEDを光らせる2
新しく追加した``||logic:もし〜なら||`` ブロックの最初の条件が ** color = 1 ** となるようにして、
``||neopixel:stripを赤色に点灯する||``をセットしてます。その後、``||variables:変数 mode を（）||``にするブロックを使って、``||variables:mode||`` を 0にします。


```blocks
basic.forever(function () {
    if (mode == 1) {
        color = keypad.getKeyString()
        basic.pause(300)
        basic.showString(color)
        if (color == "1") {
            strip.showColor(neopixel.colors(NeoPixelColors.Red))
            mode = 0
        } else if (false) {
        	
        } else if (false) {
        	
        } else {
        	
        }
    } else {
    	
    }
})
let strip: neopixel.Strip = null
```

## 4. Aボタンで決定してLEDを光らせる2
新しく追加した``||logic:もし〜なら||`` ブロックの最初の条件が ** color = 2 ** ,** color = 3** の場合も同様にして、それぞれ、青、白でLEDを点灯して、``||variables:mode||``を0にします。

```blocks
basic.forever(function () {
    if (mode == 1) {
        color = keypad.getKeyString()
        basic.pause(300)
        basic.showString(color)
        if (color == "1") {
            strip.showColor(neopixel.colors(NeoPixelColors.Red))
            mode = 0
        } else if (color == "2") {
            strip.showColor(neopixel.colors(NeoPixelColors.Blue))
            mode = 0
        } else if (color == "3") {
            strip.showColor(neopixel.colors(NeoPixelColors.White))
            mode = 0
        } else {
        	
        }
    } else {
    	
    }
})
let strip: neopixel.Strip = null
```


## 4. LEDを光らせる4
**mode=1**の下に新しく追加した``||logic:もし〜なら||``ブロックの一番うえの ``||logic:(　)=(　)||`` をあてはめ、
右辺に ``||text:テキスト||``にある``||text:("　")||``をセットして、**""**の間に**1**を書き入れます。
その後、左辺に ``||variables:変数||``から``||variables:color||``をセットします。

```blocks
input.onButtonPressed(Button.A, function () {
    if (mode == 0) {
        mode = 1
        basic.showNumber(mode)
        strip.showColor(neopixel.colors(NeoPixelColors.Red))
    } else if (mode == 1) {
        if (color == "1") {
        	
        } else if (false) {
        	
        } else if (false) {
        	
        }
        mode = 0
        basic.showNumber(mode)
        strip.showColor(neopixel.colors(NeoPixelColors.Black))
    } else {
    	
    }
})
let strip: neopixel.Strip = null
```

## 4. Aボタンで決定してLEDを光らせる5
**color="1"** と同様に、 **color="2"** と**color="3"** について、それぞれ、青色、白色でLEDをつけるようにプログラムします。

```blocks
input.onButtonPressed(Button.A, function () {
    if (mode == 0) {
        mode = 1
        basic.showNumber(mode)
        strip.showColor(neopixel.colors(NeoPixelColors.Black))
    } else if (mode == 1) {
        if (color == "1") {
            strip.showColor(neopixel.colors(NeoPixelColors.Red))
        } else if (color == "2") {
            strip.showColor(neopixel.colors(NeoPixelColors.Blue))
        } else if (color == "3") {
            strip.showColor(neopixel.colors(NeoPixelColors.White))
        }
        mode = 0
        basic.showNumber(mode)
    } else {
    	
    }
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
strip = neopixel.create(DigitalPin.P12, 8, NeoPixelMode.RGB)
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

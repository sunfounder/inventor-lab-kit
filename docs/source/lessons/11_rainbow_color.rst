.. note::

    こんにちは、SunFounderのRaspberry Pi & Arduino & ESP32愛好者コミュニティへようこそ！Facebookでさらに深くRaspberry Pi、Arduino、ESP32を楽しみましょう。同じ興味を持つ仲間と一緒に学び、共有しましょう。

    **なぜ参加するのか？**

    - **専門的なサポート**: 購入後の問題や技術的な課題をコミュニティと私たちのチームがサポートします。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **限定プレビュー**: 新製品の発表や先行プレビューに早くアクセスできます。
    - **特別割引**: 最新の製品に対して特別な割引を受けられます。
    - **フェスティバルプロモーションとプレゼント**: プレゼントやホリデープロモーションに参加しましょう。

    👉 一緒に探求し、創造しましょう！[|link_sf_facebook|]をクリックして、今すぐ参加してください！

11. 虹の色彩
=======================================
光で絵を描くことを想像してみてください。赤、緑、青を混ぜ合わせて、あらゆる色合いを作り出すことができます。まるでパレット上の絵の具を混ぜ合わせるように、光のビームで色を作り出すのです。

.. .. image:: img/12_rgb_mix.png
..     :width: 300
..     :align: center

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/11_rainbow_color.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンでは、RGB LEDの魅力的な世界を探求し、基本色の組み合わせがどのようにして豊かな色彩のスペクトルを生み出すかを学びます。この実践的なコースは、RGB LEDの機能の原理を理解し、プログラミングと回路作成の実際の応用を紹介します。

このレッスンで学ぶこと：

* RGB LEDの動作原理を理解する
* コード内で関数を作成し、タスクを簡素化し、可読性を向上させる方法を学ぶ
* RGB LEDを操作して、さまざまな色の組み合わせが与える影響を探る
* パルス幅変調（PWM）を使用して、RGB LEDで繊細な色の混合を行う
* Arduinoでパラメータを受け取る関数を作成し、コードの効率と明確さを向上させる

回路の構築
-----------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB LED
     - 3 * 220Ω 抵抗器
     - ジャンパーワイヤー
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - 1 * マルチメーター
     -
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter|
     -

**手順に従った構築方法**

配線図または以下の手順に従って回路を構築します。

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

1. まず、RGB LEDから始めましょう。

RGB LEDは、赤、緑、青のLEDを1つのパッケージに統合し、さまざまな色を発光します。この3つのピンに供給される電圧を調整することで、最大16,777,216色を作り出すことができます。

.. image:: img/12_mix_color_rgb.png
    :width: 400
    :align: center

RGB LEDは設計により、共通アノードまたは共通カソードのいずれかになります。このプロジェクトでは、 **共通カソード** のRGB LEDを使用します。このLEDでは、3つのLEDがすべて負極を共有しています。

* 共通カソードRGB LEDは、負極を共有しています。
* 共通アノードRGB LEDは、正極を共有しています。

.. image:: img/12_rgb_cc_ca.jpg
    :width: 600
    :align: center

通常、RGB LEDには4つのピンがあり、最も長いピンがグランドです。RGB LEDを配置する際は、最も長いリードが左から2番目になるように配置し、ピンを左から右に向かって赤、GND、緑、青とします。

.. image:: img/12_mix_color_rgb_1.jpg
    :width: 200
    :align: center

ダイオードテストモードのマルチメーターを使用して、各ピンが発光する色を識別することもできます。

マルチメーターを **Continuity** 設定にセットして、抵抗を測定します。

.. image:: img/multimeter_diode_measure.png
    :width: 300
    :align: center

RGB LEDの最も長いピンにマルチメーターの黒いリードを接触させ、他のピンに赤いリードを個別に接触させます。これにより、赤、緑、青のいずれかの色でLEDが点灯するのを確認できます。

.. image:: img/12_mix_color_measure_pin.png
    :width: 500
    :align: center

2. RGB LEDを、最も長いピンを穴17Dに、他の3つのピンをそれぞれ18C、16C、15Cに挿入して、ブレッドボードに配置します。

.. image:: img/12_mix_color_bb_1.png
    :width: 500
    :align: center

3. 3つの220Ωの抵抗器を、穴15Eから15G、16Eから16G、18Eから18Gの位置に挿入します。

.. image:: img/12_mix_color_bb_2.png
    :width: 500
    :align: center

4. これらの抵抗器を、ジャンパーワイヤーを使ってArduino Uno R3のピン9、10、11に接続します。

.. image:: img/12_mix_color_bb_3.png
    :width: 500
    :align: center

5. RGB LEDの最も長いピンを、ジャンパーワイヤーを使ってブレッドボードの負極レールに接続します。

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

コード作成 - RGB LEDを点灯させる
----------------------------------------
1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して、新しいプロジェクトを開始します。
2. スケッチを ``Lesson11_Rainbow_Color`` として保存し、 ``Ctrl + S`` または「保存」をクリックして保存します。

3. RGB LEDの3つのピンを保存するための変数を作成し、それらをOUTPUTとして設定します。

.. code-block:: Arduino

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // ここに一度だけ実行するセットアップコードを記述します:
        pinMode(bluePin, OUTPUT);   // RGB LEDのブルーピンを出力に設定
        pinMode(greenPin, OUTPUT);  // RGB LEDのグリーンピンを出力に設定
        pinMode(redPin, OUTPUT);  // RGB LEDのレッドピンを出力に設定
    }

    void loop() {
        // ここに繰り返し実行するメインコードを記述します:
    }

4. 次に、 ``void loop()`` 関数内で、RGB LEDのレッドピンを ``HIGH`` に設定し、他の2つのピンを ``LOW`` に設定します。

.. note::

    9、10、および11のPWMピンを使用しているため、 ``digitalWrite()`` または ``analogWrite()`` を使用して高または低のレベルを出力することができます。
    
    このレッスンでは、ピンを単に高低に設定するだけなので、 ``digitalWrite()`` を使用します。

.. code-block:: Arduino
    :emphasize-lines: 10-12

    void setup() {
        // ここに一度だけ実行するセットアップコードを記述します:
        pinMode(bluePin, OUTPUT);   // RGB LEDのブルーピンを出力に設定
        pinMode(greenPin, OUTPUT);  // RGB LEDのグリーンピンを出力に設定
        pinMode(redPin, OUTPUT);  // RGB LEDのレッドピンを出力に設定
    }

    void loop() {
        // ここに繰り返し実行するメインコードを記述します:
        digitalWrite(bluePin, LOW);    // RGB LEDのブルーピンをオフにする
        digitalWrite(greenPin, LOW);   // RGB LEDのグリーンピンをオフにする
        digitalWrite(redPin, HIGH);  // RGB LEDのレッドピンをオンにする
    }

5. コードを保存し、「アップロード」をクリックしてArduino Uno R3に送信します。どうなるか見てみましょう。

6. RGB LEDが赤色に点灯するのが見えます。しかし、緑と青も点灯させたい場合はどうすればいいでしょうか？コードをどのように変更すればよいでしょうか？

次に、3つの ``digitalWrite()`` コマンドを2回コピーして、それぞれのピンを表示したい色に対応して ``HIGH`` に設定し、他のピンを ``LOW`` に設定します。各色が点灯するたびに1秒間待つようにしましょう。

.. code-block:: Arduino
    :emphasize-lines: 17-25

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // ここに一度だけ実行するセットアップコードを記述します:
        pinMode(bluePin, OUTPUT);   // RGB LEDのブルーピンを出力に設定
        pinMode(greenPin, OUTPUT);  // RGB LEDのグリーンピンを出力に設定
        pinMode(redPin, OUTPUT);  // RGB LEDのレッドピンを出力に設定
    }

    void loop() {
        // ここに繰り返し実行するメインコードを記述します:
        digitalWrite(bluePin, LOW);    // RGB LEDのブルーピンをオフにする
        digitalWrite(greenPin, LOW);   // RGB LEDのグリーンピンをオフにする
        digitalWrite(redPin, HIGH);  // RGB LEDのレッドピンをオンにする
        delay(1000);              // 1秒待機
        digitalWrite(bluePin, LOW);    // RGB LEDのブルーピンをオフにする
        digitalWrite(greenPin, HIGH);  // RGB LEDのグリーンピンをオンにする
        digitalWrite(redPin, LOW);   // RGB LEDのレッドピンをオフにする
        delay(1000);              // 1秒待機
        digitalWrite(bluePin, HIGH);   // RGB LEDのブルーピンをオンにする
        digitalWrite(greenPin, LOW);   // RGB LEDのグリーンピンをオフにする
        digitalWrite(redPin, LOW);   // RGB LEDのレッドピンをオフにする
        delay(1000);              // 1秒待機
    }

7. コードを再度アップロードして効果を確認しましょう。RGB LEDが赤、緑、青の順に点灯するのがわかるでしょう。

**質問**:

1. 他の色を作りたい場合はどうすればよいでしょうか？以下の図を参照し、アイデアを手帳に記入してください。

.. image:: img/12_rgb_mix.png
    :width: 300
    :align: center

.. list-table::
   :widths: 20 20 20 20
   :header-rows: 1

   * - 色
     - 赤ピン
     - 緑ピン
     - 青ピン
   * - 赤
     - *HIGH*
     - *LOW*
     - *LOW*
   * - 緑
     - *LOW*
     - *HIGH*
     - *LOW*
   * - 青
     - *LOW*
     - *LOW*
     - *HIGH*
   * - 黄
     -
     -
     -
   * - ピンク
     -
     -
     -
   * - シアン
     - 
     -
     -
   * - 白
     -
     -
     -

コード作成 - 色の表示
------------------------------------

RGB LEDの制御をマスターするための旅で、 ``digitalWrite()`` を使用して基本的な色を点灯させる方法を学びました。次に、RGB LEDが生成できる全色域を探索し、PWM（パルス幅変調）信号を送信するために ``analogWrite()`` を使用することで、さまざまな色を実現する方法を学びます。

これをコードで実装する方法を見てみましょう。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して、新しいプロジェクトを開始します。
2. スケッチを ``Lesson11_PWM_Color_Mixing`` として保存し、 ``Ctrl + S`` または「保存」をクリックして保存します。

3. RGB LEDの3つのピンを保存するための変数を作成し、それらをOUTPUTとして設定します。

.. code-block:: Arduino

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // 一度だけ実行するセットアップコード:
        pinMode(bluePin, OUTPUT);   // RGB LEDのブルーピンを出力に設定
        pinMode(greenPin, OUTPUT);  // RGB LEDのグリーンピンを出力に設定
        pinMode(redPin, OUTPUT);  // RGB LEDのレッドピンを出力に設定
    }

4. ``analogWrite()`` を使用してRGB LEDにPWM値を送信します。レッスン9で学んだように、PWM値はLEDの明るさを変えることができ、PWM範囲は0〜255です。赤を表示するには、RGB LEDのレッドピンのPWM値を255に設定し、他の2つのピンを0に設定します。

.. code-block:: Arduino
    :emphasize-lines: 14-16

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // 一度だけ実行するセットアップコード:
        pinMode(bluePin, OUTPUT);   // RGB LEDのブルーピンを出力に設定
        pinMode(greenPin, OUTPUT);  // RGB LEDのグリーンピンを出力に設定
        pinMode(redPin, OUTPUT);  // RGB LEDのレッドピンを出力に設定
    }

    void loop() {
        // 繰り返し実行するメインコード:
        analogWrite(bluePin, 0);    // ブルーピンのPWM値を0に設定
        analogWrite(greenPin, 0);   // グリーンピンのPWM値を0に設定
        analogWrite(redPin, 255);  // レッドピンのPWM値を255に設定
    }

5. この設定で、コードをArduino Uno R3にアップロードすると、RGB LEDが赤色を表示します。

6. ``analogWrite()`` 関数を使用すると、RGB LEDは7つの基本色だけでなく、さまざまな色合いも表示できます。9、10、11のピンの値を個別に調整し、観察した色を手帳に記録してください。

.. list-table::
    :widths: 20 20 20 40
    :header-rows: 1

    *   - レッドピン    
        - グリーンピン  
        - ブルーピン
        - 色
    *   - 0
        - 128
        - 128
        - 
    *   - 128
        - 0
        - 255
        - 
    *   - 128
        - 128
        - 255
        - 
    *   - 255
        - 128
        - 0
        -     

コード作成 - パラメータ化された関数
------------------------------------------------

異なる色を表示するために ``analogWrite()`` 関数を使用すると、同時に多くの色を表示したい場合、コードが長くなることがあります。したがって、関数を作成する必要があります。

前のレッスンとは異なり、今回はパラメータを持つ関数を作成する準備をしています。

パラメータ化された関数を使用すると、特定の値を関数に渡し、その値を使用してタスクを実行できます。これにより、色の強度などのプロパティを動的に調整することができ、コードが柔軟で読みやすくなります。

パラメータ化された関数を定義する際には、関数名の後にかっこ内に必要なパラメータを指定します。これらのパラメータは、関数が呼び出されたときに実際の値に置き換えられるプレースホルダとして機能します。

以下は、RGB LEDの色を設定するためのパラメータ化された関数を定義する方法です。

1. 以前保存したスケッチ ``Lesson11_PWM_Color_Mixing`` を開き、「ファイル」メニューから「名前を付けて保存」を選択し、 ``Lesson11_PWM_Color_Mixing_Function`` に名前を変更します。保存をクリックします。

2. ``void loop()`` の後に ``void`` キーワードを使用して関数を宣言し、関数名とパラメータをかっこ内に記述します。 ``setColor`` 関数には、RGB LEDの各色成分の強度を表す3つのパラメータ（ ``red`` 、 ``green`` 、 ``blue`` ）を使用します。

.. code-block:: Arduino
    :emphasize-lines: 5,6

    void loop() {
        // 繰り返し実行するメインコードをここに記述します:
    }

    void setColor(int red, int green, int blue) {
    }

   
3. 関数の本体内で、 ``analogWrite()`` コマンドを使用してRGB LEDのピンにPWM信号を送信します。 ``setColor`` に渡された値が各色の明るさを決定します。ここで使用するパラメータ ``red`` 、 ``green`` 、 ``blue`` は、各LEDピンの強度を直接制御します。

.. code-block:: Arduino

    // RGB LEDの色を設定する関数
    void setColor(int red, int green, int blue) {
        // 赤、緑、青のPWM値をRGB LEDに書き込む
        analogWrite(redPin, red);
        analogWrite(greenPin, green);
        analogWrite(bluePin, blue);
    }

4. 作成した ``setColor()`` 関数を ``void loop()`` 内で呼び出すことができます。パラメータを持つ関数を作成したので、 ``(255, 0, 0)`` のように引数を ``()`` 内に入力する必要があります。コメントを記述することを忘れないでください。

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        // 繰り返し実行するメインコードをここに記述します:
        setColor(255, 0, 0); // 赤色を表示
    }

    // RGB LEDの色を設定する関数
    void setColor(int red, int green, int blue) {
        // 赤、緑、青のPWM値をRGB LEDに書き込む
        analogWrite(redPin, red);
        analogWrite(greenPin, green);
        analogWrite(bluePin, blue);
    }

5. RGB LEDの3つのピンに異なる値を提供することで、異なる色の光を点灯できることはすでにわかっています。では、RGB LEDをどのようにして正確に希望の色に点灯させるのでしょうか？これにはカラーパレットが必要です。 **ペイント** （Windowsに付属しているソフトウェア）や、個人のコンピュータにインストールされている任意の描画ソフトウェアを開いてください。

.. image:: img/13_mix_color_paint.png

6. 好きな色を選び、そのRGB値を記録してください。

.. note::

    色を選択する前に、輝度を適切な位置に調整することを忘れないでください。

.. image:: img/13_mix_color_paint_2.png

7. 選んだ色を ``void loop()`` の ``setColor()`` 関数に入力し、 ``delay()`` 関数を使用して各色の表示時間を指定します。

.. code-block:: Arduino

    void loop() {
        // 繰り返し実行するメインコードをここに記述します:
        setColor(255, 0, 0);      // 赤色を表示
        delay(1000);              // 1秒待機
        setColor(0, 128, 128);    // ティール色を表示
        delay(1000);              // 1秒待機
        setColor(128, 0, 255);    // 紫色を表示
        delay(1000);              // 1秒待機
        setColor(128, 128, 255);  // ライトブルー色を表示
        delay(1000);              // 1秒待機
        setColor(255, 128, 0);    // オレンジ色を表示
        delay(1000);              // 1秒待機
    }

8. 以下に完全なコードがあります。「アップロード」をクリックして、コードをArduino Uno R3にアップロードし、効果を確認してください。

.. code-block:: Arduino

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // 一度だけ実行するセットアップコード:
        pinMode(bluePin, OUTPUT);   // RGB LEDのブルーピンを出力に設定
        pinMode(greenPin, OUTPUT);  // RGB LEDのグリーンピンを出力に設定
        pinMode(redPin, OUTPUT);  // RGB LEDのレッドピンを出力に設定
    }

    void loop() {
        // 繰り返し実行するメインコードをここに記述します:
        setColor(255, 0, 0);      // 赤色を表示
        delay(1000);              // 1秒待機
        setColor(0, 128, 128);    // ティール色を表示
        delay(1000);              // 1秒待機
        setColor(128, 0, 255);    // 紫色を表示
        delay(1000);              // 1秒待機
        setColor(128, 128, 255);  // ライトブルー色を表示
        delay(1000);              // 1秒待機
        setColor(255, 128, 0);    // オレンジ色を表示
        delay(1000);              // 1秒待機
    }

    // RGB LEDの色を設定する関数
    void setColor(int red, int green, int blue) {
        // 赤、緑、青のPWM値をRGB LEDに書き込む
        analogWrite(redPin, red);
        analogWrite(greenPin, green);
        analogWrite(bluePin, blue);
    }

9. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**まとめ**

一連のコーディング演習を通じて、RGB LEDの色を動的に変化させるスケッチを作成します。各色を制御するための基本的なコマンドから始め、関数を使用してコードをリファクタリングし、セットアップをよりモジュール化し、保守しやすくします。このアプローチにより、コードがよりクリーンになり、プログラミングにおける関数の重要性についても学ぶことができます。


.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！FacebookでRaspberry Pi、Arduino、ESP32に興味を持つ仲間たちと一緒に、さらに深く探求しましょう。

    **参加する理由は？**

    - **専門的なサポート**: コミュニティやチームの助けを借りて、販売後の問題や技術的な課題を解決できます。
    - **学び＆共有**: スキルを向上させるためのヒントやチュートリアルを交換できます。
    - **限定プレビュー**: 新製品の発表やスニークピークにいち早くアクセスできます。
    - **特別割引**: 最新製品に対して、特別な割引をお楽しみいただけます。
    - **イベントプロモーションとギブアウェイ**: ギブアウェイや季節のプロモーションに参加できます。

    👉 さあ、一緒に探求し、創造しましょう！[|link_sf_facebook|]をクリックして、今日から参加しましょう！

32. ストップウォッチ
=======================
このエキサイティングなプロジェクトでは、4桁の7セグメントディスプレイを使って機能的なストップウォッチを作成する方法を学びます。このレッスンの終わりまでに、複数桁の7セグメントディスプレイを制御する方法を理解し、分と秒を計測するシンプルなストップウォッチを構築できるようになります。デジタルディスプレイの世界に飛び込み、Arduinoのスキルを向上させましょう！

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/32.stopwatch.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンの終わりまでに、次のことができるようになります:

* 4桁の7セグメントディスプレイをマルチプレックス化する方法を学ぶ。
* 単一の桁に数字を表示するコードを書く。
* 数字のスクロール表示を作成する。
* 4桁の7セグメントディスプレイを使って分と秒を計測するストップウォッチを実装する。
* ``AND`` 演算子と ``>>`` 演算子を学ぶ。

4桁の7セグメントディスプレイを学ぶ
----------------------------------------

**はじめに**

1. 4桁の7セグメントディスプレイを見つけてください。

.. image:: img/32_stopwatch_4_digit.png
  :align: center

7セグメントディスプレイは、8の字型のコンポーネントで、7つのLEDをパッケージ化しています。ディスプレイ内の各LEDには位置セグメントが割り当てられ、その接続ピンの1つが長方形のプラスチックパッケージから引き出されています。このLEDピンは、それぞれの個別のLEDを表す"a"から"g"までのラベルが付けられています。

.. image:: img/32_stopwatch_7segment.png
  :align: center

* :ref:`learn_7segment`

4桁のディスプレイは、4つの7セグメントディスプレイを組み合わせたもので、それぞれが1桁を表しています。必要なピンの数を減らすために、各ディスプレイのセグメントはマルチプレックスされており、各セグメントピンが他のディスプレイの対応するセグメントピンに接続されています。

.. image:: img/32_stopwatch_common_pins.png
  :width: 800
  :align: center

これによりピン数は減りますが、制御の複雑さは増します。例えば、"a"ピンに電圧をかけると、すべての桁の"a"セグメントが点灯します。どの桁にセグメントを表示するかを制御するために、各桁には個別の制御ピン(d1~d4)があります。

.. image:: img/32_stopwatch_control_pins.png
  :width: 800
  :align: center

その結果、数字「2222」を表示するには、d1、d2、d3、d4に電圧をかける必要があります。すべてのディスプレイが桁を表示するので、入力a、b、d、e、g、dpにも電圧をかける必要があります。

.. image:: img/32_stopwatch_show_2.png
  :width: 800
  :align: center

**ピン配置**

一般的な4桁の7セグメントディスプレイには、各側面に6つずつ、合計12ピンがあります。

4つのピン（d1、d2、d3、およびd4）は、各桁を制御します。残りのピンはセグメントに対応しています。

.. image:: img/32_stopwatch_pins.png
  :width: 600
  :align: center

**コモンカソードまたはコモンアノード**

4桁の7セグメントディスプレイがコモンカソードかコモンアノードかを判断するには、マルチメータを使用します。また、次の手順でディスプレイの各セグメントが正常に動作しているかをテストすることもできます。

1. マルチメータをダイオードテストモードに設定します。ダイオードテストは、ダイオードや類似の半導体デバイス（LEDなど）の順方向伝導をチェックするために使用されるマルチメータの機能です。マルチメータはダイオードに微小電流を流します。ダイオードが正常であれば、電流を通過させます。

.. image:: img/multimeter_diode.png
    :width: 300
    :align: center

2. 4桁の7セグメントディスプレイをブレッドボードに挿入します。ディスプレイのピン **d1** と同じ行にワイヤを挿入し、それをマルチメータの黒いリードで接触させます。ディスプレイのピン **e** と同じ行にもう1本のワイヤを挿入し、それを赤いリードで接触させます。

.. image:: img/32_stopwatch_test_cathode.png
    :align: center
    :width: 500

3. いずれかのLEDセグメントが点灯するかどうかを確認します。点灯する場合、ディスプレイがコモンカソードであることを示しています。点灯しない場合、赤と黒のリードを入れ替えてください。入れ替え後にセグメントが点灯する場合、ディスプレイがコモンアノードであることを示しています。

.. note::

  私たちのキットには、コモンカソードの4桁7セグメントディスプレイが含まれています。制御ピンd1-d4をLOWに、セグメントピンa-gをHIGHに設定して動作させます。

**質問**

4桁の7セグメントディスプレイの左端の桁（d1）に「2」を表示したい場合、d1~d4およびa~gのピンのレベルはどうすればよいでしょうか？

.. image:: img/32_stopwatch_show_2d1.png
  :width: 800
  :align: center

.. list-table::
    :widths: 20 20 20 20
    :header-rows: 1

    *   - 7セグメントディスプレイ
        - HIGHまたはLOW
        - 7セグメントディスプレイ
        - HIGHまたはLOW
    *   - d1
        - 
        - a
        -  
    *   - d2
        - 
        - b
        - 
    *   - d3
        - 
        - c
        -   
    *   - d4
        - 
        - d
        - 
    *   - 
        - 
        - e
        - 
    *   - 
        - 
        - f
        - 
    *   - 
        - 
        - g
        - 
    *   - 
        - 
        - dp
        - 


回路の構築
------------------------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 4桁7セグメントディスプレイ
     - 4 * 220Ω抵抗
     - 1 * マルチメーター
   * - |list_uno_r3|
     - |list_4digit| 
     - |list_220ohm|
     - |list_meter|
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - 
     -   
   * - |list_usb_cable| 
     - |list_breadboard| 
     - 
     - 
    
**構築手順**

配線図に従って、または以下の手順に従って回路を構築してください。

.. image:: img/32_stopwatch_connect_ag.png
    :width: 500
    :align: center

1. 4桁7セグメントディスプレイをブレッドボードに挿入します。

.. image:: img/32_stopwatch_connect_4digit.png
    :width: 500
    :align: center

2. 4つの220Ω抵抗をブレッドボードに挿入します。

.. image:: img/32_stopwatch_connect_resistors.png
    :width: 500
    :align: center

3. 制御ピンd1を最初の抵抗の片側に接続します。抵抗のもう片側をArduino Uno R3のピン10に接続します。これにより、制御ピンd1が抵抗を介してピン10に接続されます。

.. image:: img/32_stopwatch_connect_d1.png
    :width: 500
    :align: center

4. 同様に、d2をピン11、d3をピン12、d4をピン13に接続します。

.. image:: img/32_stopwatch_connect_d1d3.png
    :width: 500
    :align: center
  
5. 次に、adpピンを配線表に従ってArduinoのピン2～9に接続します。

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 7セグメントディスプレイ
        - Arduino Uno R3
    *   - a
        - 2
    *   - b
        - 3 
    *   - c
        - 4
    *   - d
        - 5
    *   - e
        - 6
    *   - f
        - 7
    *   - g
        - 8
    *   - dp
        - 9

.. image:: img/32_stopwatch_connect_ag.png
    :width: 500
    :align: center

コードの作成 - 一桁に「2」を表示する
--------------------------------------------------

次に、4桁7セグメントディスプレイの一桁に数字を表示するコードを書いてみましょう。

1. Arduino IDEを開き、「ファイル」メニューから「新規スケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Lesson32_Show_2_One_Digit`` という名前で保存し、 ``Ctrl + S`` を押すか「保存」をクリックして保存します。

3. まず、4桁7セグメントディスプレイのセグメントピンと桁ピンを格納する2つの配列を作成します。

.. code-block:: Arduino

  // Define the pins of the segments and the digits on the 4-digit 7-segment display
  int segmentPins[] = { 2, 3, 4, 5, 6, 7, 8, 9 };  // Segments a~g and dp (decimal point)
  int digitPins[] = { 10, 11, 12, 13 };            // Digits d1-d4

4. ``void setup()`` 関数内で、すべてのピンを出力として設定します。この4桁7セグメントディスプレイはコモンカソードタイプなので、最初にすべてのセグメントピンを ``LOW`` 、すべての桁ピンを ``HIGH`` に設定してディスプレイをオフにします。

.. code-block:: Arduino

  void setup() {
    // Set all segment pins as output
    for (int i = 0; i < 8; i++) {
      pinMode(segmentPins[i], OUTPUT);
      digitalWrite(segmentPins[i], LOW);  // Ensure all segments are off initially
    }

    // Set all digit pins as output and turn them off (common cathode, so HIGH is off)
    for (int i = 0; i < 4; i++) {
      pinMode(digitPins[i], OUTPUT);
      digitalWrite(digitPins[i], HIGH);
    }
  }

5. ``loop()`` 関数内で、最初の桁（d1）を有効にするには、その状態を ``LOW`` に設定します。右端の桁（d4）を有効にする場合は、 ``0`` を ``3`` に変更してください。

.. code-block:: Arduino

  void loop() {
    digitalWrite(digitPins[0], LOW);     // Turn on first digit
  }

6. 数字「2」を表示するには、セグメントa、b、d、e、およびgを ``HIGH`` に設定します。これで数字「2」が表示されます。

.. code-block:: Arduino
  :emphasize-lines: 4-8

  void loop() {
    digitalWrite(digitPins[1], LOW);     // Turn on first digit
    
    digitalWrite(segmentPins[0], HIGH);  //Turn on segment a
    digitalWrite(segmentPins[1], HIGH);  //Turn on segment b
    digitalWrite(segmentPins[3], HIGH);  //Turn on segment d
    digitalWrite(segmentPins[4], HIGH);  //Turn on segment e
    digitalWrite(segmentPins[6], HIGH);  //Turn on segment g
  }

7. コードをArduino Uno R3ボードにアップロードすると、最初の桁に数字「2」が表示されます。

.. code-block:: Arduino

  // Define the pins of the segments and the digits on the 4-digit 7-segment display
  int segmentPins[] = { 2, 3, 4, 5, 6, 7, 8, 9 };  // Segments a~g and dp (decimal point)
  int digitPins[] = { 10, 11, 12, 13 };            // Digits d1-d4

  void setup() {
    // Set all segment pins as output
    for (int i = 0; i < 8; i++) {
      pinMode(segmentPins[i], OUTPUT);
      digitalWrite(segmentPins[i], LOW);  // Ensure all segments are off initially
    }

    // Set all digit pins as output and turn them off (common cathode, so HIGH is off)
    for (int i = 0; i < 4; i++) {
      pinMode(digitPins[i], OUTPUT);
      digitalWrite(digitPins[i], HIGH);
    }
  }

  void loop() {
    digitalWrite(digitPins[1], LOW);     // Turn on first digit
    
    digitalWrite(segmentPins[0], HIGH);  //Turn on segment a
    digitalWrite(segmentPins[1], HIGH);  //Turn on segment b
    digitalWrite(segmentPins[3], HIGH);  //Turn on segment d
    digitalWrite(segmentPins[4], HIGH);  //Turn on segment e
    digitalWrite(segmentPins[6], HIGH);  //Turn on segment g
  }

コード作成 - 1桁に数字をスクロール表示
-------------------------------------------------
前のプロジェクトでは、1桁に「2」を表示する方法を学びました。しかし、0から9までの数字をスクロール表示したい場合、同じ方法を使うと非常に長くなってしまいます。

レッスン28では、コモンカソードディスプレイでの数字0〜9のバイナリ、10進数、および16進数コードを学びました。

.. list-table::
    :widths: 20 40 30 30
    :header-rows: 1

    *   - 数字
        - バイナリ
        - 10進数
        - 16進数
    *   - 0
        - B00111111
        - 63
        - 0x3F
    *   - 1
        - B00000110
        - 6
        - 0x06
    *   - 2
        - B01011011
        - 91
        - 0x5B
    *   - 3
        - B01001111
        - 79
        - 0x4F
    *   - 4
        - B01100110
        - 102
        - 0x66
    *   - 5
        - B01101101
        - 109
        - 0x6D
    *   - 6
        - B01111101
        - 125
        - 0x7D
    *   - 7
        - B00000111
        - 7
        - 0x07
    *   - 8
        - B01111111
        - 127
        - 0x7F
    *   - 9
        - B01101111
        - 111
        - 0x6F

1桁に0から9の数字をスクロールさせる方法

1. 先ほど保存したスケッチ ``Lesson32_Show_2_One_Digit`` を開き、「ファイル」メニューから「名前を付けて保存...」を選択し、 ``Lesson32_Scroll_Numbers_One_Digit`` に名前を変更して保存します。

2. 数字0〜9のバイナリコードを ``numArray[]`` 配列に格納します。

.. code-block:: Arduino
  :emphasize-lines: 6

  // Define the pins of the segments and the digits on the 4-digit 7-segment display
  int segmentPins[] = { 2, 3, 4, 5, 6, 7, 8, 9 };  // Segments a~g and dp (decimal point)
  int digitPins[] = { 10, 11, 12, 13 };            // Digits d1-d4

  //display 0,1,2,3,4,5,6,7,8,9
  int numArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };

3. 次に、選択した数字を指定した桁に表示する関数を作成します。

.. code-block:: Arduino

  void displayNumberOnDigit(int number, int digit) {
    // Turn off all digits to prevent ghosting when switching numbers
    for (int i = 0; i < 4; i++) {
      // Turn off digit (common cathode -> HIGH is off)
      digitalWrite(digitPins[i], HIGH);
    }

    // Set the segments for the current number
    int value = numArray[number];
    for (int i = 0; i < 8; i++) {
      digitalWrite(segmentPins[i], (value >> i) & 1);  // Set each segment
    }

    // Turn on the selected digit (common cathode -> LOW is on)
    digitalWrite(digitPins[digit], LOW);
  }

* 番号を切り替える際にゴースティングを防ぐためにすべての桁をオフにします。

.. code-block:: Arduino
  
    // Turn off all digits to prevent ghosting when switching numbers
    for (int i = 0; i < 4; i++) {
      // Turn off digit (common cathode -> HIGH is off)
      digitalWrite(digitPins[i], HIGH);
    }

* ビット演算を使用して各数字に対応するセグメントを点灯します。
  
  .. code-block:: Arduino
    :emphasize-lines: 4
    
    // 現在の番号のセグメントを設定する
    int value = numArray[number];
    for (int i = 0; i < 8; i++) {
      digitalWrite(segmentPins[i], (value >> i) & 1);  // Set each segment
    }
  
  * ここで、 ``numArray[]`` 配列の要素が変数 ``value`` に割り当てられます。 ``number`` が2の場合、 ``numArray[]`` の3番目の要素（ ``B01011011`` ）が ``value`` に割り当てられます。
  * 次に、 ``for`` ループで ``B01011011`` の8ビット（Bを除く）を ``segmentPins[i]`` 配列に ``digitalWrite()`` を使用して書き込みます。これにより、セグメントa、b、d、e、およびgが1に設定され、c、f、およびdpが0に設定されて、数字2が表示されます。
  * ``&`` は ``AND`` 演算子で、ビットごとの ``AND`` 演算を実行します。 ``1&1`` は1、 ``1&0`` は0になります。

  .. image:: img/32_stopwatch_and.png
    :width: 300
    :align: center
  
  * ``>>`` は右シフト演算子で、指定したビット数だけ右にシフトします。たとえば、 ``i`` が1の場合、 ``B01011011`` は1ビット右にシフトし、右端のビットが削除され、左に0が追加されます。 ``i`` が2の場合、 ``B01011011`` は2ビット右にシフトし、右端の2ビットが削除され、左に2つの0が追加されます。
  * 右シフトの結果に対して、ビットごとのAND演算が1と行われ、1または0が得られます。

  .. image:: img/32_stopwatch_shift_right.png
    :width: 500
    :align: center

* 表示する数字の桁のみを有効にします。

.. code-block:: Arduino
  
    // Turn on the selected digit (common cathode -> LOW is on)
    digitalWrite(digitPins[digit], LOW);

4. ``void loop`` のメインプログラムで、 ``for`` ループを使用して、左端の桁が0から9までの数字をスクロールするようにします。

.. code-block:: Arduino
  :emphasize-lines: 4

  void loop() {
    // Display numbers 0 to 9 sequentially on the first digit (D1)
    for (int num = 0; num < 10; num++) {
      displayNumberOnDigit(num, 0);  // Display the number on digit 1 (index 0)
      delay(1000);                   // Display each number for 1 second
    }
  }

5. 以下は完成したコードです。これをArduino Uno R3にアップロードすると、左端の桁に0から9までの数字がスクロール表示されるのが確認できます。

.. code-block:: Arduino

  // Define the pins of the segments and the digits on the 4-digit 7-segment display
  int segmentPins[] = { 2, 3, 4, 5, 6, 7, 8, 9 };  // Segments A-G and DP (decimal point)
  int digitPins[] = { 10, 11, 12, 13 };            // Digits D1-D4

  //display 0,1,2,3,4,5,6,7,8,9
  int numArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };

  void setup() {
    // Set all segment pins as output
    for (int i = 0; i < 8; i++) {
      pinMode(segmentPins[i], OUTPUT);
      digitalWrite(segmentPins[i], LOW);  // Ensure all segments are off initially
    }

    // Set all digit pins as output and turn them off (common cathode, so HIGH is off)
    for (int i = 0; i < 4; i++) {
      pinMode(digitPins[i], OUTPUT);
      digitalWrite(digitPins[i], HIGH);
    }
  }

  void loop() {
    // Display numbers 0 to 9 sequentially on the first digit (D1)
    for (int num = 0; num < 10; num++) {
      displayNumberOnDigit(num, 0);  // Display the number on digit 1 (index 0)
      delay(1000);                   // Display each number for 1 second
    }
  }

  void displayNumberOnDigit(int number, int digit) {
    // Turn off all digits to prevent ghosting when switching numbers
    for (int i = 0; i < 4; i++) {
      // Turn off digit (common cathode -> HIGH is off)
      digitalWrite(digitPins[i], HIGH);
    }

    // Set the segments for the current number
    int value = numArray[number];
    for (int i = 0; i < 8; i++) {
      digitalWrite(segmentPins[i], (value >> i) & 1);  // Set each segment
    }

    // Turn on the selected digit (common cathode -> LOW is on)
    digitalWrite(digitPins[digit], LOW);
  }


**質問**

プログラミングにおいて、ビット単位の演算（ ``AND`` や ``OR`` ）は、データの個々のビットを操作する上で重要です。ビット単位の ``AND`` 演算（ ``&`` ）は、オペランドの各ビットを比較し、両方のビットが1の場合に1、それ以外の場合は0を返します。一方、ビット単位の ``OR`` 演算（ ``|`` ）は、少なくとも1つのビットが1である場合に1、両方のビットが0の場合にのみ0を返します。

この情報を踏まえて、式 ``(B01011011 >> 2) | 1`` を考えてみましょう。2ビット右シフトしたバイナリ数 ``B01011011`` に対して、ビット単位の ``OR`` 演算を1と行った結果はどうなりますか？


コード作成 - ストップウォッチ
--------------------------------

これまでに、一桁の数字を表示し、その数字をスクロールする方法を学びました。今回は、4桁の7セグメントディスプレイを使用してストップウォッチを作成する方法を学びましょう。

* ストップウォッチを作成するには、左側の2桁で分を、右側の2桁で秒を表示します。
* 秒数が59に達すると0にリセットされ、分数が1増加します。
* 分数が99に達すると0にリセットされ、再びカウントが開始されます。

1. 先ほど保存したスケッチ ``Lesson32_Show_2_One_Digit`` を開き、「名前を付けて保存...」を選択し、 ``Lesson32_Stopwatch`` に名前を変更して保存します。

2. 次に、時間の要素を保存するための3つの変数を作成します。 ``previousMillis`` は最後に表示が更新されてからの時間を記録し、 ``seconds`` と ``minutes`` はストップウォッチの時間を保存します。

.. code-block:: Arduino
  :emphasize-lines: 9-11

  // Define the pins of the segments and the digits on the 4-digit 7-segment display
  int segmentPins[] = {2, 3, 4, 5, 6, 7, 8, 9};  // Segments A-G and DP (decimal point)
  int digitPins[] = {10, 11, 12, 13};            // Digits D1-D4

  //display 0,1,2,3,4,5,6,7,8,9
  int numArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };

  // Variables to store time components
  unsigned long previousMillis = 0;  // Stores the last time the display was updated
  int seconds = 0;  // Stores the second count
  int minutes = 0;  // Stores the minute count

3. ``void loop()``  関数内で:

* ``millis()`` 関数を使用して、Arduinoボードが現在のプログラムを実行し始めてからのミリ秒数を返します。
* 1000ミリ秒（1秒）ごとに秒数を1ずつ増加させます。秒数が60に達すると0にリセットされ、分数が増加します。分数が100に達すると0にリセットされ、再びカウントが開始されます。
* 各ループの反復ごとに ``updateDisplay()`` を呼び出して、現在の秒数と分数に基づいてディスプレイを積極的にマルチプレックスします。

.. code-block:: Arduino

  void loop() {
    unsigned long currentMillis = millis();        // Get the current time in milliseconds
    if (currentMillis - previousMillis >= 1000) {  // Check if a second has passed
      previousMillis = currentMillis;              // Reset the timer
      seconds++;                                   // Increment the seconds
      if (seconds >= 60) {                         // Check if 60 seconds have passed
        seconds = 0;                               // Reset seconds
        minutes++;                                 // Increment the minutes
        if (minutes > 99) {                        // Check if 100 minutes have passed
          minutes = 0;                             // Reset minutes
        }
      }
    }
    updateDisplay();  // 現在の時間を表示するようにディスプレイを更新
  }

4. ``updateDisplay()`` 関数について: 1秒ごとに表示を設定する代わりに、 ``updateDisplay()`` はメインループ内で継続的に呼び出されます。この関数は各桁を順に処理し、短時間その桁を点灯させてから再びオフにします。このプロセスは高速で繰り返され、安定した表示が行われているように見えます。

.. code-block:: Arduino

  void updateDisplay() {
    for (int digit = 0; digit < 4; digit++) {
      setDigitValues(minutes, seconds, digit);
      digitalWrite(digitPins[digit], LOW); // Turn on current digit
      delay(5); // Delay to keep the digit visible
      digitalWrite(digitPins[digit], HIGH); // Turn off digit
    }
  }

5. ``setDigitValues()`` 関数について: ``setDigitValues()`` は、現在の時間（分と秒）に基づいて各桁のセグメントを設定します。この関数は、桁が有効になるたびに呼び出され、正しい値を表示するようにします。

.. code-block:: Arduino

  void setDigitValues(int mins, int secs, int digit) {
    int values[] = {
      mins / 10, // tens of minutes
      mins % 10, // ones of minutes
      secs / 10, // tens of seconds
      secs % 10  // ones of seconds
    };

    int value = numArray[values[digit]];

    for (int segment = 0; segment < 8; segment++) {
      digitalWrite(segmentPins[segment], (value >> segment) & 1);
    }
  }

6. 以下は完成したコードです。これをArduinoボードにアップロードすると、4桁の7セグメントディスプレイにストップウォッチが表示されるのを確認できます。

.. code-block:: Arduino

  // Define the pins of the segments and the digits on the 4-digit 7-segment display
  int segmentPins[] = { 2, 3, 4, 5, 6, 7, 8, 9 };  // Segments A-G and DP (decimal point)
  int digitPins[] = { 10, 11, 12, 13 };            // Digits D1-D4

  //display 0,1,2,3,4,5,6,7,8,9
  int numArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };

  // Variables to store time components
  unsigned long previousMillis = 0;  // Stores the last time the display was updated
  int seconds = 0;                   // Stores the second count
  int minutes = 0;                   // Stores the minute count

  void setup() {
    // Set all segment pins as output
    for (int i = 0; i < 8; i++) {
      pinMode(segmentPins[i], OUTPUT);
      digitalWrite(segmentPins[i], LOW);  // Ensure all segments are off initially
    }

    // Set all digit pins as output and turn them off (common cathode, so HIGH is off)
    for (int i = 0; i < 4; i++) {
      pinMode(digitPins[i], OUTPUT);
      digitalWrite(digitPins[i], HIGH);
    }
  }

  void loop() {
    unsigned long currentMillis = millis();        // Get the current time in milliseconds
    if (currentMillis - previousMillis >= 1000) {  // Check if a second has passed
      previousMillis = currentMillis;              // Reset the timer
      seconds++;                                   // Increment the seconds
      if (seconds >= 60) {                         // Check if 60 seconds have passed
        seconds = 0;                               // Reset seconds
        minutes++;                                 // Increment the minutes
        if (minutes > 99) {                        // Check if 100 minutes have passed
          minutes = 0;                             // Reset minutes
        }
      }
    }
    updateDisplay();  // Update the display to show the current time
  }

  void updateDisplay() {
    for (int digit = 0; digit < 4; digit++) {
      setDigitValues(minutes, seconds, digit);
      digitalWrite(digitPins[digit], LOW);   // Turn on current digit
      delay(5);                              // Delay to keep the digit visible
      digitalWrite(digitPins[digit], HIGH);  // Turn off digit
    }
  }

  void setDigitValues(int mins, int secs, int digit) {
    int values[] = {
      mins / 10,  // tens of minutes
      mins % 10,  // ones of minutes
      secs / 10,  // tens of seconds
      secs % 10   // ones of seconds
    };

    int value = numArray[values[digit]];

    for (int segment = 0; segment < 8; segment++) {
      digitalWrite(segmentPins[segment], (value >> segment) & 1);
    }
  }


7. 最後に、コードを保存して作業スペースを整理することを忘れないでください。


**まとめ**

今回のレッスンでは、4桁の7セグメントディスプレイの機能を探り、Arduinoを使ってそれを制御する方法を学びました。まず、1桁に数字を表示する方法を学び、次に数字をスクロールする方法を学びました。最後に、これらのスキルを組み合わせて、分と秒を表示するシンプルなストップウォッチを作成しました。このプロジェクトを通じて、デジタルディスプレイについて学ぶだけでなく、Arduinoでのプログラミングスキルも向上しました。レッスンを完了したことを称賛し、さらに素晴らしいプロジェクトを作成するために実験を続けてください！

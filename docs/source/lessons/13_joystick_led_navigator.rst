.. note::

    こんにちは、SunFounderのRaspberry Pi & Arduino & ESP32愛好者コミュニティへようこそ！Facebookで他のエンスージアストたちと一緒に、Raspberry Pi、Arduino、ESP32についてさらに深く学びましょう。

    **参加する理由**

    - **専門サポート**: コミュニティとチームの助けを借りて、購入後の問題や技術的な課題を解決できます。
    - **学びと共有**: スキル向上のためのヒントやチュートリアルを交換できます。
    - **限定プレビュー**: 新製品の発表や先行情報をいち早く入手できます。
    - **特別割引**: 新製品に対する限定割引を利用できます。
    - **イベントプロモーションとプレゼント企画**: プレゼント企画や季節のプロモーションに参加できます。

    👉 探索と創造を私たちと共に始めましょう！[|link_sf_facebook|] をクリックして、今日から参加しましょう！

13. ジョイスティック LED ナビゲーター
===================================================

サムスティックと聞くと、ゲームコントローラーを思い浮かべるかもしれませんが、実はゲーム以外にも多用途で、様々なDIYエレクトロニクスプロジェクトに最適です。例えば、ロボットやローバーの制御や、カメラの動きを管理するためにも使用できます。

このプロジェクトベースのコースでは、ジョイスティックをArduinoに接続し、ジョイスティックの動きに応じてLEDを制御する方法を学びます。ジョイスティックの動作原理を探り、シリアルモニタを活用して出力を読み取り、デバッグし、指定された方向でLEDを点灯させるための制御ロジックを開発します。このコースは、実際のシナリオで重要となる精密な方向制御を強調し、実践的な応用に直接役立つ内容となっています。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/13_joystick_led.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このコースの終了時には、以下のことができるようになります:

* ジョイスティックの動作原理と、その出力（X軸、Y軸、SW）を理解する。
* Arduinoでセンサ値を読み取り、デバッグするためのシリアルモニタの使用方法を学ぶ。
* ハードウェアを入力値に基づいて制御するための条件文（ ``if-else if`` ）を記述し、理解する。


回路の構築
------------------------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 4 * 色の異なるLED
     - 4 * 220Ω抵抗
     - 1 * ジョイスティックモジュール
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_joystick_module| 
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - ジャンパワイヤ
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - 
     
**構築手順**

配線図または以下の手順に従って回路を構築します。

.. image:: img/11_joystick_circuit.png
    :width: 700
    :align: center

1. ジョイスティックモジュールを見つけます。

ジョイスティックモジュール、別名ジョイスティックセンサーは、ノブの動きを水平方向（X軸）と垂直方向（Y軸）の2方向で測定する入力デバイスです。


.. image:: img/11_joystick_module.jpg
    :width: 300
    :align: center

* **GND**: グランドに接続します。
* **+5V**: モジュールに電源を供給し、3.3Vから5Vまで対応可能です。
* **VRX**: X軸位置を表すアナログ値を出力します。
* **VRY**: Y軸位置を表すアナログ値を出力します。
* **SW**: ジョイスティックボタンが押されたときにデジタル出力を提供します。信頼性の高い動作のためには、SWピンをアイドル時に高、押されたときに低に保つ外部プルアップ抵抗を使用してください。

ジョイスティックは通常、10キロオームの2つのポテンショメータの抵抗変化に基づいて動作します。X軸とY軸の方向に応じて抵抗を変化させることで、Arduinoは電圧の変化を受け取り、それをX座標およびY座標に変換します。プロセッサは、ジョイスティックのアナログ値をデジタル値に変換し、必要な処理を行うためにADCユニットを必要とします。

Arduinoボードには6つの10ビットADCチャンネルがあります。これは、Arduinoの基準電圧（5ボルト）が1024セグメントに分割されることを意味します。ジョイスティックがX軸に沿って動くと、ADC値は0から1023まで上昇し、中央の値は512になります。以下の画像は、ジョイスティック位置に基づくADCの概略値を示しています。

.. image:: img/11_joystick_xy_range.jpg
    :width: 500
    :align: center

ジョイスティックには、ボタンのように押し込む機能もあり、メニューオプションの選択や他のインタラクティブ要素に便利です。

.. image:: img/11_joystick_module_button.jpg
    :width: 300
    :align: center

2. ジョイスティックモジュールの各ピンをArduino Uno R3に接続します。

.. list-table:: 
   :widths: 10 30
   :header-rows: 0

   * - Arduino Uno R3
     - ジョイスティック
   * - GND
     - GND(ブレッドボードの負のレール)
   * - +5v
     - 5v
   * - VRX
     - A0
   * - VRY
     - A1
   * - SW
     - 2

.. image:: img/11_joystick_circuit_joystick.png
    :width: 700
    :align: center

3. 異なる色の4つのLEDをブレッドボードに挿入します。各LEDの陰極（短いピン）をブレッドボードの負のレールに接続し、陽極（長いピン）を指定されたポート（58A、53A、49A、45A）に接続します。

.. image:: img/11_joystick_circuit_led.png
    :width: 700
    :align: center

4. 各LEDの陽極と同じ行に220オームの抵抗を挿入し、LEDを過電流から保護します。

.. image:: img/11_joystick_circuit_resistor.png
    :width: 700
    :align: center

5. ジャンパワイヤを使用して、ブレッドボードの58J穴をArduinoのピン11に接続し、最初のLEDの制御を可能にします。

.. image:: img/11_joystick_circuit_11.png
    :width: 700
    :align: center

6. 同様に、他の3つのLEDをそれぞれArduinoのピン10、9、8に接続します。

.. image:: img/11_joystick_circuit_8910.png
    :width: 700
    :align: center

7. 回路をグランドに接続することを忘れないでください。Arduino Uno R3のGNDピンをブレッドボードの負のレールに接続し、ジャンパワイヤを使用してブレッドボードの両方の負のレールを接続します。

.. image:: img/11_joystick_circuit.png
    :width: 700
    :align: center


コード作成 - ジョイスティックモジュールからの読み取り
-------------------------------------------------------

ジョイスティックモジュールのX軸、Y軸、およびボタンから取得される値がどのようなものかを見てみましょう。そのために、シリアルモニタというツールを使用します。

シリアルモニタは、Arduinoプロジェクトを作成する際に欠かせないツールです。デバッグツールとして、概念をテストしたり、Arduinoボードと直接通信したりするために使用されます。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して、新しいプロジェクトを開始します。
2. スケッチを ``Lesson13_Joystick_Module`` として保存します（ ``Ctrl + S`` を押すか、「保存」をクリックします）。

3. ジョイスティックモジュールの3つのピンからの値を保存するための3つの変数を作成します。

.. code-block:: Arduino
    :emphasize-lines: 1,2,3

    const int xPin = A0;  //the VRX attach to
    const int yPin = A1;  //the VRY attach to
    const int swPin = 2;  //the SW attach to

    void setup() {
        // put your main code here, to run repeatedly:

    }

4. また、Arduinoソフトウェアのプルアップ機能を使用して、 ``swPin`` を入力として設定し、 ``PULLUP`` として有効にします。

.. code-block:: Arduino
    :emphasize-lines: 7

    const int xPin = A0;  // VRXに接続
    const int yPin = A1;  // VRYに接続
    const int swPin = 2;  // SWに接続

    void setup() {
        // ここにメインコードを繰り返し実行するために書きます:
        pinMode(swPin, INPUT_PULLUP);  // 内部プルアップ抵抗でsw Pinを入力として設定
    }

5. シリアルモニタを有効にするには、Arduino Uno R3でシリアル通信を開始する必要があります。これは通常、スケッチの ``void setup()`` セクションで ``Serial.begin(baud)`` コマンドを使用して行われます。ここで ``baud`` は、コンピュータとArduino Uno R3の間のデータ転送速度を示し、一般的な速度は9600ビット/秒および115200ビット/秒です。

.. code-block:: Arduino
    :emphasize-lines: 8

    const int xPin = A0;  // VRXに接続
    const int yPin = A1;  // VRYに接続
    const int swPin = 2;  // SWに接続

    void setup() {
        // ここにセットアップコードを一度だけ実行するために書きます:
        pinMode(swPin, INPUT_PULLUP);  // 内部プルアップ抵抗でsw Pinを入力として設定
        Serial.begin(9600);        // 9600ボーレートでシリアル通信を開始
    }

6. 次に、X、Y、およびSWピンからの値を保存するための3つの変数 ``xValue`` 、 ``yValue`` 、 ``swValue`` を作成します。

.. code-block:: Arduino
    :emphasize-lines: 4-6

    void loop() {

        // ジョイスティックの値を読み取ります
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin);
        int swValue = digitalRead(swPin);
    }

7. これで、シリアルモニタを使用してデータを表示する準備が整いました。データやその他のテキストを表示するために ``Serial.print()`` を使用します。

使用方法は以下の通りです:

    * ``Serial.print(val)`` または ``Serial.print(val, format)`` : データをシリアルポートに人間が読めるASCIIテキストとして表示します。

    **パラメータ**
        - ``Serial`` : シリアルポートオブジェクト。
        - ``val`` : 表示する値。許可されるデータ型: 任意のデータ型。

    **戻り値**
        ``print()`` は書き込まれたバイト数を返しますが、その数を読むことはオプションです。データ型: size_t。

このコマンドは、数字、浮動小数点、バイト、文字列など、さまざまなデータ型と形式を表現できます。例えば:

.. code-block:: Arduino

    Serial.print(78);                // "78"と表示
    Serial.print(78, BIN);           // "1001110"と表示
    Serial.print(1.23456);           // "1.23"と表示
    Serial.print(1.23456, 0);        // "1"と表示
    Serial.print('N');               // "N"と表示
    Serial.print("Hello world.");    // "Hello world."と表示

8. 次に、このコマンドを使用して、印刷されるデータを示すプロンプトを表示します。これにより、複数のデータを同時に表示するときに区別しやすくなります。

.. code-block:: Arduino
    :emphasize-lines: 8

    void loop() {

        // Read the joystick values
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin);
        int swValue = digitalRead(swPin);

        Serial.print("X: ");
    }

9. 次に、ジョイスティックモジュールのVRXピンからの値を表示します。
    
.. code-block:: Arduino
    :emphasize-lines: 9

    void loop() {

        // Read the joystick values
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin);
        int swValue = digitalRead(swPin);

        Serial.print("X: ");
        Serial.print(xValue);  // print the value of VRX
    }


10. 同じ方法を使用して、VRYピンとSWピンの値を表示します。

.. note::

    * Serial Monitorで各出力が新しい行に表示されるようにするには、SWピンの値に ``Serial.println()`` を使用します。これにより、印刷文の最後に改行文字が追加されます。
    * 次のデータが表示される前に時間間隔を確保するために、 ``delay(100)`` を使用します。Serial Monitorにデータを出力する際、更新が早すぎるとクラッシュの原因になるため、遅延を追加することをお勧めします。

.. code-block:: Arduino
    :emphasize-lines: 10-14

    void loop() {

        // Read the joystick values
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin);
        int swValue = digitalRead(swPin);
        
        Serial.print("X: ");
        Serial.print(xValue);  // print the value of VRX
        Serial.print(" | Y: ");
        Serial.print(yValue);  // print the value of VRX
        Serial.print(" | SW: ");
        Serial.println(swValue);  // print the value of SW
        delay(100);
    }

11. 完全なコードは以下の通りです。 **Upload** をクリックして、コードをArduino Uno R3に転送できます。

.. code-block:: Arduino

    const int xPin = A0;  // VRXはA0に接続
    const int yPin = A1;  // VRYはA1に接続
    const int swPin = 2;  // SWは2に接続

    void setup() {
        // セットアップコードは一度だけ実行されます:
        pinMode(swPin, INPUT_PULLUP);  // 内部プルアップ抵抗を使用してSWピンを入力に設定
        Serial.begin(9600);        // 9600ボーのレートでシリアル通信を開始
    }

    void loop() {

        // ジョイスティックの値を読み取ります
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin);
        int swValue = digitalRead(swPin);

        Serial.print("X: ");
        Serial.print(xValue);  // print the value of VRX
        Serial.print(" | Y: ");
        Serial.print(yValue);  // print the value of VRX
        Serial.print(" | SW: ");
        Serial.println(swValue);  // print the value of SW
        delay(100);
    }

12. その後、Arduino IDEの右上にある「Serial Monitor」ボタンをクリックします。

.. image:: img/11_joystick_serial_monitor.png
    :align: center

13. もしデータが乱れて表示された場合は、コードで設定したボー・レートに合わせてボー・レートを調整する必要があります。

.. image:: img/11_joystick_baud.png
    :align: center

14. アップロードが完了したら、ジョイスティックを動かして、XとYの値が0から1023の間で変動するのを確認します。ジョイスティックを押したり離したりすると、SWピンが0から1に切り替わる様子が観察できます。

.. code-block::

    X: 617 | Y: 1022 | SW: 1
    X: 767 | Y: 1023 | SW: 1
    X: 1022 | Y: 1022 | SW: 1
    X: 516 | Y: 522 | SW: 1
    X: 516 | Y: 522 | SW: 1
    X: 517 | Y: 524 | SW: 1
    X: 517 | Y: 524 | SW: 1

15. Serial Monitorにデータを表示する方法を学んだところで、Serial Monitorのいくつかのボタンを見てみましょう：

.. image:: img/11_joystick_serial_button.png
        :align: center

* **Autoscrollの切り替え**: 最新のデータを常に確認できるようにスクロールを有効にします。
* **タイムスタンプの切り替え**: データに秒単位でタイムスタンプを付けて表示します。
* **出力をクリア**: 現在画面に表示されているデータをクリアします。


**質問**

ジョイスティックモジュールのX軸およびY軸はアナログ値を返し、SWピンはデジタル値を返します。前の手順で、これらの値がすでにSerial Monitorに表示されていることを確認しました。

Arduinoプログラミングにおけるデジタル値とアナログ値の違いを要約してください。

Code Creation - ジョイスティックの動きに基づくLED制御
----------------------------------------------------------

このチュートリアルでは、ジョイスティックの動きに応じてLEDをプログラムする方法を説明します。

.. image:: img/11_joystick_xy_range.jpg
    :width: 500
    :align: center

各LEDをジョイスティックの動きに応じた方向を示すように設定します：

* **上方向インジケーター**: LEDをピン10に接続します。ジョイスティックを上に押すと（Y軸の値が減少）、LEDが点灯します。
* **下方向インジケーター**: LEDをピン9に接続します。ジョイスティックを下に押すと（Y軸の値が増加）、LEDが点灯します。
* **左方向インジケーター**: LEDをピン11に接続します。ジョイスティックを左に押すと（X軸の値が減少）、LEDが点灯します。
* **右方向インジケーター**: LEDをピン8に接続します。ジョイスティックを右に押すと（X軸の値が増加）、LEDが点灯します。

ここで疑問が生じます。Arduino Uno R3はどのようにしてジョイスティックがどの方向に動いているかを認識するのでしょうか？

理想的には、ジョイスティックが中央にあるときの値は(1024/2=512)になるはずです。したがって、ジョイスティックが上、下、左、右のどちらに押されているかを判断するには、値が512より大きいか小さいかを確認すればよいのです。

しかし、モジュールの設計上の不正確さや接続の抵抗により、ジョイスティックが中央にあるときでも512から値がずれる可能性があります。このため、Arduino Uno R3が誤ってX値が512未満であると解釈し、実際には動いていないのに左方向インジケーターLEDが点灯する場合があります。

そのため、中央の値（512±100）の周囲に閾値を設定します：

.. image:: img/11_joystick_xy_200.png
    :width: 400
    :align: center

* **上方向**: Y軸の値が412未満。
* **下方向**: Y軸の値が612より大きい。
* **左方向**: X軸の値が412未満。
* **右方向**: X軸の値が612より大きい。

1. それではスケッチの作成を始めましょう。前回保存したスケッチ ``Lesson13_Joystick_Module`` を開きます。「ファイル」メニューから「名前を付けて保存」を選択し、 ``Lesson13_Joystick_Module_LEDs``  として保存します。「保存」をクリックします。

2. 4つのLEDを定義する変数を初期化します。

.. code-block:: Arduino
    :emphasize-lines: 2-5

    // LEDのピンを定義
    const int ledLeft = 11;
    const int ledRight = 8;
    const int ledUp = 10;
    const int ledDown = 9;

    // ジョイスティックのピンを定義
    const int xPin = A0;  // VRXが接続されるピン
    const int yPin = A1;  // VRYが接続されるピン
    const int swPin = 2;  // SWが接続されるピン

    void setup() {
        // メインコードは繰り返し実行されます:

    }

3. 次に、 ``void setup()``  内で4つのLEDピンを全て出力に設定します。

.. code-block:: Arduino
    :emphasize-lines: 3-6

    void setup() {
        // Initialize LED pins as outputs
        pinMode(ledLeft, OUTPUT);
        pinMode(ledRight, OUTPUT);
        pinMode(ledUp, OUTPUT);
        pinMode(ledDown, OUTPUT);
        
        pinMode(swPin, INPUT_PULLUP);  // Set sw Pin as input with an internal pull-up resistor
        Serial.begin(9600);        // Begin serial communication with a baud rate of 9600
    }

4. このプロジェクトでは、ジョイスティックの値を常にチェックする必要はないため、5行の ``Serial.print()`` を選択し、 ``Ctrl + /`` を押してコメントアウトします。

.. code-block:: Arduino
    :emphasize-lines: 7-12

    void loop() {
        // Read the joystick values
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin);
        int swValue = digitalRead(swPin);

        // Serial.print("X: ");
        // Serial.print(xValue);  // print the value of VRX
        // Serial.print(" | Y: ");
        // Serial.print(yValue);  // print the value of VRX
        // Serial.print(" | SW: ");
        // Serial.println(swValue);  // print the value of SW

        // Add a small delay to stabilize readings
        delay(100);
    }

5. ジョイスティックの動きに応じて対応するLEDを点灯させる前に、まず4つのLED全てを消灯します。

.. code-block:: Arduino
    :emphasize-lines: 15-18

    void loop() {
        // Read the joystick values
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin);
        int swValue = digitalRead(swPin);

        // Serial.print("X: ");
        // Serial.print(xValue);  // print the value of VRX
        // Serial.print(" | Y: ");
        // Serial.print(yValue);  // print the value of VRX
        // Serial.print(" | SW: ");
        // Serial.println(swValue);  // print the value of SW

        // First, turn off all LEDs
        digitalWrite(ledLeft, LOW);
        digitalWrite(ledRight, LOW);
        digitalWrite(ledUp, LOW);
        digitalWrite(ledDown, LOW);

        // Add a small delay to stabilize readings
        delay(100);
    }

7. ジョイスティックモジュールのX軸およびY軸の値に基づいて、各LEDを順次点灯させるには、複数の条件が必要です。 ``if`` を使用してポテンショメータの値の異なる範囲に対する動作を指定できます：
  
* Y軸の値が412未満の場合、"上"インジケーターを点灯させる。
* Y軸の値が612より大きい場合、"下"インジケーターを点灯させる。
* X軸の値が412未満の場合、"左"インジケーターを点灯させる。
* X軸の値が612より大きい場合、"右"インジケーターを点灯させる。

しかし、これらの条件を個別に管理するのは効率的ではなく、Arduinoはループサイクルごとに各条件をチェックする必要があります。

これを効率化するために、 ``if-else if`` 構造を利用します：

.. code-block:: Arduino

    if (condition 1) {
        // Execute if condition 1 is true
    }
    else if (condition 2) {
        // Execute if condition 2 is true
    }
    else if (condition 3) {
        // Execute if condition 3 is true
    }
    else {
        // Execute if none of the conditions are true
    }

.. image:: img/if_else_if.png
    :width: 500
    :align: center

``if-else if`` 構造では、最初に条件1がテストされます。条件1が真であれば、関連するコマンドが実行され、それ以外の条件はすべてスキップされます（たとえそれらが真であっても）。条件1が偽であれば、次に条件2がテストされ、条件2が真であれば、そのコマンドが実行され、他の条件はスキップされます。もし条件2も偽であれば、条件3がテストされ、以下同様に処理が続きます。あるシナリオでは、複数の条件が真である場合があります。そのため、条件の順序が重要です。最初の真の条件のみが実行されるコマンドを持ちます。
8. まず、 ``yValue`` が412未満の場合、 ``digitalWrite()`` 関数を使用して「上」インジケーターライトを ``HIGH`` に設定し、点灯させます。

.. code-block:: Arduino
    :emphasize-lines: 8-11
    
    // First, turn off all LEDs
    digitalWrite(ledLeft, LOW);
    digitalWrite(ledRight, LOW);
    digitalWrite(ledUp, LOW);
    digitalWrite(ledDown, LOW);

    // Check joystick positions and set LEDs accordingly
    if (yValue < 412) {
        // Joystick up
        digitalWrite(ledUp, HIGH);
    }

9. ``yValue`` が612を超えたときに「下」インジケーターを点灯させるために、 ``else if`` 文を追加します。

.. code-block:: Arduino
    :emphasize-lines: 12-15
    
    // First, turn off all LEDs
    digitalWrite(ledLeft, LOW);
    digitalWrite(ledRight, LOW);
    digitalWrite(ledUp, LOW);
    digitalWrite(ledDown, LOW);

    // Check joystick positions and set LEDs accordingly
    if (yValue < 412) {
        // Joystick up
        digitalWrite(ledUp, HIGH);
    }
    else if (yValue > 612) {
        // Joystick down
        digitalWrite(ledDown, HIGH);
    } 

10. ``xValue`` が412未満のときに「左」インジケーターを点灯させるために、次のように ``else if`` 条件を挿入します。

.. code-block:: Arduino
    :emphasize-lines: 8-11
    
    // Check joystick positions and set LEDs accordingly
    if (yValue < 412) {
        // Joystick up
        digitalWrite(ledUp, HIGH);
    } else if (yValue > 612) {
        // Joystick down
        digitalWrite(ledDown, HIGH);
    } else if (xValue < 412) {
        // Joystick left
        digitalWrite(ledLeft, HIGH);
    }  

11. 同様に、 ``xValue`` が612を超えたときに「右」インジケーターを点灯させるために、さらに ``else if`` 条件を追加します。

.. code-block:: Arduino
    :emphasize-lines: 11-14 

    // Check joystick positions and set LEDs accordingly
    if (yValue < 412) {
        // Joystick up
        digitalWrite(ledUp, HIGH);
    } else if (yValue > 612) {
        // Joystick down
        digitalWrite(ledDown, HIGH);
    } else if (xValue < 412) {
        // Joystick left
        digitalWrite(ledLeft, HIGH);
    } else if (xValue > 612) {
        // Joystick right
        digitalWrite(ledRight, HIGH);
    }

12. 最後に、 ``else`` ブロック内で ``digitalWrite()`` を使用して4つのLEDすべてを消灯します。このブロックには、他のどの条件も当てはまらない場合に実行されるコマンドが含まれています。

.. code-block:: Arduino
    :emphasize-lines: 14-20

    // Check joystick positions and set LEDs accordingly
    if (yValue < 412) {
        // Joystick up
        digitalWrite(ledUp, HIGH);
    } else if (yValue > 612) {
        // Joystick down
        digitalWrite(ledDown, HIGH);
    } else if (xValue < 412) {
        // Joystick left
        digitalWrite(ledLeft, HIGH);
    } else if (xValue > 612) {
        // Joystick right
        digitalWrite(ledRight, HIGH);
    } else {
        // Joystick in the middle, turn off all LEDs
        digitalWrite(ledLeft, LOW);
        digitalWrite(ledRight, LOW);
        digitalWrite(ledUp, LOW);
        digitalWrite(ledDown, LOW);
    }

13. 完成したコードは以下の通りです。「Upload」ボタンをクリックして、コードをArduino Uno R3に送信してください。

.. code-block:: Arduino

    // Define pins for the LEDs
    const int ledLeft = 11;
    const int ledRight = 8;
    const int ledUp = 10;
    const int ledDown = 9;

    // Define pins for the joystick
    const int xPin = A0;  //the VRX attach to
    const int yPin = A1;  //the VRY attach to
    const int swPin = 2;  //the SW attach to

    void setup() {
        // Initialize LED pins as outputs
        pinMode(ledLeft, OUTPUT);
        pinMode(ledRight, OUTPUT);
        pinMode(ledUp, OUTPUT);
        pinMode(ledDown, OUTPUT);

        pinMode(swPin, INPUT_PULLUP);  // Set sw Pin as input with an internal pull-up resistor
        Serial.begin(9600);        // Begin serial communication with a baud rate of 9600
    }

    void loop() {
        // Read the joystick values
        int xValue = analogRead(xPin);
        int yValue = analogRead(yPin);
        int swValue = digitalRead(swPin);

        // Serial.print("X: ");
        // Serial.print(xValue);  // print the value of VRX
        // Serial.print(" | Y: ");
        // Serial.print(yValue);  // print the value of VRX
        // Serial.print(" | SW: ");
        // Serial.println(swValue);  // print the value of SW

        // First, turn off all LEDs
        digitalWrite(ledLeft, LOW);
        digitalWrite(ledRight, LOW);
        digitalWrite(ledUp, LOW);
        digitalWrite(ledDown, LOW);

        // Check joystick positions and set LEDs accordingly
        if (yValue < 412) {
            // Joystick up
            digitalWrite(ledUp, HIGH);
        } else if (yValue > 612) {
            // Joystick down
            digitalWrite(ledDown, HIGH);
        } else if (xValue < 412) {
            // Joystick left
            digitalWrite(ledLeft, HIGH);
        } else if (xValue > 612) {
            // Joystick right
            digitalWrite(ledRight, HIGH);
        } else {
            // Joystick in the middle, turn off all LEDs
            digitalWrite(ledLeft, LOW);
            digitalWrite(ledRight, LOW);
            digitalWrite(ledUp, LOW);
            digitalWrite(ledDown, LOW);
        }
        // Add a small delay to stabilize readings
        delay(100);
    }

14. ジョイスティックを動かすと、対応する方向のLEDが点灯するのが確認できるでしょう。

* **上方向インジケーター** は、ジョイスティックが上に押されたとき（Y軸の値が減少したとき）に点灯します。
* **下方向インジケーター** は、ジョイスティックが下に押されたとき（Y軸の値が増加したとき）に点灯します。
* **左方向インジケーター** は、ジョイスティックが左に押されたとき（X軸の値が減少したとき）に点灯します。
* **右方向インジケーター** は、ジョイスティックが右に押されたとき（X軸の値が増加したとき）に点灯します。

**質問**

1. 前のコードでは、ジョイスティックのXおよびY値に基づいて対応するLEDを制御しました。点灯しているLEDの明るさを調整するには、コードをどのように変更すればよいでしょうか？

2. ピン8に接続されたLEDの動作が他のピンに接続されたLEDと異なるのはなぜでしょうか？

**まとめ**

このレッスンでは、ジョイスティックモジュールの動作原理を学び、シリアルモニターを使用してジョイスティックからX、Y、およびSWの値を読み取る方法を習得しました。また、Arduinoプログラミングにおけるアナログ値とデジタル値の違いを理解し、if-else if構造を用いた条件分岐を使って、入力値に基づいてハードウェアを制御する方法も学びました。

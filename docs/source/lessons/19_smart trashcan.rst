.. note::

    こんにちは、SunFounderのRaspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebookでラズベリーパイ、Arduino、ESP32に興味を持つ仲間たちと一緒に、これらのデバイスをさらに深く探求しましょう。

    **参加する理由**

    - **専門的なサポート**: コミュニティとチームの助けを借りて、購入後の問題や技術的な課題を解決できます。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **限定プレビュー**: 新製品の発表やスニークピークにいち早くアクセスできます。
    - **特別割引**: 最新製品に対する限定割引をお楽しみください。
    - **フェスティブプロモーションとプレゼント**: プレゼントやホリデープロモーションに参加しましょう。

    👉 私たちと一緒に探索し、創造する準備ができましたか？[|link_sf_facebook|] をクリックして、今すぐ参加しましょう！

.. _ar_smart_trash_can:

19. スマートゴミ箱
===========================

スマートゴミ箱を作るエキサイティングなプロジェクトベースのコースへようこそ！このコースでは、超音波センサーとサーボモーターを組み合わせて、存在に反応するゴミ箱を作成する実践的なアプローチを提供します。このコースの終わりには、日常の物をよりスマートでインタラクティブにする方法を理解することができるでしょう。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/19_smart_trash_can.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンの終わりには、以下のことができるようになります：

* 距離測定のための超音波センサーの理解と活用。
* サーボモーターを統合して物理的な動作を自動化。
* センサー入力に基づいてデバイスの動作を制御するArduinoのプログラミング。

超音波モジュールの学習
---------------------------------

暗い部屋にいて、周囲の物が見えないと想像してみてください。この状況では、手を叩いて音を出し、その音が外に広がります。この音が壁や他の物体に当たると、エコーとして反射します。注意深く耳を澄ませば、このエコーを聞くことができます。音が外に出てエコーが戻ってくるまでの時間を計算することで、壁や物体までの距離を大まかに推定することができます。超音波センサーは、これと似た方法で周囲の世界を「見る」ことができます。

.. image:: img/19_ultrasonic_pic.png
    :width: 400
    :align: center

* **TRIG**: トリガーパルス入力
* **ECHO**: エコーパルス出力
* **GND**: グランド
* **VCC**: 5V電源

HC-SR04超音波距離センサーは、2cmから400cmまでの非接触測定を提供し、範囲精度は最大3mmです。モジュールには超音波送信機、受信機、および制御回路が含まれています。

使用するには、4つのピン（VCC（電源）、Trig（トリガー）、Echo（受信）、GND（グランド））を接続するだけで、測定プロジェクトで簡単に使用できます。

**原理**

基本的な原理は次のとおりです：

* IOトリガーを使用して、少なくとも10usの高レベル信号を送信します。
* モジュールは40kHzの超音波を8サイクル送信し、パルス信号が受信されるかどうかを検出します。
* 信号が戻ってきた場合、Echoは高レベルを出力します。高レベルの継続時間は、放射から戻りまでの時間です。
* 距離 = （高レベル時間 x 音速（340M/S）） / 2

.. image:: img/19_ultrasonic_ms.png
    :width: 600
    :align: center

.. note::

  このモジュールは電源を入れて接続しないでください。必要に応じて、まずモジュールのGNDを接続してください。さもないと、モジュールの動作に影響を与える可能性があります。

  測定対象の物体の面積は少なくとも0.5平方メートルで、できるだけ平坦である必要があります。さもないと、結果に影響を与える可能性があります。

回路の構築
------------------------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * サーボ
     - 1 * 超音波モジュール
     - 1 * ブレッドボードパワーモジュール 
   * - |list_uno_r3|
     - |list_servo| 
     - |list_ultrasonic|
     - |list_power_module|
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - ジャンパーワイヤー
     -
   * - |list_usb_cable|
     - |list_breadboard|
     - |list_wire|
     -
   * - 1 * 9V電池
     - 1 * 電池ケーブル
     - 
     -  
   * - |list_battery| 
     - |list_bat_cable| 
     -
     -

**ステップごとの構築**

配線図または以下の手順に従って回路を構築します。

.. image:: img/19_trashcan_ultrasonic_pins.png
    :width: 600
    :align: center

1. モーターやサーボ、その他のアクチュエータを使用する場合、メインボードを損傷しないように外部電源を使用することをお勧めします。ブレッドボードにパワーモジュールを挿入し、ジャンパーワイヤーを使用して、ブレッドボードの負極レールをArduino Uno R3のGNDに接続して、共通グランドを実現します。

.. image:: img/14_dinosaur_power_module.png
    :width: 400
    :align: center

.. note::

    配線図のブレッドボード上の正極端子と負極端子の順序は、キットに含まれているブレッドボードとは逆です。

    実際の配線では、ブレッドボードのパワーモジュールを数字の大きい方（60〜65）から挿入し、パワーモジュールの「-」がブレッドボードの負極レール「-」に、「+」が正極レール「+」に入るようにします。

    .. raw:: html

        <video controls style = "max-width:100%">
            <source src="_static/video/about_power_module.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

2. サーボの3本のワイヤーを短いジャンパーワイヤーで延長し、黄色のワイヤーをArduino Uno R3のピン9に、赤いワイヤーをブレッドボードの正極レールに、茶色のワイヤーを負極レールに接続します。

.. image:: img/19_trashcan_servo.png
    :width: 600
    :align: center

4. 超音波モジュールをブレッドボードに挿入します。

.. image:: img/19_trashcan_ultrasonic.png
    :width: 600
    :align: center


5. 超音波モジュールのVCCピンをブレッドボードの正極側に、TrigピンをArduinoボードのピン8に、Echoピンをピン7に、GNDをブレッドボードの負極側に接続します。

.. image:: img/19_trashcan_ultrasonic_pins.png
    :width: 600
    :align: center

.. _ar_read_distance:

コード作成 - 距離の読み取り
-----------------------------------------
それでは、超音波モジュールから距離測定を取得する方法を見てみましょう。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して、新しいプロジェクトを開始します。
2. スケッチを ``Lesson19_Read_Distance`` として保存します（ ``Ctrl + S`` または「保存」をクリックして行います）。

3. まず、Arduinoに接続されている超音波モジュールのピンを定義する必要があります。

.. code-block:: Arduino
  :emphasize-lines: 1,2

  #define TRIGGER_PIN  8
  #define ECHO_PIN     7


4. ``setup()`` 関数内で、各ピンのモードを設定します。Trigピンは信号を送信するため、出力に設定し、Echoピンは信号を受信するため、入力に設定します。

.. code-block:: Arduino
  :emphasize-lines: 2,3
  
  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Trigピンを出力に設定
    pinMode(ECHO_PIN, INPUT);      // Echoピンを入力に設定
    Serial.begin(9600);            // デバッグ用にシリアル通信を開始
  }

5. ``measureDistance()`` 関数の作成:

``measureDistance()`` 関数は、超音波センサーをトリガーし、エコーに基づいて距離を読み取るためのロジックをカプセル化します。

a. 超音波パルスのトリガー

  * ``TRIGGER_PIN`` を最初に低に設定し、クリーンなパルスを保証します。
  * 2マイクロ秒の短い遅延により、ラインがクリアになります。
  * ``TRIGGER_PIN`` に10マイクロ秒の高パルスを送信します。このパルスは、センサーに超音波を発射するように指示します。
  * パルスを終了するために、 ``TRIGGER_PIN`` を低に戻します。

  .. code-block:: Arduino

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Ensure Trig pin is low before a pulse
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Send a high pulse
      delayMicroseconds(10);           // Pulse duration of 10 microseconds
      digitalWrite(TRIGGER_PIN, LOW);  // End the high pulse
    }


b. エコーの読み取り

  * ``pulseIn()`` 関数を ``ECHO_PIN`` で使用して、入力パルスの継続時間を測定します。この関数は、ピンが ``HIGH`` になるのを待ち、それが ``HIGH`` である時間を計測し、その継続時間をマイクロ秒で返します。
  * この ``duration`` は、超音波パルスが対象物まで移動して戻るまでの時間です。

  .. code-block:: Arduino
    :emphasize-lines: 7

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Ensure Trig pin is low before a pulse
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Send a high pulse
      delayMicroseconds(10);           // Pulse duration of 10 microseconds
      digitalWrite(TRIGGER_PIN, LOW);  // End the high pulse
      long duration = pulseIn(ECHO_PIN, HIGH);  // Measure the duration of high level on Echo pin
    }

c. 距離の計算

  * ここでは、空気中の音速（約340m/s）を使用します。距離を計算するための式は（継続時間 * 音速）/ 2です。音波は対象物まで移動して戻ってくるため、片道の距離を得るために2で割ります。
  * コード内では、0.034cm/us（音速のcm/マイクロ秒単位）が変換係数として使用されます。

  .. code-block:: Arduino
    :emphasize-lines: 8,9

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Ensure Trig pin is low before a pulse
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Send a high pulse
      delayMicroseconds(10);           // Pulse duration of 10 microseconds
      digitalWrite(TRIGGER_PIN, LOW);  // End the high pulse
      long duration = pulseIn(ECHO_PIN, HIGH);  // Measure the duration of high level on Echo pin
      long distance = duration * 0.034 / 2;     // Calculate the distance (in cm)
      return distance;
    }

6. ``loop()`` 関数内で、 ``measureDistance()`` 関数を呼び出して距離を測定し、その結果をシリアルモニタに表示します。

.. code-block:: Arduino

  void loop() {
    long distance = measureDistance(); // Call the function to measure distance
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    delay(100);  // Delay between measurements
  }

.. note::

  前のレッスンでは、 ``int`` や ``float`` 型の変数や定数を使用してきました。ここで ``long`` や ``unsigned long`` 型の変数が何であるかを理解しましょう：

  * ``long``: ``long`` 整数は ``int`` の拡張バージョンです。標準の ``int`` の容量を超える大きな整数値を保存するために使用されます。通常、 ``long`` は32ビットまたは64ビットのメモリを占有し、正負の値の両方で非常に大きな値を保持できます。
  * ``unsigned long`` : ``unsigned long`` は ``long`` に似ていますが、正の値のみを表すことができます。符号のために予約されたビットを使用して、保持できる値の範囲を拡張しますが、正の範囲に限定されます。

7. 完成したコードは以下の通りです。今すぐ「アップロード」ボタンをクリックして、コードをArduino Uno R3にアップロードできます。

.. code-block:: Arduino

  #define TRIGGER_PIN  8
  #define ECHO_PIN     7

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Set the Trig pin as output
    pinMode(ECHO_PIN, INPUT);      // Set the Echo pin as input
    Serial.begin(9600);            // Start serial communication for debugging
  }

  void loop() {
    long distance = measureDistance(); // Call the function to measure distance
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    delay(100);  // Delay between measurements
  }

  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Ensure Trig pin is low before a pulse
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH); // Send a high pulse
    delayMicroseconds(10);           // Pulse duration of 10 microseconds
    digitalWrite(TRIGGER_PIN, LOW);  // End the high pulse

    long duration = pulseIn(ECHO_PIN, HIGH);  // Measure the duration of high level on Echo pin
    long distance = duration * 0.034 / 2;     // Calculate the distance (in cm)
    return distance;
  }

8. シリアルモニタを開くと、距離の値が表示されます。超音波センサーの前に物体を動かして、表示される距離が変わるか確認できます。変わる場合、それは超音波モジュールが正常に機能していることを示します。

.. code-block::

  Distance: 30 cm
  Distance: 29 cm
  Distance: 28 cm
  Distance: 27 cm
  Distance: 26 cm
  Distance: 25 cm
  Distance: 25 cm

9. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**質問**

この装置で検出される距離を小数点以下までより正確にしたい場合、コードをどのように修正すべきでしょうか？

コード作成 - スマートゴミ箱
-------------------------------------
超音波モジュールを使って物体までの距離を測定する方法はすでに学びました。次に、スマートゴミ箱を作成するためのコードを書いてみましょう。このゴミ箱は、超音波センサーが20cm以内に物体を検出すると自動的にフタを開けます。ゴミを捨てた後、フタは自動的に閉じます。

フタの動作はサーボモーターによって制御されます：

* サーボ角度が90度のとき、サーボシャフトはサーボと平行になり、ゴミ箱のフタは閉じています。
* 0度では、サーボシャフトはサーボに対して垂直になり、シャフトに取り付けられたロッドによってフタが持ち上げられ開きます。

これをコードでどのように実装するかを見てみましょう。

1. 以前保存したスケッチ ``Lesson19_Read_Distance`` を開きます。「ファイル」メニューから「名前を付けて保存」を選択し、名前を ``Lesson19_Smart_Trashcan`` に変更して「保存」をクリックします。

2. サーボを制御するために、 ``Servo`` ライブラリをインクルードし、サーボを制御するための ``Servo`` クラスのインスタンスを作成します。

.. code-block:: Arduino
  :emphasize-lines: 1,3

  #include <Servo.h>

  Servo myServo;  // サーボオブジェクトの作成

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7

3. まずサーボピンを定義し、ゴミ箱のフタを開ける角度と閉じる角度をそれぞれ格納するために、 ``openAngle`` および ``closeAngle`` の2つの変数を作成します。

.. code-block:: Arduino
  :emphasize-lines: 9-11

  #include <Servo.h>

  Servo myServo;  // Create a Servo object

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7

  // Set up the servo motor parameters
  const int servoPin = 9;
  const int openAngle = 0;
  const int closeAngle = 90;

4. ``void setup()`` 関数内で、サーボオブジェクトを指定したピンにアタッチします。

.. code-block:: Arduino
  :emphasize-lines: 6

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Set the Trig pin as output
    pinMode(ECHO_PIN, INPUT);      // Set the Echo pin as input
    Serial.begin(9600);            // Start serial communication for debugging

    myServo.attach(servoPin);
  }

5. これでメインプログラムに移ります。プログラムの処理に干渉しないように、3つのシリアルプリントステートメントのコードをコメントアウトします。

.. code-block:: Arduino 
  :emphasize-lines: 6

  void loop() {
    long distance = measureDistance();  // Call the function to measure distance
    // Serial.print("Distance: ");
    // Serial.print(distance);
    // Serial.println(" cm");
    delay(100);  // Delay between measurements
  }

6. 計画通り、超音波センサーが20cm未満の距離を検出した場合、サーボが0度に回転してゴミ箱のフタを開けるべきです。そうでない場合、サーボは90度のままでフタを閉じたままにします。

  * ``delay(2000);`` は、フタが閉じる前にゴミを捨てるのに十分な時間を与えるために使用します。必要に応じて、このタイミングを調整できます。
  * ``if (distance > 2 && distance < 20)`` の条件で、 ``distance > 2`` を使用して無効な値を除外します。超音波センサーの有効検出範囲は2cmから400cmです。距離が遠すぎるか近すぎる場合、無効な値である-1または0が返されます。

.. code-block:: Arduino
  :emphasize-lines: 7-12

  void loop() {
    long distance = measureDistance();  // Call the function to measure distance
    // Serial.print("Distance: ");
    // Serial.print(distance);
    // Serial.println(" cm");

    if (distance > 2 && distance < 20) {
      myServo.write(openAngle);
      delay(2000);
    } else {
      myServo.write(closeAngle);
    }

    delay(100);  // Delay between measurements
  }

7. 完成したコードは以下のとおりです。アップロードして、ゴミを捨てた後にゴミ箱が自動的に開閉するかどうかをテストしてみてください。

.. code-block:: Arduino

  #include <Servo.h>

  Servo myServo;  // Create a Servo object

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7

  // Set up the servo motor parameters
  const int servoPin = 9;
  const int openAngle = 0;
  const int closeAngle = 90;

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Set the Trig pin as output
    pinMode(ECHO_PIN, INPUT);      // Set the Echo pin as input
    Serial.begin(9600);            // Start serial communication for debugging

    myServo.attach(servoPin);
  }

  void loop() {
    long distance = measureDistance();  // Call the function to measure distance
    // Serial.print("Distance: ");
    // Serial.print(distance);
    // Serial.println(" cm");

    if (distance > 2 && distance < 20) {
      myServo.write(openAngle);
      delay(2000);
    } else {
      myServo.write(closeAngle);
    }

    delay(100);  // Delay between measurements
  }

  // Function to read the sensor data and calculate the distance
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Ensure Trig pin is low before a pulse
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Send a high pulse
    delayMicroseconds(10);            // Pulse duration of 10 microseconds
    digitalWrite(TRIGGER_PIN, LOW);   // End the high pulse

    long duration = pulseIn(ECHO_PIN, HIGH);  // Measure the duration of high level on Echo pin
    long distance = duration * 0.034 / 2;     // Calculate the distance (in cm)
    return distance;
  }

8. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**まとめ**

今回は、20cm以内に物体があると自動的にフタが開くスマートゴミ箱を無事に作成しました。超音波センサーがどのように機能するか、エコーロケーションに似た仕組みを学び、この技術を使ってサーボモーターを制御しました。また、配線のベストプラクティスを検討し、効果的なArduinoプログラミングのためのヒントも提供しました。プロジェクトのインタラクティブな性質により、センサーとサーボモーターの現実世界での応用に関する実践的な経験を得ることができました。

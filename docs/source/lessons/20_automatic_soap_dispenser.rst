.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebookで、ラズベリーパイ、Arduino、ESP32に興味を持つ仲間たちと共に、これらのデバイスをさらに深く探求しましょう。

    **参加する理由**

    - **専門的なサポート**: コミュニティとチームの助けを借りて、購入後の問題や技術的な課題を解決できます。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **限定プレビュー**: 新製品の発表やスニークピークにいち早くアクセスできます。
    - **特別割引**: 最新製品に対する限定割引をお楽しみください。
    - **フェスティブプロモーションとプレゼント**: プレゼントやホリデープロモーションに参加しましょう。

    👉 私たちと一緒に探索し、創造する準備ができましたか？[|link_sf_facebook|] をクリックして、今すぐ参加しましょう！

.. _automatic_soap_dispenser:

20. 自動ソープディスペンサー
================================

Arduino技術を使用して自動ソープディスペンサーを構築するコースへようこそ！このコースでは、自動化システムの魅力的な世界を探求し、シンプルな電子機器が日常の物をどのように大幅に改善できるかを学びます。私たちの焦点は、手の近接を感知して自動的にソープを分配する装置を作成することにあります。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/20_automatic_soap_dispenser.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンの終わりには、以下のことができるようになります：


* 水ポンプの動作原理について学ぶ。
* 超音波センサーによる距離測定を利用して、手の近接に反応する自動ソープディスペンサーを開発する。

回路の構築
------------------------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * ポンプ
     - 1 * 超音波モジュール
     - 1 * L293Dチップ
   * - |list_uno_r3|
     - |list_pump| 
     - |list_ultrasonic|
     - |list_l293d|
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - ジャンパーワイヤー
     - 1 * ブレッドボードパワーモジュール
   * - |list_usb_cable|
     - |list_breadboard|
     - |list_wire|
     - |list_power_module|
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

.. image:: img/20_dispenser_connect_pump.png
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

2. 超音波モジュールをブレッドボードに挿入します。

.. image:: img/20_dispenser_ultrasonic.png
    :width: 400
    :align: center


3. 超音波モジュールのVCCピンをブレッドボードの正極側に、TrigピンをArduinoボードのピン8に、Echoピンをピン7に、GNDピンをブレッドボードの負極側に接続します。

.. image:: img/20_dispenser_ultrasonic_pins.png
    :width: 400
    :align: center

4. 水ポンプを見つけます。

.. image:: img/20_despenser_pump.png
  :width: 200
  :align: center


これはDC 2.5-6Vのミニ水中ポンプで、卓上噴水や水槽、ハイドロポニクスシステムなどの小規模なプロジェクトに最適です。

このポンプは遠心力を利用しており、電動モーターを使って回転エネルギーを流体力学的エネルギーに変換し、水を効率的に移動させます。設置とメンテナンスが簡単で、DIY愛好家にとって信頼性の高い選択です。

.. image:: img/20_despenser_pump_intro.png
  :width: 400
  :align: center


5. 水ポンプにはモータードライバーチップも必要です。では、L293Dチップをブレッドボードの中央の切り欠き部分に挿入しましょう。チップの切り欠きが左を向くようにしてください。

.. image:: img/20_dispenser_l293d.png
  :width: 600
  :align: center

6. L293Dチップのピンを次のように接続します。

* **1(1,2EN)**: チップを有効にするためにブレッドボードの正極レールに接続します。
* **4(GND)**: チップをグランドするためにブレッドボードの負極レールに接続します。
* **8(VCC2)**: モーターに電力を供給するためにブレッドボードの正極レールに接続します。
* **16(VCC1)**: チップに電力を供給するためにブレッドボードの正極レールに接続します。

.. image:: img/20_dispenser_l293d_power_pins.png
  :width: 600
  :align: center

7. モーターとは異なり、水ポンプには回転方向を区別する必要はありません。2つのピン間に電圧差を与えるだけで水の汲み上げが始まります。したがって、L293Dのピン2（1A）をArduino Uno R3のピン2に接続し、ピン3（1Y）を水ポンプに接続し、水ポンプの他のピンをGNDに接続します。

* ピン2を高に設定するだけで、水ポンプが動作を開始します。

.. image:: img/20_dispenser_connect_pump.png
  :width: 600
  :align: center

コード作成 - 水ポンプを動作させる
---------------------------------------------

まず、水ポンプの動作を確認しましょう。水ポンプを完全に浸すことができるだけの水を入れたコップと、汲み上げた水を集めるための空のコップを用意します。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Lesson20_Pump`` として保存します（ ``Ctrl + S`` または「保存」をクリックして行います）。

3. 水ポンプの操作は、LEDを点灯させるのと同じくらい簡単です。ポンプ制御ピンを初期化し、出力として設定し、次にそれを高に設定します。

.. code-block:: Arduino

  #define PUMP_PIN     2  // pump control pin

  void setup() {
    pinMode(PUMP_PIN, OUTPUT);    // Set the pump control pin as output
  }

  void loop() {
    digitalWrite(PUMP_PIN, HIGH);       // Turn on the pump at full speed
  }

4. コードはこれで完成です。Arduino Uno R3ボードにアップロードできます。アップロード後、ポンプのチューブを通じて水が満たされたコップから空のコップへ移動するのが確認できるでしょう。

**質問**

このプロジェクトでは、特定のドライバーとセットアップを使用して水ポンプを接続しました。もしポンプの接続を逆にした場合、何が起こると思いますか？ポンプは逆回転するのか、それとも動作を停止するのか、それとも何か他のことが起きるのでしょうか？これを試して、その結果を考えてみてください。

.. image:: img/20_despenser_pump_change.png
  :width: 600
  :align: center

コード作成 - 自動ソープディスペンサー
-------------------------------------------
ここでは、ソープ液を抽出する水ポンプを利用した自動ソープディスペンサーを構築します。このディスペンサーは、手の近接を検知する超音波センサーによって作動します。センサーで測定された距離が10cm未満の場合、手が近くにあると判断され、ディスペンサーがソープを排出します。

ソープの使用量を抑えるために、ポンプは500ミリ秒間だけ動作してソープを分配します。2秒間の停止後も手が検知されている場合、ポンプは再び500ミリ秒間作動して、十分な量のソープが分配されるようにします。このセットアップにより、効率的にソープを管理しつつ、ユーザーのニーズに対応します。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Lesson20_Soap_Dispenser`` として保存します（ ``Ctrl + S`` または「保存」をクリックして行います）。

3. 超音波センサーの2つのピンとポンプのピンを初期化します。

.. code-block:: Arduino
  :emphasize-lines: 1-3

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7
  #define PUMP_PIN 2  // pump control pin

  void setup() {
    // put your setup code here, to run once:

  }

4. ``void setup()`` 関数内で、プロジェクトで使用する各ピンのモードを設定し、センサー出力のデバッグとモニタリングのために9600 bpsでシリアル通信を初期化します。

.. code-block:: Arduino
  :emphasize-lines: 6-9

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7
  #define PUMP_PIN 2  // pump control pin

  void setup() {
    pinMode(PUMP_PIN, OUTPUT);     // Set the pump control pin as output
    pinMode(TRIGGER_PIN, OUTPUT);  // Set the Trig pin as output
    pinMode(ECHO_PIN, INPUT);      // Set the Echo pin as input
    Serial.begin(9600);            // Start serial communication for debugging
  }

5. 超音波モジュールで測定された距離を取得するための特定の関数が必要です。この関数の実装方法については、:ref:`ar_read_distance` を参照してください。

.. code-block:: Arduino
  :emphasize-lines: 7-17
  
  void loop() {
    // put your main code here, to run repeatedly:

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

6. 次に、 ``void loop()`` 関数に移動し、 ``measureDistance()`` 関数を呼び出して測定された距離を ``distance`` 変数に格納し、シリアルモニターに出力します。

.. code-block:: Arduino
  :emphasize-lines: 2-4

  void loop() {
    long distance = measureDistance();  // Call the function to measure distance
    Serial.println(distance);
    delay(100);  // Delay between measurements
  }

7. 次に、距離に基づいてポンプの動作状態を決定します。距離が2cmから10cmの間であれば、ポンプが作動して500ミリ秒間ソープを分配し、その後ポンプを停止し、2秒待ってから再度作動します。

.. code-block:: Arduino
  :emphasize-lines: 5-12

  void loop() {
    long distance = measureDistance();  // Call the function to measure distance
    Serial.println(distance);

    if (distance > 2 && distance < 10) {  // If distance is between 2-10cm
      digitalWrite(PUMP_PIN, HIGH);       // Turn on the pump
      delay(500);
      digitalWrite(PUMP_PIN, LOW);  // Turn off the pump
      delay(2000);
    } else {
      digitalWrite(PUMP_PIN, LOW);  // Turn off the pump
    }
    delay(100);  // Delay between measurements
  }

8. 完成したコードは以下の通りです。これをArduino Uno R3ボードにアップロードしてください。

.. code-block:: Arduino

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7
  #define PUMP_PIN 2  // pump control pin

  void setup() {
    pinMode(PUMP_PIN, OUTPUT);     // Set the pump control pin as output
    pinMode(TRIGGER_PIN, OUTPUT);  // Set the Trig pin as output
    pinMode(ECHO_PIN, INPUT);      // Set the Echo pin as input
    Serial.begin(9600);            // Start serial communication for debugging
  }

  void loop() {
    long distance = measureDistance();  // Call the function to measure distance
    Serial.println(distance);

    if (distance > 2 && distance < 10) {  // If distance is between 2-10cm
      digitalWrite(PUMP_PIN, HIGH);       // Turn on the pump
      delay(500);
      digitalWrite(PUMP_PIN, LOW);  // Turn off the pump
      delay(2000);
    } else {
      digitalWrite(PUMP_PIN, LOW);  // Turn off the pump
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

9. 最後に、コードを保存して作業スペースを整理することを忘れないでください。


**まとめ**

今日のレッスンでは、自動ソープディスペンサーの構築とプログラミングに成功しました。超音波センサーを使用して近接検知を行い、Arduinoプログラミングを通じて水ポンプを制御する方法を学びました。今日習得したスキルは、電子回路の理解を深めるだけでなく、将来のプロジェクトの幅広い可能性を開くものです。


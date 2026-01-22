.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebookへようこそ！このコミュニティで、Raspberry Pi、Arduino、ESP32についてさらに深く学び、他の愛好者たちと一緒に楽しみましょう。

    **参加する理由**

    - **専門家サポート**: 購入後の問題や技術的な課題を、コミュニティやチームの助けを借りて解決できます。
    - **学びと共有**: スキルを高めるためのヒントやチュートリアルを交換できます。
    - **限定プレビュー**: 新製品の発表やプレビューをいち早く受け取れます。
    - **特別割引**: 最新製品に対して、特別割引を楽しめます。
    - **イベントプロモーションとプレゼント**: プレゼントやホリデープロモーションに参加できます。

    👉 私たちと一緒に探求し、創造する準備ができましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

25. リバースレーダーシステム
=====================================

車をバックさせる際、特に視界が限られた状況では、車両の後方にある障害物を把握することが非常に重要です。
安全性を高めるために、多くの現代の車両にはリバースレーダーシステムが装備されています。

今日は、Arduinoを使用して超音波レーダーシステムを構築し、プログラムする方法を学びます。このシステムでは、超音波センサーを使用して距離を測定し、LCDディスプレイとブザーを通じてフィードバックを提供します。コードの各部分を段階的に解説し、その重要性についても説明します。

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/25_reverse_alarm.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

リバースレーダーシステムの進化
----------------------------------------

リバースレーダーシステム、またはパーキングセンサーの開発は、より安全な車両駐車のニーズに応えるために20世紀後半に始まりました。最初は1970年代に海洋ソナーと同様の超音波技術を使用して開発され、音波を使って物体を検出し、距離を計算していました。

1990年代には、マイクロコントローラーを搭載したシステムや電磁センサーの導入により、より正確な測定と車両への統合が進みました。この時期には、これらのセンサーが高級車に搭載され、安全性とラグジュアリー性が向上しました。

2000年代初頭までに、リバースレーダーシステムは視覚、聴覚、触覚フィードバック、デジタルディスプレイ、車両ナビゲーションシステムとの統合を含むまでに進化し、ドライバーにリアルタイムでわかりやすい情報を提供するようになりました。

今日では、この技術はAIやIoTと統合され、カメラ、レーダー、超音波センサーの組み合わせを利用して車両の周囲を詳細に把握し、事故のリスクを減らし、駐車を容易にしています。この技術は、自動運転システムの基本要素となり、今後の自動車産業の革新を支えるでしょう。

.. image:: img/25_reverse_radar.png
  :width: 600
  :align: center

回路の構築
--------------------------------

**必要な部品**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 超音波モジュール
     - 1 * アクティブブザー
     - 1 * I2C LCD1602
   * - |list_uno_r3| 
     - |list_ultrasonic| 
     - |list_active_buzzer| 
     - |list_i2c_lcd1602|
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - ジャンパーワイヤー
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - 

**段階的な構築手順**

回路を構築するには、配線図または以下の手順に従ってください。

.. image:: img/25_reverse_circuit.png
    :width: 700
    :align: center

1. 超音波モジュールをブレッドボードに挿入します。

.. image:: img/25_reverse_ultrasonic.png
    :width: 400
    :align: center

2. 超音波モジュールのVCCピンをブレッドボードの正極側に接続し、TrigピンをArduinoボードのピン8に、Echoピンをピン7に、GNDをブレッドボードの負極側に接続します。

.. image:: img/25_reverse_ultrasonic_pins.png
    :width: 400
    :align: center

3. 白いステッカーのついたアクティブブザーをブレッドボードに挿入します。"+"ピンをピン9に、"-"ピンをGNDに接続します。

.. image:: img/25_reverse_pa_buzzer.png
    :width: 400
    :align: center

4. I2C LCD1602モジュールを接続します：GNDをブレッドボードの負極レールに、VCCを正極レールに、SDAをピンA4に、SCLをピンA5に接続します。

.. image:: img/25_reverse_i2c_lcd1602.png
    :width: 700
    :align: center

5. 最後に、Arduino Uno R3のGNDと5Vピンをそれぞれブレッドボードの負極と正極レールに接続します。

.. image:: img/25_reverse_circuit.png
    :width: 700
    :align: center

コード作成
--------------------
リバースレーダーシステムでは、各コンポーネントが正確な距離測定と効果的なフィードバックを保証するために重要な役割を果たします：

* 超音波センサーは、前方の物体までの距離を検出します。
* I2C LCD1602は、超音波センサーで検出された距離を表示します。
* アクティブブザーは、超音波センサーで測定された距離に基づいてビープ音の間隔を変化させます。

システムは、以下の距離範囲に基づいて反応します：

* **10cm未満** : ブザーが100ミリ秒の間隔で急速にビープ音を鳴らします。
* **10cmから20cmの間** : ビープ音の間隔が500ミリ秒に増加します。
* **20cmから50cmの間** : 間隔がさらに延び、1000ミリ秒（1秒）になります。
* **50cm以上** : ブザーが2000ミリ秒（2秒）の間隔でゆったりとビープ音を鳴らします。

それでは、上記の機能を実装するためのコーディングを開始しましょう。

.. note::

  超音波センサー、I2C LCD1602、またはアクティブブザーの基本的な使用方法に慣れていない場合は、以下のプロジェクトで基礎を学ぶことができます：

  * :ref:`ar_i2c_lcd1602`
  * :ref:`ar_smart_trash_can`
  * :ref:`ar_morse_code`

1. Arduino IDEを開き、「ファイル」メニューから「新規スケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Lesson25_Reverse_Radar_System`` として保存します。 ``Ctrl + S`` または「保存」をクリックしてください。

3. まず、LCDを使用するために必要なライブラリをインクルードし、正しいI2Cアドレスとサイズで初期化します。

.. note::

  ここでは ``LiquidCrystal I2C`` ライブラリを使用します。 **ライブラリマネージャ** からインストールできます。

.. code-block:: Arduino

  #include <Wire.h>
  #include <LiquidCrystal_I2C.h>

  // Initialize the LCD with I2C address 0x27 and size 16x2
  LiquidCrystal_I2C lcd(0x27, 16, 2);


4. 次に、Arduinoのピンと超音波センサーのトリガー、エコー、およびブザーを接続するためのピンを定義します。

.. code-block:: Arduino

  #define TRIGGER_PIN 8  // Pin to trigger the ultrasonic pulse
  #define ECHO_PIN 7     // Pin to receive the echo
  #define BUZZER_PIN 9   // Pin for the buzzer

5. 測定された距離に基づいて、ブザーがどのくらいの頻度でビープ音を鳴らすかを制御するための変数を設定します。

.. code-block:: Arduino

  // Timing variables to control the beeping frequency based on distance
  unsigned long intervals = 1000;    // Default interval for beeping
  unsigned long previousMillis = 0;  // Store last time the buzzer beeped

  // 距離測定用の変数
  long distance = 0;

6. ``void setup()`` 関数で、ピンモードを設定し、LCDとシリアル通信を初期化します。

.. code-block:: Arduino

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Set the trigger pin as output
    pinMode(ECHO_PIN, INPUT);      // Set the echo pin as input
    pinMode(BUZZER_PIN, OUTPUT);   // Set the buzzer pin as output
    lcd.init();                    // Initialize the LCD
    lcd.backlight();               // Turn on LCD backlight
    Serial.begin(9600);            // Start serial communication at 9600 baud rate
  }

7. メインループでは、距離を連続的に測定し、ビープ音の間隔を調整し、LCDディスプレイを更新します。

.. code-block:: Arduino

  void loop() {
    distance = measureDistance();  // Measure distance

    // Adjust intervals based on distance
    adjustBeepingInterval();

    unsigned long currentMillis = millis();  // Get current time
    // Check if it's time to beep
    if (currentMillis - previousMillis >= intervals) {
      Serial.println("Beeping!");
      beep();
      previousMillis = currentMillis;  // Update previousMillis directly here
    }

    updateLCD();  // Update the LCD display
    delay(100);   // Short delay to stabilize readings
  }

* まず、 ``measureDistance()`` 関数を使用して、超音波センサーを用いて距離を測定します。

.. code-block:: Arduino

  distance = measureDistance();  // Measure distance

* 次に、 ``adjustBeepingInterval()`` 関数を使用して、新たに測定された距離に基づいてビープ音の周波数を調整します。これにより、検出された物体が近づくほどブザーの鳴る頻度が動的に変わります。

.. code-block:: Arduino

  // Adjust intervals based on distance
  adjustBeepingInterval();

* 次に、 ``millis()`` 関数を呼び出して、Arduinoボードがプログラムを実行し始めてからのミリ秒数を記録します。

.. code-block:: Arduino

  unsigned long currentMillis = millis();

* 最後のビープ音から経過した時間が設定された間隔以上であるかどうかを確認します。もしそうであれば、シリアルモニターにメッセージを表示し、ブザーを作動させ、 ``previousMillis`` をリセットします。これにより、距離に応じて調整された間隔でブザーが動作し、一貫した警告タイミングが維持されます。

.. code-block:: Arduino
  
  if (currentMillis - previousMillis >= intervals) {
    Serial.println("Beeping!");
    beep();
    previousMillis = currentMillis;  // Update previousMillis directly here
  }
 
* 最後に、 ``updateLCD()`` 関数を呼び出して、現在の距離測定値でLCDを更新します。

.. code-block:: Arduino

  updateLCD();  // Update the LCD display

8. ``adjustBeepingInterval()`` 関数について: 測定された距離に基づいてビープ音の間隔を調整します。この関数は ``intervals`` 変数を設定します。物体が近づくほど、間隔が短くなり、物体が近づくにつれてブザーが頻繁に鳴ります。

.. code-block:: Arduino

  // Function to adjust intervals based on distance
  void adjustBeepingInterval() {
    if (distance <= 10) {
      intervals = 100;
    } else if (distance <= 20) {
      intervals = 500;
    } else if (distance <= 50) {
      intervals = 1000;
    } else {
      intervals = 2000;
    }
  }

9. ``beep()`` 関数について: ブザーをオンにし、短い間隔の後にオフにします。

.. code-block:: Arduino

  // Function to make buzzer beep
  void beep() {
    digitalWrite(BUZZER_PIN, HIGH);  // Turn buzzer ON
    delay(100);                      // Beep duration: 100 milliseconds
    digitalWrite(BUZZER_PIN, LOW);   // Turn buzzer OFF
  }

10. ``measureDistance()`` 関数について: 超音波センサーを使用して距離を測定します。この関数は超音波を発信し、その反射が戻ってくるまでの時間を測定します。この波の移動時間に基づいて ``distance`` が計算されます。

.. code-block:: Arduino

  // Function to measure distance using the ultrasonic sensor
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Ensure trigger pin is low
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Send a high pulse
    delayMicroseconds(10);            // Pulse duration
    digitalWrite(TRIGGER_PIN, LOW);   // End the pulse

    long duration = pulseIn(ECHO_PIN, HIGH);  // Measure the duration of high level on Echo pin
    long distance = duration * 0.034 / 2;     // Calculate the distance in cm
    return distance;
  }

11. ``updateLCD()`` 関数について: 測定された距離が変わった場合のみLCDを更新し、不要な更新を減らします。これにより、現在の距離がLCDに表示されます。

.. code-block:: Arduino

  // Function to update the LCD display with distance
  void updateLCD() {
    static float lastDistance = -1;  // Store last distance displayed
    if (distance != lastDistance) {
      lcd.clear();          // Clear LCD display
      lcd.setCursor(0, 0);  // Set cursor at beginning
      lcd.print("Dis: ");
      lcd.print(distance);
      lcd.print(" cm");
      lastDistance = distance;  // Update last displayed distance
    }
  }

12. すべてのコード部分を書き終えたら、Arduinoボードにアップロードして期待どおりに動作するか確認してください。

.. code-block:: Arduino

  #include <Wire.h>
  #include <LiquidCrystal_I2C.h>

  // Initialize the LCD with I2C address 0x27 and size 16x2
  LiquidCrystal_I2C lcd(0x27, 16, 2);

  #define TRIGGER_PIN 8  // Pin to trigger the ultrasonic pulse
  #define ECHO_PIN 7     // Pin to receive the echo
  #define BUZZER_PIN 9   // Pin for the buzzer

  // Timing variables to control the beeping frequency based on distance
  unsigned long intervals = 1000;    // Default interval for beeping
  unsigned long previousMillis = 0;  // Store last time the buzzer beeped

  // Distance measurement variable
  long distance = 0;

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Set the trigger pin as output
    pinMode(ECHO_PIN, INPUT);      // Set the echo pin as input
    pinMode(BUZZER_PIN, OUTPUT);   // Set the buzzer pin as output
    lcd.init();                    // Initialize the LCD
    lcd.backlight();               // Turn on LCD backlight
    Serial.begin(9600);            // Start serial communication at 9600 baud rate
  }

  void loop() {
    distance = measureDistance();  // Measure distance

    // Adjust intervals based on distance
    adjustBeepingInterval();

    unsigned long currentMillis = millis();  // Get current time
    // Check if it's time to beep
    if (currentMillis - previousMillis >= intervals) {
      Serial.println("Beeping!");
      beep();
      previousMillis = currentMillis;  // Update previousMillis directly here
    }

    updateLCD();  // Update the LCD display
    delay(100);   // Short delay to stabilize readings
  }

  // Function to adjust intervals based on distance
  void adjustBeepingInterval() {
    if (distance <= 10) {
      intervals = 100;
    } else if (distance <= 20) {
      intervals = 500;
    } else if (distance <= 50) {
      intervals = 1000;
    } else {
      intervals = 2000;
    }
  }

  // Function to make buzzer beep
  void beep() {
    digitalWrite(BUZZER_PIN, HIGH);  // Turn buzzer ON
    delay(100);                      // Beep duration: 100 milliseconds
    digitalWrite(BUZZER_PIN, LOW);   // Turn buzzer OFF
  }

  // Function to measure distance using the ultrasonic sensor
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Ensure trigger pin is low
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Send a high pulse
    delayMicroseconds(10);            // Pulse duration
    digitalWrite(TRIGGER_PIN, LOW);   // End the pulse

    long duration = pulseIn(ECHO_PIN, HIGH);  // Measure the duration of high level on Echo pin
    long distance = duration * 0.034 / 2;     // Calculate the distance in cm
    return distance;
  }

  // Function to update the LCD display with distance
  void updateLCD() {
    static float lastDistance = -1;  // Store last distance displayed
    if (distance != lastDistance) {
      lcd.clear();          // Clear LCD display
      lcd.setCursor(0, 0);  // Set cursor at beginning
      lcd.print("Dis: ");
      lcd.print(distance);
      lcd.print(" cm");
      lastDistance = distance;  // Update last displayed distance
    }
  }


13. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**質問**

このプロジェクトでは、アラートメカニズムとしてアクティブブザーを使用しましたが、パッシブブザーでも同様の機能を実現できます。アクティブブザーをパッシブブザーに置き換える場合、コードをどのように修正する必要がありますか？

**まとめ**

この授業を通じて、逆転レーダーシステムの概念的理解から実際の実装までの道のりを辿りました。ブレッドボード上で回路を組み立てることから始まり、超音波センサー、アクティブブザー、およびLCDディスプレイをArduinoボードに接続しました。ハードウェアのセットアップの後、コード作成に進み、センサーデータを操作して、車両後方の障害物の距離に基づいて音声および視覚フィードバックをトリガーする方法を学びました。

あなたは現在、Arduinoをプログラムして距離を測定し、ブザーを通じたアラートやLCDによる視覚フィードバックを提供することに成功し、現代の車両に搭載されている高度な逆転レーダーシステムの機能を模倣しています。これにより、さまざまな電子部品を統合する能力が示されるだけでなく、車両の安全性を向上させるシステムを作成するスキルも強調されます。


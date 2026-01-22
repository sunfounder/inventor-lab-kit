.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebookで仲間と一緒にRaspberry Pi、Arduino、ESP32についてさらに深く学びましょう。

    **参加する理由**

    - **専門家サポート**: 購入後の問題や技術的な課題を、コミュニティやチームのサポートで解決。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換。
    - **独占プレビュー**: 新製品の発表や予告をいち早く入手。
    - **特別割引**: 新製品に対する特別割引を享受。
    - **フェスティバルプロモーションとプレゼント企画**: プレゼント企画やホリデープロモーションに参加。

    👉 一緒に探求し、創造しましょう！今すぐ[|link_sf_facebook|]をクリックして参加しませんか？

29. 植物モニター
=========================

Arduinoを使用して植物モニターを作成するインタラクティブなレッスンへようこそ！このレッスンでは、電子部品の世界に触れ、植物のモニタリングシステムを一から組み立てる方法を学びます。

このプロジェクトでは、土壌の湿度が特定のしきい値を下回ると、水ポンプが自動的に作動して植物に水を供給します。さらに、LCDスクリーンに温度、光量、土壌湿度が表示され、植物の成長環境に関するインサイトをユーザーに提供します。

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/29_plant_monitor.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンで学べること:

* 土壌湿度モジュールの仕組みを理解する。
* Arduinoとこれらのセンサーを統合して、植物の健康に影響を与える環境変数をモニタリングする方法を学ぶ。


回路の組み立て
-----------------------

**必要な部品**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * I2C LCD1602
     - 1 * サーミスタ
     - 1 * 光センサー
   * - |list_uno_r3| 
     - |list_i2c_lcd1602|
     - |list_thermistor|
     - |list_photoresistor|
   * - 土壌湿度モジュール
     - 1 * ポンプ
     - 2 * 10KΩ 抵抗
     - 1 * L293D チップ
   * - |list_moisture_module|
     - |list_pump|
     - |list_10kohm|
     - |list_l293d|
   * - ジャンパーワイヤー
     - 1 * USBケーブル
     - 1 * ブレッドボード
     - 1 * ブレッドボード電源モジュール
   * - |list_wire|
     - |list_usb_cable|
     - |list_breadboard|
     - |list_power_module|
   * - 1 * 9V バッテリー
     - 1 * バッテリーケーブル
     - 
     -  
   * - |list_battery| 
     - |list_bat_cable| 
     -
     -

**回路の組み立て手順**


回路図に従うか、以下の手順に従って回路を組み立ててください。

.. image:: img/29_plant_connect_mositure.png
  :width: 800
  :align: center

1. まず、ブレッドボードに電源モジュールを挿入し、ジャンパーワイヤーを使用してブレッドボードの負極レールをArduino Uno R3のGNDに接続し、共通のグラウンドを実現します。

.. image:: img/14_dinosaur_power_module.png
    :width: 400
    :align: center

.. note::

    配線図では、ブレッドボードの正極と負極の端子の順序が、キットに提供されたブレッドボードとは逆になっています。

    実際の配線では、ブレッドボードの電源モジュールを番号の高い側（60-65）から挿入し、電源モジュールの"-"がブレッドボードの負極レール"-"に、"+"が正極レール"+"に接続されるようにする必要があります。

    .. raw:: html

        <video controls style = "max-width:100%">
            <source src="_static/video/about_power_module.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

2. 次に、L293Dチップのピンを以下のように接続します。

* **1(1,2EN)**: ブレッドボードの正極レールに接続して、チップを有効化します。
* **4(GND)**: ブレッドボードの負極レールに接続して、チップをグラウンドします。
* **8(VCC2)**: ブレッドボードの正極レールに接続して、モーターに電力を供給します。
* **16(VCC1)**: ブレッドボードの正極レールに接続して、チップに電力を供給します。

.. image:: img/29_plant_connect_l293d.png
  :width: 500
  :align: center

3. モーターとは異なり、水ポンプは回転方向を区別する必要がありません。単に2つのピン間に電圧差を与えることで水を汲み始めます。したがって、L293Dのピン2（1A）をArduino Uno R3のピン12に、ピン3（1Y）を水ポンプに接続し、水ポンプのもう一方のピンをGNDに接続します。

* ピン12を高レベルに設定するだけで、水ポンプが水を汲み始めます。

.. image:: img/29_plant_connect_pump.png
  :width: 500
  :align: center

4. 回路の組み立てを続けます。光センサーの片方のピンをブレッドボードの負極端子に接続し、もう片方のピンをArduino Uno R3のA0ピンに接続します。

.. image:: img/29_plant_phr.png
    :width: 500
    :align: center

5. フォトレジスタが接続されているA0ピンと同じピンに10KΩ抵抗を挿入します。

.. image:: img/29_plant_phr_resistor.png
    :width: 500
    :align: center

6. 10KΩ抵抗のもう一方のピンをブレッドボードの正極端子に接続します。

.. image:: img/29_plant_phr_vcc.png
    :width: 500
    :align: center

7. サーミスタをフォトレジスタと同様に接続します。サーミスタをブレッドボードに挿入し、一方のピンをブレッドボードの正極レールに、もう一方をA0ピンに接続します。

.. image:: img/29_plant_connect_thermistor.png
    :width: 500
    :align: center

8. サーミスタが接続されているA2ピンと同じピンに10KΩ抵抗を挿入します。

.. image:: img/29_plant_connect_thr_mistor.png
    :width: 500
    :align: center

9. 10KΩ抵抗のもう一方のピンをブレッドボードの負極端子に接続します。

.. image:: img/29_plant_connect_resistor_vcc.png
    :width: 500
    :align: center

10. I2C LCD1602モジュールを接続します。GNDをブレッドボードの負極レールに、VCCを正極レールに、SDAをA4ピンに、SCLをA5ピンに接続します。

    .. image:: img/29_plant_connect_lcd.png
        :width: 800
        :align: center

11. 今回初めて使用する土壌湿度モジュールを探します。これは土壌の湿度を検出するためのモジュールです。

.. image:: img/29_plant_soil_mositure.png
  :width: 500
  :align: center

* **GND**: グラウンド
* **VCC**: 電源供給、3.3V~5V
* **AOUT**: 土壌湿度値を出力し、土壌が湿っているほどその値は小さくなります。

この容量式土壌湿度センサーは、市場にある多くの抵抗式センサーとは異なり、容量式誘導の原理を使用して土壌湿度を検出します。これにより、抵抗式センサーが腐食に非常に敏感であるという問題を回避し、その耐用年数を大幅に延ばします。

腐食に強い素材で作られており、優れた耐久性を誇ります。植物の周りの土壌に挿入してリアルタイムで土壌の湿度データをモニタリングできます。土壌の湿度が高いほどセンサーの容量が高まり、信号線の電圧が低下し、マイクロコントローラーを通じてアナログ入力の値が小さくなります。このモジュールにはオンボードの電圧レギュレータが含まれており、3.3V～5.5Vの電圧範囲で動作できます。

12. 次に、それを回路に接続します。理想的には、VCCとGNDをそれぞれブレッドボードの正極端子と負極端子に接続します。しかし、Arduinoボードを跨いで配線を交差させて干渉を引き起こさないようにするために、VCCとGNDをArduinoボードの5VとGNDピンに接続します。

.. image:: img/29_plant_connect_mositure.png
  :width: 800
  :align: center

コード作成 - 土壌湿度の読み取り
---------------------------------------------
次に、土壌湿度センサーから値を読み取るコードを作成します。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2. 「Ctrl + S」を押すか「保存」をクリックして、スケッチを ``Lesson29_Read_Soil_Noisture`` として保存します。

3. 次に、土壌湿度モジュールから値を読み取るコードを作成します。

.. code-block:: Arduino

  const int moisturePin = A1;  // Define the pin where the soil moisture sensor is connected

  void setup() {
    Serial.begin(9600);  // Initialize serial communication at 9600 baud rate
  }

  void loop() {
    int moistureValue = analogRead(moisturePin);  // Read the analog value from the moisture sensor
    Serial.print("Moisture Value: ");
    Serial.println(moistureValue);  // Output the raw sensor value to the serial monitor for observation

    delay(1000);  // Delay for one second before the next reading to reduce data flooding
  }


4. コードを実行した後、土壌湿度モジュールを土壌に挿入する必要があります。土壌に水を供給すると、表示される読み取り値が低下することに気付くでしょう。さらに、土壌の湿度の変化は線形ではなく、ゆっくりと変化します。

.. code-block:: Arduino

  Moisture Value: 438
  Moisture Value: 438
  Moisture Value: 378
  Moisture Value: 354
  Moisture Value: 323
  Moisture Value: 210

**質問**

提供されたコードでは、湿度が高いほどセンサーの値が低くなることがわかります。湿度は通常、パーセンテージで表されます。土壌湿度レベルをパーセンテージで表示するようにコードをどのように変更できますか？


コード作成 - 植物モニター
---------------------------------------------
前のプロジェクトから、土壌湿度モジュールのデータ変化を理解しました。次に、土壌湿度モジュール、光センサー、サーミスタ、水ポンプ、I2C LCD1602を使用して、植物モニタリングシステムを作成します。

* サーミスタは温度を検出し、LCDに摂氏と華氏の両方を表示します。
* 光センサーは光の状態を検出し、LCDに表示します。
* 土壌湿度モジュールは土壌湿度のパーセンテージを検出し、LCDに表示します。
* 検出された土壌湿度が35％未満の場合、水ポンプが3秒間作動し、次のチェックでも35％未満である場合、再び3秒間作動します。設定された土壌湿度のしきい値に達するまで、複数回の短時間の散水が行われます。

では、目的の効果を実現するためにコードを書いてみましょう。

.. note::

  サーミスタ、光センサー、ポンプ、またはI2C LCD1602に慣れていない場合は、以下のプロジェクトで基本的な使い方を学ぶことができます。

  * :ref:`ar_temperature`
  * :ref:`ar_photoresistor`
  * :ref:`automatic_soap_dispenser` 
  * :ref:`ar_i2c_lcd1602`

  ここでは ``LiquidCrystal I2C`` ライブラリを使用します。ライブラリマネージャーからインストールできます。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2.  ``Ctrl + S`` を押すか「保存」をクリックして、スケッチを ``Lesson29_plant_monitor`` として保存します。

3. では、コーディングを開始しましょう。I2C LCD1602に必要なライブラリをインクルードし、そのアドレスとディスプレイを初期化します。次に、各センサーのピンを定義します。

.. code-block:: Arduino

  #include <Wire.h>               // Includes I2C communication library
  #include <LiquidCrystal_I2C.h>  // Includes library for controlling the I2C LCD

  LiquidCrystal_I2C lcd(0x27, 16, 2);  // Initializes LCD at address 0x27 for a 16x2 display

  const int lightSensorPin = A0;  // Light sensor
  const int moisturePin = A1;     // Soil moisture sensor
  const int tempSensorPin = A2;   // NTC thermistor
  const int pumpPin = 12;         // Pump

4. 次に、サーミスタに必要なパラメータを定義します。

.. code-block:: Arduino
  :emphasize-lines: 13

  #include <Wire.h>               // Includes I2C communication library
  #include <LiquidCrystal_I2C.h>  // Includes library for controlling the I2C LCD

  LiquidCrystal_I2C lcd(0x27, 16, 2);  // Initializes LCD at address 0x27 for a 16x2 display

  const int lightSensorPin = A0;  // Light sensor
  const int moisturePin = A1;     // Soil moisture sensor
  const int tempSensorPin = A2;   // NTC thermistor
  const int pumpPin = 12;         // Pump

  // Constants for temperature calculation
  const float beta = 3950.0;               // NTC thermistor's Beta value
  const float seriesResistor = 10000;      // Series resistor value (ohms)
  const float roomTempResistance = 10000;  // NTC resistance at 25°C
  const float roomTemp = 25 + 273.15;      // Room temperature in Kelvin

5. ``void setup()`` 関数では、水ポンプのピンを出力に設定し、LCDディスプレイを初期化します。アナログピンはデフォルトで入力モードになっているため、入力/出力モードを手動で設定する必要はありません。

.. code-block:: Arduino

  void setup() {
    pinMode(pumpPin, OUTPUT);  // Sets the pump pin as output
    lcd.init();                // Initializes LCD display
    lcd.backlight();           // Turns on LCD backlight for visibility
  }

6. ``loop()`` 関数で、フォトレジスタ、サーミスタ、および土壌湿度モジュールからの値を読み取り、それらを対応する変数に格納します。土壌湿度を ``map()`` 関数を使用してパーセンテージに変換します。

.. code-block:: Arduino
  :emphasize-lines: 3-5,8

  void loop() {
    // Read sensors
    int tempValue = analogRead(tempSensorPin);
    int lightValue = analogRead(lightSensorPin);
    int moistureValue = analogRead(moisturePin);

    // Calculate soil moisture percentage
    float moisturePercent = map(moistureValue, 0, 1023, 100, 0);
  }

7. 次に、サーミスタの値に基づいて、摂氏温度と華氏温度に変換します。

.. code-block:: Arduino
  :emphasize-lines: 11-14

  void loop() {
    // Read sensors
    int tempValue = analogRead(tempSensorPin);
    int lightValue = analogRead(lightSensorPin);
    int moistureValue = analogRead(moisturePin);

    // Calculate soil moisture percentage
    float moisturePercent = map(moistureValue, 0, 1023, 100, 0);

    // Calculate temperature in Celsius
    float resistance = (1023.0 / tempValue - 1) * seriesResistor;
    float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    float tempC = tempK - 273.15;
    float tempF = tempC * 9.0 / 5.0 + 32.0;
  }

8. 次に、I2C LCDにデータを表示します。まず、 ``lcd.clear()`` 関数を使用してLCD上のデータをクリアし、次に1行目に摂氏温度を、2行目に華氏温度を表示して2秒間保持します。

.. code-block:: Arduino
  :emphasize-lines: 8-15

  // Calculate temperature in Celsius
  float resistance = (1023.0 / tempValue - 1) * seriesResistor;
  float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
  float tempC = tempK - 273.15;
  float tempF = tempC * 9.0 / 5.0 + 32.0;

  // Display Temperature
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Temp C: ");
  lcd.print(tempC);
  lcd.setCursor(0, 1);
  lcd.print("Temp F: ");
  lcd.print(tempF);
  delay(2000);

9. 次に、光のデータを1行目に、土壌湿度のパーセンテージを2行目に表示し、同様に2秒間保持します。

.. code-block:: Arduino
  :emphasize-lines: 12-20

  // Display Temperature
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Temp C: ");
  lcd.print(tempC);
  lcd.setCursor(0, 1);
  lcd.print("Temp F: ");
  lcd.print(tempF);
  delay(2000);

  // Display light and soil moisture
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Light: ");
  lcd.print(lightValue);
  lcd.setCursor(0, 1);
  lcd.print("Soil: ");
  lcd.print(moisturePercent);
  lcd.print("%");
  delay(2000);

10. 次に、土壌湿度が35%未満の場合に水ポンプを3秒間作動させるように、 ``if`` ステートメントを使用してポンプを制御します。このしきい値は、実際の条件に応じて調整可能です。ポンプが停止した後、LCDの表示が乱れるのを防ぐために ``lcd.init()`` を呼び出して再初期化します。

.. code-block:: Arduino
  :emphasize-lines: 2-7

  // Control pump if soil moisture is below 35%
  if (moisturePercent < 35) {
    digitalWrite(pumpPin, HIGH);  // Turn on pump
    delay(3000);
    digitalWrite(pumpPin, LOW);  // Turn off pump
    lcd.init(); // Reinitialize LCD to prevent display corruption
  }

11. 以下に完成したコードを示します。これをArduinoにアップロードして、設定された効果が得られるか確認してください。

.. code-block:: Arduino

  #include <Wire.h>               // Includes I2C communication library
  #include <LiquidCrystal_I2C.h>  // Includes library for controlling the I2C LCD

  LiquidCrystal_I2C lcd(0x27, 16, 2);  // Initializes LCD at address 0x27 for a 16x2 display

  const int lightSensorPin = A0;  // Light sensor
  const int moisturePin = A1;     // Soil moisture sensor
  const int tempSensorPin = A2;   // NTC thermistor
  const int pumpPin = 12;         // Pump

  // Constants for temperature calculation
  const float beta = 3950.0;               // NTC thermistor's Beta value
  const float seriesResistor = 10000;      // Series resistor value (ohms)
  const float roomTempResistance = 10000;  // NTC resistance at 25°C
  const float roomTemp = 25 + 273.15;      // Room temperature in Kelvin

  void setup() {
    pinMode(pumpPin, OUTPUT);  // Sets the pump pin as output
    lcd.init();                // Initializes LCD display
    lcd.backlight();           // Turns on LCD backlight for visibility
  }

  void loop() {
    // Read sensors
    int tempValue = analogRead(tempSensorPin);
    int lightValue = analogRead(lightSensorPin);
    int moistureValue = analogRead(moisturePin);

    // Calculate soil moisture percentage
    float moisturePercent = map(moistureValue, 0, 1023, 100, 0);

    // Calculate temperature in Celsius
    float resistance = (1023.0 / tempValue - 1) * seriesResistor;
    float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    float tempC = tempK - 273.15;
    float tempF = tempC * 9.0 / 5.0 + 32.0;

    // Display Temperature
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Temp C: ");
    lcd.print(tempC);
    lcd.setCursor(0, 1);
    lcd.print("Temp F: ");
    lcd.print(tempF);
    delay(2000);

    // Display light and soil moisture
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Light: ");
    lcd.print(lightValue);
    lcd.setCursor(0, 1);
    lcd.print("Soil: ");
    lcd.print(moisturePercent);
    lcd.print("%");
    delay(2000);

    // Control pump if soil moisture is below 35%
    if (moisturePercent < 35) {
      digitalWrite(pumpPin, HIGH);  // Turn on pump
      delay(3000);
      digitalWrite(pumpPin, LOW);  // Turn off pump
      lcd.init(); // Reinitialize LCD to prevent display corruption
    }
  }

12. 最後に、コードを保存し、作業スペースを整理するのを忘れないでください。

**Question**

センサーが環境変化に対して反応が遅すぎる、または早すぎる場合、システムをどのように改善または調整できますか。

**Summary**

今回のレッスンでは、Arduinoを使用して植物モニターを構築し、プログラムすることに成功しました。このプロジェクトを通じて、さまざまなセンサーやコンポーネントに触れ、それらを統合して実用的なデバイスを作成する方法を学びました。実際に手を動かして学ぶことで、現実世界のデータを収集し、植物のケアに関する適切な意思決定を行う方法を理解しました。環境を積極的に制御することで、植物の最適な成長環境を確保するための大きな一歩を踏み出しました。

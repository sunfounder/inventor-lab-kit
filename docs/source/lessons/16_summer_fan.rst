.. note::

    こんにちは！SunFounderのRaspberry Pi & Arduino & ESP32エンスージアストコミュニティへようこそ！Facebookで仲間たちと一緒にRaspberry Pi、Arduino、ESP32をもっと深く学びましょう。

    **なぜ参加するのか？**

    - **専門家サポート**: 購入後の問題や技術的な課題を、コミュニティやチームの助けを借りて解決しましょう。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **限定プレビュー**: 新製品発表やスニークピークへの早期アクセスをゲット。
    - **特別割引**: 最新製品の特別割引をお楽しみください。
    - **フェスティブプロモーションとプレゼント企画**: プレゼント企画やホリデープロモーションに参加しましょう。

    👉 一緒に探求し、クリエイトする準備はできましたか？[|link_sf_facebook|]をクリックして、今すぐ参加しましょう！

16. サマーファン
======================

夏が近づくこの時期に、楽しくて魅力的なプロジェクトに挑戦してみましょう。このレッスンでは、Arduinoを使って簡単でありながら魅力的な夏のファンを作る方法を学びます。モーター制御の基本、モータードライバの重要性、ボタンを使ったモーターの速度と方向の制御方法について探求します。このレッスンが終わる頃には、実際のファンを模倣するプロジェクトを作成し、夏の暑さを乗り切る準備が整います！

.. raw:: html

     <video muted controls style = "max-width:90%">
        <source src="_static/video/16_summer_fan.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
  
このレッスンが終わる頃には、以下ができるようになります：

* L293Dチップの目的と機能を学ぶ。
* Arduino、モーター、モータードライバを使用して回路を構築する。
* Arduinoのコードを作成し、モーターの速度と方向を制御する。
* ボタンを使ってモーターの速度を調整し、ファンの制御をシミュレートする。

回路を構築する
------------------------------------

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * モーター
     - 4 * ボタン
     - 1 * L293Dチップ
   * - |list_uno_r3|
     - |list_motor| 
     - |list_button|
     - |list_l293d|
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - ジャンパーワイヤー
     - 1 * マルチメーター
   * - |list_usb_cable|
     - |list_breadboard|
     - |list_wire|
     - |list_meter|
   * - 1 * ブレッドボードパワーモジュール
     - 1 * 9Vバッテリー
     - 1 * バッテリーケーブル
     - 
   * - |list_power_module| 
     - |list_battery| 
     - |list_bat_cable| 
     -

**構築手順**

配線図に従うか、以下の手順に従って回路を構築します。

.. image:: img/16_motor_button_gnd.png
  :width: 500
  :align: center

**1. L293Dチップの接続**

通常、モーターの端子をバッテリーやコントロールボードのGNDや5Vピンに直接接続すると、モーターが回転します。

しかし、プログラムでモーターを制御するためには、Arduinoボードの信号ピンに接続する必要があります。これらのピンは約20mAしか出力しないため、モーターには十分ではありません。そのため、L293Dのようなモータードライバが必要です。

.. image:: img/16_motor_l293d_pic.png
  :width: 300
  :align: center

L293Dは、高電圧および高電流を処理できる4チャンネルドライバで、DCモーターやステッピングモーターなどのインダクティブ負荷を駆動するのに適しています。標準のDTL、TTLロジックレベルで動作します。

.. image:: img/16_motor_l293d_pinout.png
  :align: center

* L293Dには、Vcc1とVcc2という2つの電源ピンがあります。Vcc2はモーターに電力を供給し、Vcc1はチップ自体に電力を供給します。小型のDCモーターには、両方のピンを+5Vに接続します。
* ピン **EN** はイネーブルピンで、高レベルで動作します。 **A** は入力を、 **Y** は出力を示します。
* ピン **EN** が高レベルの場合、 **A** が高レベルならば **Y** は高レベルを出力し、 **A** が低レベルならば **Y** は低レベルを出力します。
* ピン **EN** が低レベルの場合、L293Dは動作しません。

.. list-table:: 
   :widths: 25 25 25
   :header-rows: 0

   * - EN
     - A
     - Y
   * - H
     - H
     - H  
   * - H
     - L
     - L 
   * - L
     - X
     - X 

さあ、このモータードライバチップをテストするための回路を構築しましょう。


1. モーターやサーボ、その他のアクチュエータを使用する際は、メインボードを損傷しないように外部電源を使用することをお勧めします。ブレッドボードパワーモジュールをブレッドボードに挿入し、ジャンパーワイヤーを使用して、ブレッドボードの負のレールをArduino Uno R3のGNDに接続し、共通グランドを実現します。

.. image:: img/14_dinosaur_power_module.png
    :width: 400
    :align: center

.. note::

    回路図におけるブレッドボードの正負端子の順序は、キットに含まれているブレッドボードの配置とは逆です。

    実際の配線では、ブレッドボードパワーモジュールを番号が大きい側（60〜65）から挿入し、パワーモジュールの「-」がブレッドボードの負のレール「-」に入り、「+」が正のレール「+」に入るようにします。

    .. raw:: html

        <video controls style = "max-width:90%">
            <source src="_static/video/about_power_module.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

2. L293Dチップをブレッドボードの中央の切れ目にまたがるように挿入します。チップの切り欠きが左を向いていることを確認してください。

.. image:: img/16_motor_l293d.png
  :width: 500
  :align: center

3. L293Dチップのピンを次のように接続します。

* **1(1,2EN)**: チップを有効にするために、ブレッドボードの正のレールに接続します。
* **4(GND)**: チップをグランドするために、ブレッドボードの負のレールに接続します。
* **8(VCC2)**: モーターに電力を供給するために、ブレッドボードの正のレールに接続します。
* **16(VCC1)**: チップに電力を供給するために、ブレッドボードの正のレールに接続します。

.. image:: img/16_motor_l293d_power.png
  :width: 500
  :align: center

4. 次に、チップのAピン（1A、2A、3A、4A）を5VまたはGNDに接続し、Yピン（1Y、2Y、3Y、4Y）の電圧を確認できます。1Aと1Yを使用してテストします。まず、2(1A)をブレッドボードの正のレールに接続します。

.. image:: img/16_motor_l293d_1a_5v.png
  :width: 500
  :align: center

5. マルチメーターを直流20ボルトの設定に調整します。

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center
  
6. マルチメーターの赤いリードをピン3(1Y)に、黒いリードを任意のGNDに接触させます。

.. image:: img/16_motor_l293d_1y.png
  :width: 500
  :align: center

7. 以下の表に、ピン3(1Y)での電圧を記録します。

.. list-table:: 
   :widths: 25 25 25
   :header-rows: 0

   * - 1,2EN
     - 1A
     - 1Y
   * - 5V
     - 5V
     - *≈5.04V* 
   * - 5V
     - 0V
     - 

8. 次に、2(1A)をブレッドボードの負のレールに接続します。

.. image:: img/16_motor_l293d_1a.png
  :width: 500
  :align: center

9. 同様に、マルチメーターで3(1Y)の電圧を測定し、結果を表に記入します。

.. image:: img/16_motor_l293d_1y.png
  :width: 500
  :align: center

.. list-table:: 
   :widths: 25 25 25
   :header-rows: 0

   * - 1,2EN
     - 1A
     - 1Y
   * - 5V
     - 5V
     - *≈5.04V* 
   * - 5V
     - 0V
     - *≈0V*  

上記のテスト結果から、ENが高レベルのとき、L293Dチップが動作し、Aピン（1A、2A、3A、4A）が高レベルの場合、Yピン（1Y、2Y、3Y、4Y）が高レベルを出力し、Aピンが低レベルの場合、Yピンも低レベルを出力することが確認されます。

10. 次に、L293Dチップのピン2(1A)をArduino Uno R3のピン10に、ピン7(2A)をピン9に接続し、ピン9とピン10を使用してチャネル1および2の入力を制御します。

.. image:: img/16_motor_l293d_910.png
  :width: 500
  :align: center

**2. モーターの接続**

これは3VのDCモーターです。2つの端子にそれぞれ高レベルと低レベルを与えると、回転します。

.. image:: img/16_motor_pic.png
  :width: 300
  :align: center

モーターは私たちの日常生活で重要な役割を果たしています。いたるところに存在します！暑い日に私たちを涼しくする扇風機や、おいしいケーキを作るミキサー、街中を走る電動自動車など、モーターが物を動かしてくれます！

.. image:: img/motor_application.jpg
  :width: 600
  :align: center

モーターは機械の心臓のようなものです。電気エネルギーを機械エネルギーに変換し、私たちのおもちゃや家電製品、さらには大きな車両にまで命を吹き込みます！

仕組みはこうです。モーターに電気が供給されると、磁場が発生します。この磁場がモーター内の他の磁石と相互作用し、モーターが回転します。この回転は、トップを回すように、車輪やプロペラ、その他の機械の可動部分を動かすのに使用されます。

.. image:: img/motor_rotate1.gif
  :align: center

次に、モーターの2つの端子をL293Dチップのピン3(1Y)とピン6(2Y)に接続します。

.. image:: img/16_motor_motor.png
  :width: 500
  :align: center

モーターを制御するための真理値表は以下の通りです。

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1,2EN
     - 1A
     - 2A
     - モーターの状態
   * - H
     - H
     - L 
     - モーターが回転
   * - H
     - L
     - H 
     - モーターが逆回転
   * - H
     - L
     - L 
     - モーターが停止
   * - H
     - H
     - H 
     - モーターが停止

**3. 4つのボタンの接続**

モーターの速度を制御するために4つのボタンが必要であり、それぞれのボタンは速度設定を表します。

1. ブレッドボードに4つのボタンを取り付け、それぞれが中央の溝をまたぐように配置します。

.. image:: img/16_motor_button.png
  :width: 700
  :align: center

2. 各ボタンの左下のピンをArduinoのピン4、5、6、7にそれぞれ接続します。

.. image:: img/16_motor_button_pin.png
  :width: 700
  :align: center

3. 最後に、各ボタンの右上のピンをGNDに接続します。ここではプルダウン抵抗を使用せず、Arduinoの内部プルアップを利用して配線を簡略化しています。

.. image:: img/16_motor_button_gnd.png
  :width: 700
  :align: center


コード作成 - モーターを動かす
---------------------------------------

次に、モーターを駆動するためのコードを書いてみましょう。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2. ``Ctrl + S`` を押すか、「保存」ボタンをクリックして、スケッチを ``Lesson16_Motor`` として保存します。

3. モーター制御ピンを初期化します。

.. code-block:: Arduino
  :emphasize-lines: 2,3,7,8

  // Define motor control pins
  int motor1A = 10;
  int motor2A = 9;

  void setup() {
    // Set motor control pins as outputs
    pinMode(motor1A, OUTPUT);
    pinMode(motor2A, OUTPUT);
  }

4. ``void loop()`` の中で、 ``digitalWrite()`` 関数を使って、モーターの2つの制御ピンに ``HIGH`` と ``LOW`` の状態を書き込み、モーターを回転させます。

.. code-block:: Arduino
  :emphasize-lines: 13,14

  // Define motor control pins
  int motor1A = 10;
  int motor2A = 9;

  void setup() {
    // Set motor control pins as outputs
    pinMode(motor1A, OUTPUT);
    pinMode(motor2A, OUTPUT);
  }

  void loop() {
    // Rotate the motor forward
    digitalWrite(motor1A, HIGH);
    digitalWrite(motor2A, LOW);
  }

5. ここまで完了したら、コードをArduinoにアップロードし、モーターが動作することを確認します。

6. 次に、モーターの回転方向を逆にする方法と停止する方法を見てみましょう。モーターの回転方向を逆にするには、2つの制御ピンのレベルを入れ替えるだけです。

.. code-block:: Arduino
  :emphasize-lines: 7,8

  void loop() {
    // Rotate the motor forward
    digitalWrite(motor1A, HIGH);
    digitalWrite(motor2A, LOW);

    // Rotate the motor in reverse
    digitalWrite(motor1A, LOW);
    digitalWrite(motor2A, HIGH);
    delay(2000);  // Motor runs for 1 seconds
  }

7. モーターを停止させるには、2つの制御ピンをどちらも ``HIGH`` または ``LOW`` に設定するだけで、モーターが停止します。

.. code-block:: Arduino
  :emphasize-lines: 23,24

  // Define motor control pins
  int motor1A = 10;
  int motor2A = 9;

  void setup() {
    // Set motor control pins as outputs
    pinMode(motor1A, OUTPUT);
    pinMode(motor2A, OUTPUT);
  }

  void loop() {
    // Rotate the motor forward
    digitalWrite(motor1A, HIGH);
    digitalWrite(motor2A, LOW);
    delay(2000);  // Motor runs for 1 seconds

    // Rotate the motor in reverse
    digitalWrite(motor1A, LOW);
    digitalWrite(motor2A, HIGH);
    delay(2000);  // Motor runs for 1 seconds

    // Stop the motor
    digitalWrite(motor1A, LOW);
    digitalWrite(motor2A, LOW);
    delay(3000);  // Motor stops for 2 second
  }

8. コードが完成したので、Arduinoボードにアップロードできます。これにより、モーターが2秒間前進し、次に2秒間逆回転し、3秒間停止するサイクルが繰り返されることが確認できます。

コード作成 - 夏の扇風機
-----------------------------------
次に、4つのボタンを使用してモーターの速度を制御する方法を探ってみましょう。これは、実際の扇風機の速度を調整するのに似ています。

1. 以前保存したスケッチ ``Lesson16_Motor`` を開きます。「ファイル」メニューから「名前を付けて保存...」を選択し、名前を ``Lesson16_Summer_Fan`` に変更します。「保存」をクリックします。

2. ここでは、モーターの回転速度を制御する必要があるため、 ``motorRotate()`` 関数を作成して速度を制御します。

* この関数では、 ``analogWrite()`` 関数を使用して ``motor1A`` ピンにPWM値を書き込み、 ``motor2A`` は0に設定されます。これにより、モーターは一方向に回転します。
* ``speed`` の値が大きいほど、モーターの回転速度が速くなります。

.. code-block:: Arduino
  :emphasize-lines: 12, 14-17

  // Define motor control pins
  int motor1A = 10;
  int motor2A = 9;

  void setup() {
    // Set motor control pins as outputs
    pinMode(motor1A, OUTPUT);
    pinMode(motor2A, OUTPUT);
  }

  void loop() {
    motorRotate(150);
  }

  void motorRotate(int speed) {
    analogWrite(motor1A, speed);  // Control motor speed
    analogWrite(motor2A, 0);      // Control motor speed
  }

3. コードをArduinoボードにアップロードした後、モーターが一方向に回転することが確認できます。 ``motorRotate(150)`` の値を変更すると、モーターの速度が変化し、値が大きいほど速度が速くなります。

4. 次に、4つのボタンピンを初期化します。

.. code-block:: Arduino
  :emphasize-lines: 6-9

  // Define motor control pins
  const int motor1A = 10;
  const int motor2A = 9;

  // Define button pins
  const int button1 = 4;
  const int button2 = 5;
  const int button3 = 6;
  const int button4 = 7;

5. ``void setup()`` で、4つのボタンをすべて ``INPUT_PULLUP`` に設定します。

.. code-block:: Arduino
  :emphasize-lines: 7-10

  void setup() {
    // Set motor control pins as outputs
    pinMode(motor1A, OUTPUT);
    pinMode(motor2A, OUTPUT);

    // Initialize button pins as INPUT_PULLUP
    pinMode(button1, INPUT_PULLUP);
    pinMode(button2, INPUT_PULLUP);
    pinMode(button3, INPUT_PULLUP);
    pinMode(button4, INPUT_PULLUP);
  }
  
6. 次に、メインプログラム部分を書いてみましょう。 ``button1`` が ``LOW`` と読み取られると、それは ``button1`` が押されたことを意味し、この時点でモーターの速度を0に設定し、つまりモーターを停止させます。

.. code-block:: Arduino
  :emphasize-lines: 2-4

  void loop() {
    if (digitalRead(button1) == LOW) {         // Check if first button is pressed
      motorRotate(0);                          // Turn off the motor
    }
  }

7. 同様に、 ``button2`` が押された場合、モーターの速度を150に設定します。

.. code-block:: Arduino
  :emphasize-lines: 4-6

  void loop() {
    if (digitalRead(button1) == LOW) {         // Check if first button is pressed
      motorRotate(0);                          // Turn off the motor
    } else if (digitalRead(button2) == LOW) {  // Check if second button is pressed
      motorRotate(150);                        // Set speed for low
    }
  }

8. ``button3`` が押された場合、モーターの速度を200に設定します。

.. code-block:: Arduino
  :emphasize-lines: 6-8

  void loop() {
    if (digitalRead(button1) == LOW) {         // Check if first button is pressed
      motorRotate(0);                          // Turn off the motor
    } else if (digitalRead(button2) == LOW) {  // Check if second button is pressed
      motorRotate(150);                        // Set speed for low
    } else if (digitalRead(button3) == LOW) {  // Check if third button is pressed
      motorRotate(200);                        // Set speed for medium
    } 
  }

9. 最後に、 ``button4`` が押された場合、モーターの速度を250に設定します。

.. code-block:: Arduino
  :emphasize-lines: 8-10

  void loop() {
    if (digitalRead(button1) == LOW) {         // Check if first button is pressed
      motorRotate(0);                          // Turn off the motor
    } else if (digitalRead(button2) == LOW) {  // Check if second button is pressed
      motorRotate(150);                        // Set speed for low
    } else if (digitalRead(button3) == LOW) {  // Check if third button is pressed
      motorRotate(200);                        // Set speed for medium
    } else if (digitalRead(button4) == LOW) {  // Check if fourth button is pressed
      motorRotate(250);                        // Set speed for high
    }
  }

10. これで、プログラムが完成しました。コードをArduinoボードにアップロードし、4つのボタンをそれぞれ押してモーターの速度が変わるか確認してみてください。

.. code-block:: Arduino

  // Define motor control pins
  const int motor1A = 10;
  const int motor2A = 9;

  // Define button pins
  const int button1 = 4;
  const int button2 = 5;
  const int button3 = 6;
  const int button4 = 7;

  void setup() {
    // Set motor control pins as outputs
    pinMode(motor1A, OUTPUT);
    pinMode(motor2A, OUTPUT);

    // Initialize button pins as INPUT_PULLUP
    pinMode(button1, INPUT_PULLUP);
    pinMode(button2, INPUT_PULLUP);
    pinMode(button3, INPUT_PULLUP);
    pinMode(button4, INPUT_PULLUP);
  }

  void loop() {
    if (digitalRead(button1) == LOW) {         // Check if first button is pressed
      motorRotate(0);                          // Turn off the motor
    } else if (digitalRead(button2) == LOW) {  // Check if second button is pressed
      motorRotate(150);                        // Set speed for low
    } else if (digitalRead(button3) == LOW) {  // Check if third button is pressed
      motorRotate(200);                        // Set speed for medium
    } else if (digitalRead(button4) == LOW) {  // Check if fourth button is pressed
      motorRotate(250);                        // Set speed for high
    }
  }

  void motorRotate(int speed) {
    analogWrite(motor1A, speed);  // Control motor speed
    analogWrite(motor2A, 0);      // Control motor speed
  }


11. 最後に、コードを保存し、作業スペースを片付けることを忘れないでください。

**質問**

モーターの回転方向も制御したい場合、コードをどのように修正する必要がありますか？

**まとめ**

このレッスンでは、L293Dモータードライバーチップの動作原理と、モーターの基本操作について学びました。Arduinoを使用してモーターを回転させ、その方向を制御する方法を学びました。最後に、4つのボタンを使用して異なるモーター速度を制御する、扇風機をシミュレートした完全なプロジェクトをまとめました。

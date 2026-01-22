.. note::

    こんにちは！SunFounder Raspberry Pi & Arduino & ESP32 愛好者コミュニティのFacebookページへようこそ！ここでは、Raspberry Pi、Arduino、ESP32の世界をさらに深く探求し、他の愛好者と一緒に楽しむことができます。

    **参加する理由**

    - **エキスパートサポート**: アフターセールスの問題や技術的な課題を、コミュニティやチームの助けを借りて解決できます。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換できます。
    - **限定プレビュー**: 新製品の発表や先行プレビューに早期アクセスできます。
    - **特別割引**: 最新の製品に対する特別割引を楽しむことができます。
    - **フェスティブプロモーションとギブアウェイ**: ギブアウェイやホリデープロモーションに参加できます。

    👉 一緒に探求し、創造する準備はできましたか？今すぐ[|link_sf_facebook|]をクリックして参加しましょう！

31. 数字当てゲーム
==========================
今日のレッスンへようこそ！このインタラクティブなレッスンでは、IRリモコンとLCDディスプレイを使って、隠された数字を当てるゲームを作成し、楽しく学びましょう。

「数字当てゲーム」は、友達と一緒に楽しむパーティーゲームです。0～99の数字を交互に入力し、プレイヤーが正解を当てるまで範囲が狭まります。正解したプレイヤーは罰ゲームを受けます。例えば、ラッキーナンバーが51で、プレイヤー1が50を入力すると、次の範囲は50～99に狭まり、プレイヤー2が70を入力すると範囲が50～70になります。そして、プレイヤー3が51を入力すると、そのプレイヤーが罰ゲームとなります。ここでは、IRリモコンで数字を入力し、LCDに結果を表示します。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/31_guess_number.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンで学べること：

* ゲームの秘密のターゲットとして使うランダムな数字の生成方法を学びます。
* 赤外線リモコンを使用してユーザー入力を行い、数字を推測します。
* 推測が高すぎるか低すぎるか、または正しいかをLCDで即座にフィードバックします。
* ゲームロジックとフローを管理するために条件文とループ構造を利用します。


回路の構築
--------------------------------
**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * I2C LCD1602
     - 1 * IR受信機
     - 1 * リモコン
   * - |list_uno_r3| 
     - |list_i2c_lcd1602| 
     - |list_receiver| 
     - |list_remote| 
   * - 1 * USBケーブル
     - 1 * ブレッドボード
     - ジャンパーワイヤー
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - 

**ステップごとの構築手順**

配線図に従って回路を構築するか、以下の手順に従ってください。

.. image:: img/31_guess_circuit.png
    :width: 700
    :align: center

1. 赤外線受信機をブレッドボードに差し込みます。赤外線受信機には表と裏があり、突起がある方が前面です。左から右へのピン順は、OUT、GND、VCCです。

.. image:: img/31_guess_receiver.png
    :width: 500
    :align: center

2. 赤外線受信機のOUTピンをArduino Uno R3のピン2に接続し、GNDをブレッドボードの負極に、VCCをブレッドボードの正極に接続します。

.. image:: img/31_guess_receiver_pins.png
    :width: 500
    :align: center

3. I2C LCD1602モジュールを接続します：GNDをブレッドボードの負極に、VCCをブレッドボードの正極に、SDAをピンA4に、SCLをピンA5に接続します。

.. image:: img/31_guess_i2c_lcd1602.png
    :width: 700
    :align: center

4. 最後に、Arduino Uno R3のGNDと5Vピンをそれぞれブレッドボードの負極と正極に接続します。

.. image:: img/31_guess_circuit.png
    :width: 700
    :align: center

コードの作成
------------------
数字当てゲームを実装するには、以下の点を慎重に検討する必要があります：

* **ランダムな数字**: ランダムなターゲット数字を生成する方法を実装します。
* **ユーザー入力**: プレイヤーがどのようにして数字を入力するかを決定します（例：キーパッド、IRリモコン）。
* **フィードバック**: プレイヤーに推測が高すぎるか低すぎるか、または正しいかをどのように伝えるかを決定します。
* **ゲームの制限**: 推測の範囲を設定し、ゲームの構造を決定し、難易度を調整します。

それでは、数字当てゲームを実装するコードを書き始めましょう。

.. note::

  IR受信機とI2C LCD1602に不慣れな場合は、以下のプロジェクトを通じてその基本的な使用方法を学んでください：

  * :ref:`ar_ir_receiver`
  * :ref:`ar_i2c_lcd1602`

  ここでは ``LiquidCrystal I2C`` および ``IRremote`` ライブラリを使用します。これらのライブラリは、 **Library Manager** からインストールできます。

1. 以前に保存したスケッチ ``Lesson22_Decode_Key_Value`` を開きます。 ``File`` メニューから「名前を付けて保存」をクリックし、ファイル名を ``Lesson31_Guess_Number`` に変更して「保存」をクリックします。

.. code-block:: Arduino

  #include <IRremote.h>  // Include the IRremote library

  const int receiverPin = 2;  // Define the pin number for the IR Sensor

  void setup() {
    // Start serial communication at a baud rate of 9600
    Serial.begin(9600);
    // Initialize the IR receiver on the specified pin with LED feedback enabled
    IrReceiver.begin(receiverPin, ENABLE_LED_FEEDBACK);
  }

  void loop() {
    if (IrReceiver.decode()) {  // Check if the IR receiver has received a signal
      bool result = 0;
      String key = decodeKeyValue(IrReceiver.decodedIRData.command);
      if (key != "ERROR") {
        Serial.println(key);  // Print the readable command
        delay(100);
      }
    IrReceiver.resume();  // Enable receiving of the next value
    }
  }

  // Function to map received IR signals to corresponding keys
  String decodeKeyValue(long result) {
    switch (result) {
      case 0x45: return "POWER";
      case 0x47: return "MUTE";
      case 0x46: return "MODE";
      case 0x44: return "PLAY/PAUSE";
      case 0x40: return "BACKWARD";
      case 0x43: return "FORWARD";
      case 0x7: return "EQ";
      case 0x15: return "-";
      case 0x9: return "+";
      case 0x19: return "CYCLE";
      case 0xD: return "U/SD";
      case 0x16: return "0";
      case 0xC: return "1";
      case 0x18: return "2";
      case 0x5E: return "3";
      case 0x8: return "4";
      case 0x1C: return "5";
      case 0x5A: return "6";
      case 0x42: return "7";
      case 0x52: return "8";
      case 0x4A: return "9";
      case 0x0: return "ERROR";
      default: return "ERROR";
    }
  }

2. 必要なライブラリをインクルードし、LCDを正しいI2Cアドレスとサイズで初期化します。

.. code-block:: Arduino
  :emphasize-lines: 2,3,5

  #include <IRremote.h>           // Include the IR remote control library
  #include <Wire.h>               // Include the Wire library for I2C communication
  #include <LiquidCrystal_I2C.h>  // Include the LCD library for I2C

  LiquidCrystal_I2C lcd(0x27, 16, 2);  // Set up the LCD (address 0x27, 16 columns, 2 rows)

  const int receiverPin = 2;  // IR sensor pin

3. 次に、入力された数字、ランダムに生成されたターゲットナンバー、推測範囲の上限（99）、および下限（0）を格納するための4つの変数を作成します。

.. code-block:: Arduino
  :emphasize-lines: 9-12

  #include <IRremote.h>           // Include the IR remote control library
  #include <Wire.h>               // Include the Wire library for I2C communication
  #include <LiquidCrystal_I2C.h>  // Include the LCD library for I2C

  LiquidCrystal_I2C lcd(0x27, 16, 2);  // Set up the LCD (address 0x27, 16 columns, 2 rows)

  const int receiverPin = 2;  // IR sensor pin

  int guessedNumber = 0;  // Number input by the user
  int targetNumber = 0;   // Randomly generated target number
  int upper = 99;         // Upper bound of guessing range
  int lower = 0;          // Lower bound of guessing range

4. ``setup()`` 関数内で、LCDを初期化し、新しいターゲットナンバーを生成するコードを追加します。

.. code-block:: Arduino
  :emphasize-lines: 4-6

  void setup() {
    Serial.begin(9600);                                  // Initialize serial communication at 9600 bps
    IrReceiver.begin(receiverPin, ENABLE_LED_FEEDBACK);  // Initialize IR receiver with LED feedback
    lcd.init();                                          // Initialize the LCD
    lcd.backlight();                                     // Turn on the backlight
    NewTargetNumber();                                   // Initialize game values
  }

5. ``loop()`` 関数内で、最初にboolean型変数 ``result`` を作成し、「パワー」キーが押されたかどうかを確認します。押された場合は、新しいターゲットナンバーを生成するために ``NewTargetNumber()`` を呼び出します。

.. code-block:: Arduino
  :emphasize-lines: 9, 12-14

  void loop() {
    if (IrReceiver.decode()) {           // Check if an IR message has been received
      String key = decodeKeyValue(IrReceiver.decodedIRData.command);
      if (key != "ERROR") {
        Serial.println(key);  // Print the readable command
        delay(100);
      }

      bool result = false;

      // Check the key received and act accordingly
      if (key == "POWER") {
        NewTargetNumber();  // Reset game values
      }
    IrReceiver.resume();  // Enable receiving of the next value
    }
  }

6. 0から9までの数字を押した場合、入力された数字を変数 ``guessedNumber`` に格納します。

* 蓄積された数字が10以上の場合、 ``checkGuess()`` 関数を呼び出して、推測した数字がターゲットナンバーと一致するかどうかを確認します。結果（trueまたはfalse）は ``result`` 変数に格納されます。
* 1桁の数字が入力された場合、 ``displayResult()`` 関数を直接呼び出して、LCDに表示します。
* ``guessedNumber = guessedNumber * 10 + key.toInt();``: この行は、ユーザーが入力した桁を蓄積して完全な数字を形成するために使用されます。たとえば、ユーザーが '3' を押し、その後 '5' を押すと、guessedNumber は最初は3で、次に35になります。 ``key.toInt()`` は数字の文字列表現を整数に変換します。

.. code-block:: Arduino
  :emphasize-lines: 4-11

  // Check the key received and act accordingly
  if (key == "POWER") {
    NewTargetNumber();  // Reset game values
  } else if (key >= "0" && key <= "9") {
    guessedNumber = guessedNumber * 10;
    guessedNumber += key.toInt();  // Accumulate digits typed
    if (guessedNumber >= 10) {
      result = checkGuess();  // Check if guessed number is correct
    }
    displayResult(result);  // Display input and result on LCD
  }

7. 「CYCLE」キーが押された場合、 ``checkGuess()`` 関数を呼び出して、入力された推測ナンバーが正しいかどうかを確認します。正しければ ``true`` を返し、正しくなければ ``false`` を返し、その結果を ``result`` 変数に格納します。その後、 ``displayResult()`` 関数を呼び出して、LCDに情報を表示します。

.. note::

  前述の ``else if`` 文では、10以上の数字のみがターゲットナンバーと比較されます。10未満の数字はLCDに表示されるだけです。

  そのため、ここで「CYCLE」キーを追加しました。1桁の数字を入力する場合、数字を入力した後に「CYCLE」キーを押してターゲットナンバーと比較できます。

.. code-block:: Arduino
  :emphasize-lines: 8-11

      } else if (key >= "0" && key <= "9") {
        guessedNumber = guessedNumber * 10;
        guessedNumber += key.toInt();  // Accumulate digits typed
        if (guessedNumber >= 10) {
          result = checkGuess();  // Check if guessed number is correct
        }
        displayResult(result);  // Display input and result on LCD
      } else if (key == "CYCLE") {
        result = checkGuess();  // Check if guessed number is correct
        displayResult(result);  // Display result on LCD
      }
      IrReceiver.resume();  // Enable receiving of the next value
    }
  }

8. ``NewTargetNumber()`` 関数は、ユーザーが推測するための新しいターゲットナンバーを生成することで、ゲームを初期化します。

* 推測範囲の ``upper`` および ``lower`` の限界を初期値に設定し、LCD画面をクリアしてウェルカムメッセージと指示を表示します。
* また、推測された数字をリセットし、デバッグ目的でターゲットナンバーをシリアルモニターに出力します。

.. code-block:: Arduino

  void NewTargetNumber() {
    randomSeed(analogRead(A0));    // Seed the random number generator
    targetNumber = random(99);     // Generate a new target number
    upper = 99;                    // Reset upper limit
    lower = 0;                     // Reset lower limit
    lcd.clear();                   // Clear the LCD
    lcd.print("    Welcome!");     // Welcome message
    lcd.setCursor(0, 1);           // Move cursor to the second line
    lcd.print("  Guess Number!");  // Instruction message
    guessedNumber = 0;             // Reset guessed number
    Serial.print("point is ");
    Serial.println(targetNumber);  // Print the target number in serial monitor for debugging
  }

9. ``checkGuess()`` 関数は、ユーザーが推測した数字をターゲットナンバーと比較します。

* 推測がターゲットナンバーより高い場合、上限を更新します。 
* 推測が低い場合、下限を更新します。 
* 推測が正しい場合、推測された数字をリセットし、 ``true`` を返します。 
* それ以外の場合、推測された数字をリセットし、 ``false`` を返します。

.. code-block:: Arduino

  bool checkGuess() {
    if (guessedNumber > targetNumber) {
      if (guessedNumber < upper) upper = guessedNumber;  // Update upper limit
    } else if (guessedNumber < targetNumber) {
      if (guessedNumber > lower) lower = guessedNumber;  // Update lower limit
    } else if (guessedNumber == targetNumber) {
      guessedNumber = 0;
      return true;  // Correct guess
    }
    guessedNumber = 0;
    return false;  // Incorrect guess
  }

10. ``displayResult()`` 関数は、ユーザーの推測が正しいかどうかに基づいてLCDディスプレイを更新します。

* 推測が正しい場合、成功メッセージを表示し、5秒間一時停止してから新しいターゲットナンバーを生成し、ゲームをリセットします。 
* 推測が不正解の場合、現在の推測ナンバーと更新された推測範囲を表示します。

.. code-block:: Arduino

  void displayResult(bool result) {
    lcd.clear();  // Clear the LCD
    if (result) {
      lcd.setCursor(0, 1);
      lcd.print(" You've got it! ");  // Display success message
      delay(5000);                    // Pause before resetting
      NewTargetNumber();              // Reset game values
    } else {
      lcd.print("Enter number:");
      lcd.print(guessedNumber);  // Display the current guess
      lcd.setCursor(0, 1);
      lcd.print(lower);
      lcd.print(" < Point < ");
      lcd.print(upper);  // Display the current range
    }
  }

11. 完全なコードは以下の通りです。これをArduinoボードにアップロードできます。

.. code-block:: Arduino

  #include <IRremote.h>           // Include the IR remote control library
  #include <Wire.h>               // Include the Wire library for I2C communication
  #include <LiquidCrystal_I2C.h>  // Include the LCD library for I2C

  LiquidCrystal_I2C lcd(0x27, 16, 2);  // Set up the LCD (address 0x27, 16 columns, 2 rows)

  const int receiverPin = 2;  // IR sensor pin

  int guessedNumber = 0;  // Number input by the user
  int targetNumber = 0;   // Randomly generated target number
  int upper = 99;         // Upper bound of guessing range
  int lower = 0;          // Lower bound of guessing range

  void setup() {
    Serial.begin(9600);                                  // Initialize serial communication at 9600 bps
    IrReceiver.begin(receiverPin, ENABLE_LED_FEEDBACK);  // Initialize IR receiver with LED feedback
    lcd.init();                                          // Initialize the LCD
    lcd.backlight();                                     // Turn on the backlight
    NewTargetNumber();                                   // Initialize game values
  }

  void loop() {
    if (IrReceiver.decode()) {  // Check if the IR receiver has received a signal
      String key = decodeKeyValue(IrReceiver.decodedIRData.command);
      if (key != "ERROR") {
        Serial.println(key);  // Print the readable command
        delay(100);
      }

      bool result = false;

      // Check the key received and act accordingly
      if (key == "POWER") {
        NewTargetNumber();  // Reset game values
      } else if (key >= "0" && key <= "9") {
        guessedNumber = guessedNumber * 10;
        guessedNumber += key.toInt();  // Accumulate digits typed
        if (guessedNumber >= 10) {
          result = checkGuess();  // Check if guessed number is correct
        }
        displayResult(result);  // Display input and result on LCD
      } else if (key == "CYCLE") {
        result = checkGuess();  // Check if guessed number is correct
        displayResult(result);  // Display result on LCD
      }
      IrReceiver.resume();  // Enable receiving of the next value
    }
  }

  void NewTargetNumber() {
    randomSeed(analogRead(A0));    // Seed the random number generator
    targetNumber = random(99);     // Generate a new target number
    upper = 99;                    // Reset upper limit
    lower = 0;                     // Reset lower limit
    lcd.clear();                   // Clear the LCD
    lcd.print("    Welcome!");     // Welcome message
    lcd.setCursor(0, 1);           // Move cursor to the second line
    lcd.print("  Guess Number!");  // Instruction message
    guessedNumber = 0;             // Reset guessed number
    Serial.print("point is ");
    Serial.println(targetNumber);  // Print the target number in serial monitor for debugging
  }

  bool checkGuess() {
    if (guessedNumber > targetNumber) {
      if (guessedNumber < upper) upper = guessedNumber;  // Update upper limit
    } else if (guessedNumber < targetNumber) {
      if (guessedNumber > lower) lower = guessedNumber;  // Update lower limit
    } else if (guessedNumber == targetNumber) {
      guessedNumber = 0;
      return true;  // Correct guess
    }
    guessedNumber = 0;
    return false;  // Incorrect guess
  }

  void displayResult(bool result) {
    lcd.clear();  // Clear the LCD
    if (result) {
      lcd.setCursor(0, 1);
      lcd.print(" You've got it! ");  // Display success message
      delay(5000);                    // Pause before resetting
      NewTargetNumber();              // Reset game values
    } else {
      lcd.print("Enter number:");
      lcd.print(guessedNumber);  // Display the current guess
      lcd.setCursor(0, 1);
      lcd.print(lower);
      lcd.print(" < Point < ");
      lcd.print(upper);  // Display the current range
    }
  }

  // Function to map received IR signals to corresponding keys
  String decodeKeyValue(long result) {
    switch (result) {
      case 0x45: return "POWER";
      case 0x47: return "MUTE";
      case 0x46: return "MODE";
      case 0x44: return "PLAY/PAUSE";
      case 0x40: return "BACKWARD";
      case 0x43: return "FORWARD";
      case 0x7: return "EQ";
      case 0x15: return "-";
      case 0x9: return "+";
      case 0x19: return "CYCLE";
      case 0xD: return "U/SD";
      case 0x16: return "0";
      case 0xC: return "1";
      case 0x18: return "2";
      case 0x5E: return "3";
      case 0x8: return "4";
      case 0x1C: return "5";
      case 0x5A: return "6";
      case 0x42: return "7";
      case 0x52: return "8";
      case 0x4A: return "9";
      case 0x0: return "ERROR";
      default: return "ERROR";
    }
  }

12. これで、任意の数字キーを押し、表示された数字範囲に従って数字を入力できます。

* 2桁の数字を入力した場合、2桁目を入力後、直接ターゲットナンバーと比較します。
* 1桁の数字を入力した場合、「CYCLE」キーを再度押してターゲットナンバーと比較を開始する必要があります。
* 推測がターゲットナンバーより高い場合、上限が更新されます。
* 推測が低い場合、下限が更新されます。
* 推測が正しい場合、LCDに成功メッセージが表示され、5秒間一時停止した後、新しいターゲットナンバーが生成され、ゲームがリセットされます。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/31_guess_number.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

13. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**Question**

ゲームの楽しさを高めるために追加できるコンポーネントは何ですか？ それらはゲームでどのような役割を果たしますか？

**Summary**

本日のレッスンでは、Arduinoボードを使用してナンバー推測ゲームを構築し、IR受信機やLCDなどのコンポーネントを統合して、ダイナミックなインタラクションを実現しました。ランダムナンバーの生成、入力処理、条件分岐といったさまざまなプログラミングの概念を探求しました。

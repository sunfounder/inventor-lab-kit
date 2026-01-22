.. note::

    こんにちは、SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Communityへようこそ！Facebookでラズベリーパイ、Arduino、ESP32に興味を持つ仲間たちと一緒に、より深く探求しましょう。

    **参加する理由**

    - **専門的なサポート**: コミュニティとチームの助けを借りて、購入後の問題や技術的な課題を解決できます。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **限定プレビュー**: 新製品の発表やスニークピークにいち早くアクセスできます。
    - **特別割引**: 最新製品に対する限定割引をお楽しみください。
    - **フェスティブプロモーションとプレゼント**: プレゼントやホリデープロモーションに参加しましょう。

    👉 私たちと一緒に探索し、創造する準備ができましたか？ [|link_sf_facebook|] をクリックして、今すぐ参加しましょう！

.. _onoff_desk_lamp:

18. ON/OFF デスクランプ
====================================

Arduino Uno R3を使用してリレー制御のデスクランプを作成する方法を学ぶハンズオンチュートリアルへようこそ。このプロジェクトでは、低電圧制御システムを通じて高電力デバイスを制御するリレーの実際の応用をシミュレートします。

.. .. image:: img/10_desk_lamp_button.jpg
..     :width: 500
..     :align: center

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/18_on_off_lamp.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

安全のために、高電力のランプをリレーの負荷端に直接接続するのではなく、LEDを使用して、ボタンを押してランプをオン/オフする操作をシミュレートします。

このレッスンの終わりまでに、以下のことができるようになります：

* Arduinoを使用してリレーモジュールを理解し、操作する。
* 高電流負荷を安全に制御するための対策を実装する。
* 効率的なボタン管理のための ``INPUT_PULLUP`` モードを使用する。
* 状態の変化を検知して出力を応答的に制御する。

リレーモジュールの理解
-------------------------------------------

リレーモジュールを見つけましょう。

リレーは、比較的小さい電流でより大きな電流を制御するために設計された電気的に操作されるスイッチです。この能力により、Arduinoボード（通常3.3Vから5Vで動作）などの低電圧制御システムと高電圧デバイスを接続するための理想的なインターフェースとなります。ほとんどの家庭やオフィス環境では、標準電圧が110Vから240Vの範囲であるため、リレーモジュールはこれらの高電圧を安全に制御するための実用的な解決策を提供します。

.. image:: img/10_relay_module.png
    :width: 300
    :align: center

リレーの構造には、通常、電磁石、アーマチュア、バネ、および接点が含まれています。電磁石は、鉄芯に巻かれたコイルによって作られます。コイルが無通電になると、電磁石は磁力を失い、アーマチュアが解放され、通常閉（NC）と共通（COM）の接点間の接続が維持されます。

.. image:: img/10_relay_nc.jpg
    :width: 500
    :align: center

* **NC**: 通常閉。無通電時にデフォルトでCOMピンに接続されています。
* **COM**: 共通ピン
* **NO**: 通常開。無通電時にデフォルトでCOMピンから切断されています。
* **コイルピン**: コイルの両端にある端子で、方向性はありません。

コイルに通電すると、電磁石が磁場を発生させ、アーマチュアを引き寄せ、COMとNOの間にある金属接点が接触します。コイルの通電が切れると、バネの張力がCOMとNCの接点を再び引き戻します。

.. image:: img/10_relay_no.jpg
    :width: 500
    :align: center

リレーモジュールは、リレー、トランジスタ、LED、抵抗、および3つのネジ端子がPCB上に取り付けられています。以下は、モジュールのピンについての簡単な説明です：

.. image:: img/10_relay_pinout.jpg
    :width: 500
    :align: center

* **-**: GND
* **+**: VCC
* **S**: このリレーを制御するために使用される信号ピン。入力が高でリレーが閉じ、入力が低でリレーが開きます。
* **COM**: 共通ピン
* **NC**: 通常閉
* **NO**: 通常開

モジュールの回路図は次のとおりです：

**S** ピンに高信号が入力されると、それがインジケータライトと電流制限抵抗を通過し、NPNトランジスタがオンになります。この電流がリレーのコイルに電流を流し、磁場を発生させ、アーマチュアを引き寄せ、「カチッ」という音を伴い、COMとNO端子が接触して回路が完成します。

.. image:: img/10_relay_circuit.png
    :width: 600
    :align: center


回路の組み立て
------------------------------------
次に、LEDを駆動し、リレーモジュールの動作原理を探るための回路を構築しましょう。

**必要なコンポーネント**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 赤色LED
     - 1 * 220Ω抵抗
     - 1 * リレーモジュール
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm|  
     - |list_relay_module| 
   * - 1 * ボタン
     - 1 * USBケーブル
     - 1 * ブレッドボード
     - ジャンパーワイヤー
   * - |list_button| 
     - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire|


**組み立て手順**

通常、リレーを使用して家庭のランプをプログラムで制御できるように改造できます。

    .. warning::

        220Vの電圧を扱うため、事前の電気知識がない場合は、この改造を試みないでください。非常に危険です。

.. image:: img/10_relay_lamp.jpg
    :width: 600
    :align: center

安全のため、このコースでは高電力負荷をシミュレートするためにLEDを使用します。配線図または以下の手順に従って回路を構築してください。

.. image:: img/10_relay_led.png
    :width: 500
    :align: center

1. ブレッドボードで、Arduino Uno R3の5Vをブレッドボードの正極レールに、GNDを負極レールに接続します。

.. image:: img/10_relay_led_power.png
    :width: 600
    :align: center

2. リレーモジュールのSピンをArduino Uno R3のピン2に接続します。 ``+`` ピンと ``-`` ピンはそれぞれブレッドボードの正極レールと負極レールに接続します。

.. image:: img/10_relay_led_relay_module.png
    :width: 600
    :align: center

3. 通常、リレーモジュールのCOM端子は外部電源に接続しますが、このレッスンでは、単にそれをブレッドボードの正極レールに差し込み、LEDを点灯させます。

.. image:: img/10_relay_led_relay_com.png
    :width: 600
    :align: center

4. 赤色LEDをブレッドボードに挿入し、アノードを41Eに、カソードを40Eに配置します。

.. image:: img/10_relay_led_led.png
    :width: 600
    :align: center

5. 次に、LEDのカソードをGNDに接続します。

.. image:: img/10_relay_led_gnd.png
    :width: 600
    :align: center

6. LEDのアノード用の電流制限抵抗として、41Cと45Cの穴の間に220Ωの抵抗を挿入します。

.. image:: img/10_relay_led_resistor.png
    :width: 600
    :align: center

7. 45Aの穴をジャンパーワイヤーでリレーモジュールのNO端子に接続します。

.. image:: img/10_relay_led.png
    :width: 600
    :align: center

8. ブレッドボードの13E、13F、15E、15Fの穴にボタンを挿入します。

.. image:: img/10_relay_led_button_wire.png
    :width: 600
    :align: center

9. 最後に、13Aから負極レールへ、15Aからピン7へジャンパーワイヤーを接続します。

.. image:: img/10_relay_led_button.png
    :width: 600
    :align: center


**リレーモジュールのテスト**

次に、リレーモジュールの動作原理を確認するために、COM、NO、NCの間の導通をマルチメータで測定します。

1. マルチメータを **Continuity** モードに設定します。ダイオードのシンボルと音のアイコンが表示される設定を使用して導通を測定します。

.. image:: img/multimeter_diode.png
    :width: 300
    :align: center

2. マルチメータのテストリードをリレーモジュールのCOM端子とNC端子に接触させると、マルチメータから「ビープ」音が聞こえ、これらの端子が接続されていることを示します。

.. image:: img/10_relay_led_com_nc.png
    :width: 600
    :align: center

3. 以下の表に測定結果を記録します。

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - 状態
     - NOまたはNCがCOM端子に接続されていますか？
   * - デフォルト
     - *NC*
   * - SピンがHigh
     - 

4. リレーモジュールのSピンをブレッドボードの正極レールに接続します。「カチッ」という音が聞こえ、リレーモジュールの信号インジケータと負荷LEDが点灯します。

.. image:: img/10_relay_led_s_5v.png
    :width: 600
    :align: center

5. 再び、マルチメータのテストリードをリレーモジュールのCOM端子とNO端子に接触させると、マルチメータから「ビープ」音が聞こえ、これらの端子が接続されていることを示します。

.. image:: img/10_relay_led_com_no.png
    :width: 600
    :align: center

6. 以下の表に測定結果を記録します。

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - 状態
     - NOまたはNCがCOM端子に接続されていますか？
   * - デフォルト
     - *NC*
   * - SピンがHigh
     - *NO*

これらのテストにより、リレーモジュールが高信号で作動することが確認されました。Sピンが高信号を受け取ると、COMとNO端子が接続され、回路が高電力負荷を効果的に制御できるようになります。

コード作成
---------------------------------

次に、ボタンを押してリレーモジュールの状態を切り替えるコードを書いてみましょう。これにより、ボタンを押すとリレーが閉じてLEDが点灯し、再度押すとリレーが開いてLEDが消灯する様子が繰り返されることになります。

1. Arduino IDEを開き、「ファイル」メニューから「新しいスケッチ」を選択して新しいプロジェクトを開始します。
2. スケッチを ``Lesson18_Desk_Lamp_Relay`` として保存します（ ``Ctrl + S`` または「保存」をクリックして行います）。

3. ボタンとリレーモジュールに接続されたピンを初期化します。Lesson 8では、GNDとボタンの間に手動で接続された10Kプルダウン抵抗を使用しましたが、この回路では抵抗を接続していません。その代わりに、Arduinoのソフトウェアプルアップ機能を使用します。ボタンに接続されたピンを入力として設定し、さらに ``PULLUP`` として設定する必要があります。

.. code-block:: Arduino
    :emphasize-lines: 6

    int potValue = 0;

    void setup() {
        // put your setup code here, to run once:
        pinMode(2, OUTPUT);        // Set pin 2 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
    }

4. ``void loop()`` に入る前に、ボタンとリレーモジュールの状態を初期化するために2つの変数を作成する必要があります。リレーの初期状態はLOWです。ボタンは内部プルアップ抵抗を使用しているため、押されていないときはHIGHと読み取られます。

.. code-block:: Arduino
    :emphasize-lines: 1,2

    int relayState = LOW;          // Initial state of the LED
    int lastButtonState = HIGH;  // the previous reading from the input pin

    void setup() {
        pinMode(2, OUTPUT);        // Set pin 2 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
    }

5. 次に、 ``void loop()`` 内で、まず ``digitalRead()`` を使用してボタンの状態を読み取り、その結果を ``buttonState`` 変数に格納します。

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
    }

6. まずはボタンの押下を監視するコア機能から始めましょう。

以前のレッスンで、ボタンが押されたかどうかを ``HIGH`` または ``LOW`` の状態で判断する方法を学びました。しかし、このレッスンでは、ボタンを押し続ける必要なく、単一の押下に応答することを目指します。そのためには、ボタンの状態変化を検出する必要があります。

これを実現するために、 ``if`` 文を使用して、ボタンの前回の状態（ ``lastButtonState`` ）と現在の状態（ ``buttonState`` ）を比較します。ここでは論理演算子 ``&&`` を使用し、両方の条件が真である場合に ``if`` 文内のコードが実行されます。

.. code-block:: Arduino
    :emphasize-lines: 4

    void loop() {
        int buttonState = digitalRead(7);  // ボタンの状態を読み取ります
        // ボタンの状態が前回のループの時と変わったかを確認します
        if (lastButtonState == HIGH && buttonState == LOW) {  // ボタンの押下を検出
        }
    }

7. ボタンが押されたと検出された場合、リレーの状態を切り替えます。つまり、リレーモジュールがオフだった場合はオンになり、オンだった場合はオフになります。 ``!`` 演算子を使用して ``relayState`` 変数の状態を反転させます。

.. code-block:: Arduino
    :emphasize-lines: 5

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            relayState = !relayState;                               // Toggle relay module state
        }
    }

8. 次に ``digitalWrite()`` 関数を使用して ``relayState`` をピン2に書き込みます。

.. code-block:: Arduino
    :emphasize-lines: 6

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            relayState = !relayState;                               // Toggle relay module state
            digitalWrite(2, relayState);                        // Set the relay module state
        }
    }

9. ボタンの状態を確認し、それに応じてリレーを更新した後、ボタンの現在の状態を新しい「最後に確認した状態」として記録する必要があります。このステップは、次の状態変化を検出するために重要です。

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            relayState = !relayState;                           // Toggle relay module state
            digitalWrite(2, relayState);                        // Set the relay module state
        }
        lastButtonState = buttonState;  // Update lastButtonState to the current state
        delay(200);                     // Optional: Simple software debouncing
    }

10. 完成したコードは以下のとおりです。 **Upload** ボタンをクリックして、コードをArduino Uno R3にアップロードできます。

コードが正常にアップロードされた後、ボタンを押すとリレーが「カチッ」という音とともに閉じ、リレーモジュールのインジケータライトと外部LEDが点灯します。再度ボタンを押すと、同じ「カチッ」という音が聞こえ、インジケータライトとLEDが消灯します。このサイクルが繰り返されます。

.. code-block:: Arduino

    int relayState = LOW;        // Initial state of the relay module
    int lastButtonState = HIGH;  // the previous reading from the input pin

    void setup() {
        pinMode(2, OUTPUT);        // Set pin 2 as output
        pinMode(7, INPUT_PULLUP);  // Set pin 7 as input with an internal pull-up resistor
    }

    void loop() {
        int buttonState = digitalRead(7);  // Read the state of the button
        // Check if button state has changed from the last loop iteration
        if (lastButtonState == HIGH && buttonState == LOW) {  // Button press detected
            relayState = !relayState;                           // Toggle relay module state
            digitalWrite(2, relayState);                        // Set the relay module state
        }
        lastButtonState = buttonState;  // Update lastButtonState to the current state
        delay(200);                     // Optional: Simple software debouncing
    }

11. 最後に、コードを保存し、作業スペースを整理することを忘れないでください。

**質問**

1. デジタルピン7を ``INPUT`` のみに設定した場合、どうなりますか？その理由は？

.. code-block::
    :emphasize-lines: 3

    void setup() {
        pinMode(9, OUTPUT);        // Set pin 9 as output
        pinMode(7, INPUT);  // Set pin 7 as input with an internal pull-up resistor
        Serial.begin(9600);        // Serial communication setup at 9600 baud
    }

2. ピン7が ``INPUT`` のみに設定されている場合、回路にどのような調整が必要ですか？

**まとめ**

このコースでは、LEDを高電力負荷の代わりとして使用し、リレー制御された回路を構築することに取り組みました。プロジェクトでは、ブレッドボード上での回路構築、コンポーネントの配線、ボタン入力に基づいてリレーを制御するためのArduinoのプログラミングが含まれていました。マルチメータを使用したテストを通じて、リレーモジュールの機能を確認し、異なる信号条件での動作を理解しました。

コード作成セグメントでは、状態変化の概念と、条件付きロジックを使用して物理デバイスを制御する方法が強化されました。このコースを完了することで、リレーを使用した電子プロジェクトの理論的および実用的な側面を理解し、将来より複雑で多様な応用にこれらの概念を適用する能力を向上させました。


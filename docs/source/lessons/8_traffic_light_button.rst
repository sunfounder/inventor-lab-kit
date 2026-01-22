.. note::

    こんにちは！SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community へようこそ！このFacebookコミュニティで、Raspberry Pi、Arduino、ESP32についてさらに深く学び、仲間と一緒に楽しみましょう。

    **参加する理由は？**

    - **エキスパートサポート**: 購入後の問題解決や技術的な課題を、コミュニティやチームのサポートで解決。
    - **学びと共有**: スキルを向上させるためのヒントやチュートリアルを交換しましょう。
    - **先行プレビュー**: 新製品の発表やプレビューにいち早くアクセス。
    - **特別割引**: 最新製品に対する特別割引を楽しみましょう。
    - **イベントプロモーションとプレゼント企画**: イベントやプレゼント企画に参加しよう。

    👉 私たちと一緒に探求し、クリエイトする準備ができましたか？[|link_sf_facebook|] をクリックして今すぐ参加してください！

8. 歩行者ボタン付き信号機
===============================================

Arduinoの旅の次のステップへようこそ。前回のレッスンでは、赤、黄、緑の信号灯で道路の交通を制御する基本的な信号機システムを構築しました。今回は、歩行者用ボタンという新しいインタラクション層を追加します。この機能は、交差点での歩行者と車両の動きをより動的に管理する現実世界の複雑さを反映しています。

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/8_traffic_light_button.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

このレッスンで学ぶこと:

* ボタンの仕組みと回路における役割を理解する。
* ``digitalRead()`` を使ってピン入力レベルを検出する方法を学ぶ。
* ``if`` 文を使用して信号機システムに条件付きの動作を実装する。

このプロジェクトに取り組む中で、技術的なセットアップだけでなく、歩行者や車両の交通を効率的に管理するためのロジックとプログラミングも探求していきます。

回路を作成する
-----------------------------

**必要な部品**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 赤色LED
     - 1 * 黄色LED
     - 1 * 緑色LED
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_yellow_led| 
     - |list_green_led| 
   * - 1 * 押しボタン
     - 1 * ブレッドボード
     - 3 * 220Ω 抵抗
     - 1 * 10K オーム抵抗
   * - |list_button| 
     - |list_breadboard| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * USBケーブル
     - ジャンパーワイヤー
     - 1 * マルチメーター
     - 
   * - |list_usb_cable| 
     - |list_wire| 
     - |list_meter|
     - 


**ステップバイステップの作成手順**

配線図または以下の手順に従って回路を作成します。

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center  

1. 前回のレッスンで作成した信号機回路を基に作業を始めます。

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

2. 押しボタンを用意します。

.. image:: img/8_traffic_button.png
    :width: 500
    :align: center

ボタンは電子機器において一般的な部品であり、回路を作ったり切ったりするスイッチとして機能します。以下はボタンの内部構造と、回路図で使われる一般的なシンボルです。

.. image:: img/8_traffic_button_symbol.png
    :width: 500
    :align: center

ボタンには4つのピンがありますが、ピン1と2、ピン3と4がそれぞれ接続されています。ボタンを押すと、4つのピンすべてが接続されて回路が閉じられます。

3. ボタンをブレッドボードの中央の溝をまたぐ形で差し込み、ピンを穴18e、18f、20e、20fに挿入します。

.. note::

    ボタンの差し込み方が不安な場合は、両方の向きで試してみてください。片方の向きではピンの間隔がわずかに狭く、うまく差し込めないはずです。

.. image:: img/8_traffic_light_button_button.png
    :width: 600
    :align: center

4. ボタンの右上のピンを、長いジャンパーワイヤーを使ってArduino Uno R3のデジタルピン8に接続します。一方の端を穴18jに、もう一方をピン8に挿入します。

.. image:: img/8_traffic_light_button_pin8.png
    :width: 600
    :align: center

5. ボタンの左上のピンとグラウンドの間に10Kオームの抵抗を設置し、一方の端を穴18aに、もう一方の端をブレッドボードのマイナス側のレールに接続します。この抵抗はピン8をグラウンドに引き下げ、ボタンが押されていないときにLOWの状態を安定させます。

    .. image:: img/8_traffic_light_button_10k.png
        :width: 600
        :align: center

ピン8はボタンの状態を読み取るための入力として機能します。Arduinoボードは入力ピンで0〜約5ボルトの電圧を読み取り、閾値電圧に基づいてそれをLOWまたはHIGHとして解釈します。ピンがHIGHと読み取られるには3ボルト以上が必要で、LOWと読み取られるには1.5ボルト以下である必要があります。

もし10Kオームの抵抗がなければ、ピン8はボタンだけに接続され、0Vから5Vの間で浮遊するため、状態がHIGHとLOWの間でランダムに変動してしまいます。

ピン8をグラウンドに引き下げる10Kオームの抵抗は、ボタンが押されていないときにピンがLOWと読み取られるように電圧をグラウンドレベルに引き下げます。

6. 最後に、赤い電源ワイヤーを使ってブレッドボードのプラス側レールをArduino Uno R3の5Vピンに接続し、ボタンに電源を供給します。

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center


**質問:**

あなたの信号機は直列回路と並列回路の組み合わせです。回路のどの部分が直列になっているのか、その理由を説明してください。そして、どの部分が並列になっているのか、その理由も説明してください。


コードの作成
----------------

**ピンの初期化**

これまで、信号機を緑、黄、赤のLEDが順番に点滅するようにプログラムしてきました。このレッスンでは、歩行者用のボタンをプログラムし、押されたときに赤と黄のLEDが消灯し、緑のLEDが点滅して歩行者が安全に渡れることを示すようにします。

1. 以前に保存したスケッチ ``Lesson7_Traffic_Light`` を開き、「ファイル」メニューから「名前を付けて保存」を選び、 ``Lesson8_Traffic_Light_Button`` と名前を変更して保存します。

2. ``void setup()`` 関数内で、もう一つの ``pinMode()`` コマンドを追加し、ピン8を入力(``INPUT``)として宣言します。次に、新しいコマンドを説明するコメントを追加します。

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // 初期設定コードはここに記述します。1度だけ実行されます。
        pinMode(3, OUTPUT); // ピン3を出力として設定
        pinMode(4, OUTPUT); // ピン4を出力として設定
        pinMode(5, OUTPUT); // ピン5を出力として設定
        pinMode(8, INPUT);  // ピン8（ボタン）を入力として宣言
    }
    
    void loop() {
        // メインコードはここに記述します。繰り返し実行されます。
        digitalWrite(3, HIGH);  // ピン3のLEDを点灯
        digitalWrite(4, LOW);   // ピン4のLEDを消灯
        digitalWrite(5, LOW);   // ピン5のLEDを消灯
        delay(10000);           // 10秒待機
        digitalWrite(3, LOW);   // ピン3のLEDを消灯
        digitalWrite(4, HIGH);  // ピン4のLEDを点灯
        digitalWrite(5, LOW);   // ピン5のLEDを消灯
        delay(3000);            // 3秒待機
        digitalWrite(3, LOW);   // ピン3のLEDを消灯
        digitalWrite(4, LOW);   // ピン4のLEDを消灯
        digitalWrite(5, HIGH);  // ピン5のLEDを点灯
        delay(10000);           // 10秒待機
    }

3. コーディング後、スケッチを検証してArduino Uno R3にコードをアップロードします。

**ピン8での電圧測定**

前回のレッスンで、回路のLEDセクションがどのように機能するかを理解しました。各LEDは出力として機能し、Arduino Uno R3の異なるピンによって制御されます。

しかし、ボードのピン8に接続されたボタンは異なります。これは入力デバイスです。ピン8は電圧を送信する代わりに、入力される電圧を読み取ります。

ボタンが押されたときとリリースされたときのピン8の電圧をテストするために、マルチメーターを使用しましょう。友人に手伝ってもらい、ボタンを押してもらう必要があるかもしれません。

1. マルチメーターを20ボルトのDC設定に調整します。

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. ボタンが押されていない状態で、ピン8の電圧を測定します。マルチメーターの赤いテストリードをピン8に、黒いテストリードをGNDに触れさせます。

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

3. 測定した電圧を表に記録します。

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - ボタンの状態
     - ピン8の電圧
     - 状態
   * - リリース
     - *0.00ボルト*
     - 
   * - プレス
     -
     - 

4. 友人に手伝ってもらい、ボタンを押した状態でピン8の電圧を測定します。

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

5. ボタンが押されたときのピン8の電圧を表に記録します。

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - ボタンの状態
     - ピン8の電圧
     - 状態
   * - リリース
     - *0.00ボルト*
     - 
   * - プレス
     - *≈4.97ボルト*
     - 

6. Arduinoボードは、入力ピンで0〜約5ボルトの電圧を読み取り、しきい値電圧に基づいてそれを ``LOW`` または ``HIGH`` として解釈します。ピンが ``HIGH`` と読み取られるためには、3ボルト以上の電圧が必要です。 ``LOW`` と読み取られるためには、1.5ボルト未満である必要があります。

   測定された電圧に基づいて、ピン8の状態を記入します。

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - ボタンの状態
     - ピン8の電圧
     - ピン8の状態
   * - リリース
     - *0.00ボルト*
     - *LOW*
   * - プレス
     - *≈4.97ボルト*
     - *HIGH*

**条件文**

信号機は、ボタンが押されたかどうかに応じて2つの異なる動作を行う必要があります。

* ボタンが押されたときには、歩行者用信号のコードが実行され、緑のLEDが点滅します。
* ボタンが押されていないときには、信号機は通常どおりに動作します。

これらの動作をプログラムするために、条件文と呼ばれる新しいコーディング機能を使用します。

条件文は、 ``if-then`` 文や単に ``if`` 文と呼ばれることがあります。
条件文を使用することで、特定の条件や状況が真であるときに特定のコードを実行することができます。

.. image:: img/if.png
    :width: 300
    :align: center

.. note::

    日常生活でも、意思決定を行う際に条件文を頻繁に使用しています。例えば：

    .. code-block:: Arduino

        start;
        if cold;
        then wear a coat;
        end;

Arduino IDEでは、条件文は次のように記述します。

    .. code-block:: Arduino

        if (condition) {
            commands to run when the condition is true 
        }

``condition`` は丸括弧内にあり、比較演算子を使用して2つ以上の値を比較します。これらの値は数値、変数、またはArduino Uno R3に入力される信号であることがあります。

以下は、比較演算子とそれらが条件文の中でどのように使用されるかのリストです：

.. list-table::
    :widths: 20 20 60
    :header-rows: 1

    *   - 比較演算子
        - 意味
        - 例
    *   - ==
        - 等しい
        - if (digitalRead(8) == HIGH) {do something}
    *   - !=
        - 等しくない
        - if (digitalRead(5) != LOW) {do something}
    *   - <
        - より小さい
        - if (distance < 100) {do something}
    *   - >
        - より大きい
        - if (count > 5) {do something}
    *   - <=
        - 以下
        - if (number <= minValue) {do something}
    *   - >=
        - 以上
        - if (number >= maxValue) {do something}

.. note::

    等号比較には、2つの等号(``==``)を使用します。1つの等号(``=``)は変数に値を割り当てるために使用され、2つの等号(``==``)は2つの値を比較するために使用されます。

条件内で2つの値を比較すると、その結果は ``True`` または ``False`` になります。条件が ``True`` の場合、波括弧内のコマンドが実行されます。条件が ``False`` の場合、波括弧内のコマンドはスキップされます。

プログラミングにおいて、条件文は単純なものから複数の条件やシナリオを含む複雑な論理を扱うものまでさまざまです。次に、基本的な ``if`` 文を使用していきます。

**ボタンが押されていない場合**

条件文の理解を深めたところで、この概念を信号機スケッチに応用してみましょう。ボタンが押されると交通の流れが変わるため、ボタンの状態を監視する条件を組み込みます。

1. ピン8の電圧の測定結果から、ボタンが押されていないときはピン8が ``LOW`` であることがわかっています。つまり、ピン8の状態が ``LOW`` であると読み取られた場合、それはボタンが押されていないことを意味します。次に、前のコードの ``void loop()`` 関数の冒頭に次の文を入力します：

    .. code-block:: Arduino
        :emphasize-lines: 11,13

        void setup() {
            // 初期設定コードはここに記述します。1度だけ実行されます。
            pinMode(3, OUTPUT); // ピン3を出力として設定
            pinMode(4, OUTPUT); // ピン4を出力として設定
            pinMode(5, OUTPUT); // ピン5を出力として設定
            pinMode(8, INPUT);  // ピン8（ボタン）を入力として宣言
        }

        void loop() {
            // メインコードはここに記述します。繰り返し実行されます。
            if (digitalRead(8) == LOW) {
                
            }

            digitalWrite(3, HIGH);  // ピン3のLEDを点灯
            digitalWrite(4, LOW);   // ピン4のLEDを消灯
            digitalWrite(5, LOW);   // ピン5のLEDを消灯

            ...

``digitalWrite()`` コマンドが出力ピンに使用されるのと同様に、 ``digitalRead()`` コマンドは入力ピンに使用されます。 ``digitalRead(pin)`` は、デジタルピンが ``HIGH`` か ``LOW`` かを読み取るためのコマンドです。

その構文は次のとおりです：

    * ``digitalRead(pin)``: 指定されたデジタルピンから値を読み取ります。 ``HIGH`` または ``LOW`` のいずれかを返します。

        **パラメータ**
            - ``pin``: 読み取るArduinoピン番号
        
        **戻り値**
            ``HIGH`` または ``LOW``


**2. 次に、ボタンが押されていない場合に実行するコマンドを追加します。これらのコマンドは、通常の信号機を動作させるために既に作成したものです。**

    * これらのコマンドを ``if`` 文の波括弧内にカット＆ペーストすることができます。
    * または、 ``if`` 文の右波括弧を最後の ``delay`` の後に移動するだけでもかまいません。
    * どちらの方法でも問題ありません。完了後、 ``void loop()`` 関数は次のようになります。

.. code-block:: Arduino
    :emphasize-lines: 11,24

    void setup() {
        // 初期設定コードはここに記述します。1度だけ実行されます。
        pinMode(3, OUTPUT); // ピン3を出力として設定
        pinMode(4, OUTPUT); // ピン4を出力として設定
        pinMode(5, OUTPUT); // ピン5を出力として設定
        pinMode(8, INPUT);  // ピン8（ボタン）を入力として宣言
    }

    void loop() {
        // メインコードはここに記述します。繰り返し実行されます。
        if (digitalRead(8) == LOW) {
            digitalWrite(3, HIGH);  // ピン3のLEDを点灯
            digitalWrite(4, LOW);   // ピン4のLEDを消灯
            digitalWrite(5, LOW);   // ピン5のLEDを消灯
            delay(10000);           // 10秒待つ
            digitalWrite(3, LOW);   // ピン3のLEDを消灯
            digitalWrite(4, HIGH);  // ピン4のLEDを点灯
            digitalWrite(5, LOW);   // ピン5のLEDを消灯
            delay(3000);            // 3秒待つ
            digitalWrite(3, LOW);   // ピン3のLEDを消灯
            digitalWrite(4, LOW);   // ピン4のLEDを消灯
            digitalWrite(5, HIGH);  // ピン5のLEDを点灯
            delay(10000);           // 10秒待つ
        }
    }

このように、 ``if`` 文内のコマンドがインデントされています。インデントを使用することで、コードを整然と保ち、関数内で実行されるコマンドが明確になります。インデントや改行、コードコメントを使用することで、コードの見た目が良くなり、長期的に有益です。

よくある構文エラーとしては、必要な数の波括弧を忘れることがあります。関数内で右波括弧を忘れたり、逆に右波括弧を多く追加しすぎることがあります。スケッチ内のすべての左波括弧には右波括弧が必要です。適切なインデントは、波括弧の不一致をトラブルシューティングするのにも役立ちます。


**ボタンが押された場合**

次に、ボタンが押されたときに歩行者が道路を渡れるようにするコードを書きます。

これには2つ目の条件文が必要です。ただし、今回は ``digitalRead()`` の値を ``LOW`` ではなく ``HIGH`` と比較します。

ボタンが押されると、信号機はすべての車両を停止させ、歩行者が安全に渡れるようにする必要があります。これを実現するために、赤と黄色のLEDを消灯し、緑のLEDを点滅させます。2つ目の条件文の波括弧内に、3つの ``digitalWrite()`` コマンドを追加します。

* ピン3に接続された緑のLEDを点灯する。
* ピン4に接続された黄色のLEDを消灯する。
* ピン5に接続された赤のLEDを消灯する。

次に、緑のLEDを点滅させます。点滅の頻度は、 ``delay()`` 文で決まります。

スケッチは次のようになります。

.. code-block:: Arduino
    :emphasize-lines: 24-31

    void setup() {
        pinMode(3, OUTPUT);  // ピン3（緑色LED）を出力として宣言
        pinMode(4, OUTPUT);  // ピン4（黄色LED）を出力として宣言
        pinMode(5, OUTPUT);  // ピン5（赤色LED）を出力として宣言
        pinMode(8, INPUT);   // ピン8（ボタン）を入力として宣言
    }

    void loop() {
        // Main code to run repeatedly:
        if (digitalRead(8) == LOW) {
            digitalWrite(3, HIGH);  // Light up the LED on pin 3
            digitalWrite(4, LOW);   // Switch off the LED on pin 4
            digitalWrite(5, LOW);   // Switch off the LED on pin 5
            delay(10000);           // Wait for 10 seconds
            digitalWrite(3, LOW);   // Switch off the LED on pin 3
            digitalWrite(4, HIGH);  // Light up the LED on pin 4
            digitalWrite(5, LOW);   // Switch off LED on pin 5
            delay(3000);            // Wait for 3 seconds
            digitalWrite(3, LOW);   // Switch off the LED on pin 3
            digitalWrite(4, LOW);   // Switch off the LED on pin 4
            digitalWrite(5, HIGH);  // Light up LED on pin 5
            delay(10000);           // Wait for 10 seconds
        }
        if (digitalRead(8) == HIGH) {  //if the button is pressed:
            digitalWrite(3, HIGH);       // Light up the LED on pin 3
            digitalWrite(4, LOW);        // Switch off the LED on pin 4
            digitalWrite(5, LOW);        // Switch off the LED on pin 5
            delay(500);                  // Wait half a second
            digitalWrite(3, LOW);        // Switch off the LED on pin 3
            delay(500);                  // Wait half a second
        }
    }

コードをArduino Uno R3にアップロードします。スケッチが完全に転送されると、コードが実行されます。

信号機の動作を観察してください。ボタンを押して信号機がサイクルを完了するのを待ちます。歩行者用の緑色のライトが点滅しますか？ボタンを離したとき、信号機は通常の操作モードに戻りますか？そうでない場合は、スケッチを調整し、再度R3にアップロードします。

完了したら、スケッチを保存します。


**質問:**

テスト中に、歩行者用の緑色LEDがボタンを押し続けている間だけ点滅することに気づくかもしれませんが、歩行者が道路を横断するためにはボタンを押し続ける必要はありません。ボタンが一度押されたら、緑色LEDが安全に横断できるだけの時間点灯するようにするには、コードをどのように変更すればよいでしょうか？疑似コードで解決策を手帳に書き留めてください。


**まとめ**

このレッスンでは、信号機システムに歩行者ボタンを組み込み、歩行者と車両の両方の交通の流れを調整する現実のシナリオをシミュレートしました。電子回路内のボタンの動作を調べ、 ``digitalRead()`` 関数を使用してボタンからの入力を監視しました。 ``if`` 構造を使用した条件文を実装することで、信号機が歩行者の入力に応じて動的に反応するようにプログラムし、インタラクティブシステムの理解を深めました。このレッスンは、Arduinoプログラミングのスキルを強化するだけでなく、これらの技術を日常の状況管理に効率的に適用する実用的な方法を強調しました。


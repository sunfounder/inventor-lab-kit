.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauchen Sie mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Lösen Sie nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Tutorials aus, um Ihre Fähigkeiten zu verbessern.
    - **Exklusive Einblicke**: Erhalten Sie frühzeitig Zugriff auf neue Produktankündigungen und exklusive Vorschauen.
    - **Spezielle Rabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nehmen Sie an Verlosungen und festlichen Aktionen teil.

    👉 Bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie noch heute bei!

28. Anzeige von Zahlen mit dem 74HC595
=============================================

In der vorherigen Lektion haben Sie vielleicht bemerkt, dass der 74HC595 und das 7-Segment-Display perfekt zusammenpassen. Der 74HC595 kann gleichzeitig 8-Bit-Signale ausgeben, während das 7-Segment-Display von 8 elektrischen Signalen gesteuert wird (einschließlich des Dezimalpunkt-LED-Segments, also dem dp-Segment).

Kann also der 74HC595 zur Steuerung des 7-Segment-Displays verwendet werden? Die Antwort lautet ja.

In dieser Lektion werden wir den 74HC595 verwenden, um das 7-Segment-Display zu steuern und verschiedene Zahlen anzuzeigen.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/28_show_number.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In dieser Lektion werden Sie lernen:

* Verstehen, wie man das 74HC595-Schieberegister verwendet, um ein 7-Segment-Display anzusteuern.
* Lernen der binären Darstellungen der Ziffern 0 bis 9 und wie man diese in dezimale und hexadezimale Formate umwandelt.
* Verstehen, wie man den seriellen Monitor verwendet, um Daten einzugeben und auf dem 7-Segment-Display anzuzeigen.


Aufbau der Schaltung
--------------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 7-Segment-Display
     - 1 * 220Ω Widerstand
     - 1 * 74HC595
   * - |list_uno_r3| 
     - |list_7segment| 
     - |list_220ohm| 
     - |list_74hc595| 
   * - 1 * Steckbrett
     - Jumper-Kabel
     - 1 * USB-Kabel
     -
   * - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
     -

**Schritt-für-Schritt Aufbau**

Folgen Sie dem Verdrahtungsdiagramm oder den unten stehenden Schritten, um Ihre Schaltung zu erstellen.

.. image:: img/25_show_number.png
    :width: 500
    :align: center

1. Setzen Sie das 7-Segment-Display in das Steckbrett ein, wobei der Dezimalpunkt in der unteren rechten Ecke liegt.

.. image:: img/25_show_number_7segment.png
    :width: 500
    :align: center

2. Verbinden Sie den negativen (-) Anschluss des 7-Segment-Displays mit der Masseleitung des Steckbretts mithilfe eines Jumper-Kabels.

.. image:: img/25_show_number_resistor.png
    :width: 500
    :align: center

3. Platzieren Sie den 74HC595-Chip und stecken Sie ihn in das Steckbrett. Achten Sie darauf, dass der Chip die mittlere Lücke überspannt.

.. image:: img/25_show_number_74hc595.png
    :width: 500
    :align: center

4. Verbinden Sie die VCC- und MR-Pins des 74HC595 mit der positiven Leitung auf dem Steckbrett.

.. image:: img/25_show_number_vcc.png
    :width: 500
    :align: center

5. Verbinden Sie die CE- und GND-Pins des 74HC595 mit der negativen Leitung auf dem Steckbrett.

.. image:: img/25_show_number_gnd.png
    :width: 500
    :align: center

6. Verbinden Sie Q0 des 74HC595 mit dem 'a'-Pin des 7-Segment-Displays, Q1 mit dem 'b'-Pin, Q2 mit dem 'c'-Pin, Q3 mit dem 'd'-Pin und Q4 mit dem 'e'-Pin.

.. image:: img/25_show_number_q0_q4.png
    :width: 500
    :align: center

7. Verbinden Sie Q5 des 74HC595 mit dem 'f'-Pin des 7-Segment-Displays, Q6 mit dem 'g'-Pin und Q7 mit dem 'dp'-Pin.

.. image:: img/25_show_number_q5_q7.png
    :width: 500
    :align: center

8. Verbinden Sie den DS-Pin des 74HC595 mit Pin 11 des Arduino Uno R3.

.. image:: img/25_show_number_pin11.png
    :width: 500
    :align: center

9. Verbinden Sie den ST_CP-Pin des 74HC595 mit Pin 12 des Arduino Uno R3.

.. image:: img/25_show_number_pin12.png
    :width: 500
    :align: center

10. Verbinden Sie den SH_CP-Pin des 74HC595 mit Pin 8 des Arduino Uno R3.

.. image:: img/25_show_number_pin8.png
    :width: 500
    :align: center

11. Verbinden Sie abschließend die GND- und 5V-Pins des Arduino Uno R3 mit den negativen bzw. positiven Leitungen auf dem Steckbrett.

.. image:: img/25_show_number.png
    :width: 500
    :align: center

12. Die folgende Tabelle zeigt die Pinverbindungen zwischen dem 74HC595, dem Arduino Uno R3 und dem 7-Segment-Display.

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 74HC595
        - Arduino UNO R3
    *   - VCC
        - 5V
    *   - DS
        - 11
    *   - CE
        - GND
    *   - ST_CP
        - 12
    *   - SH_CP
        - 8
    *   - MR
        - 5V
    *   - GND
        - GND

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 74HC595
        - 7-Segment-Display
    *   - Q0
        - a
    *   - Q1
        - b 
    *   - Q2
        - c
    *   - Q3
        - d
    *   - Q4
        - e
    *   - Q5
        - f
    *   - Q6
        - g
    *   - Q7
        - dp

Binärzahlen für die Ziffern 0 bis 9
---------------------------------------

In diesem Projekt verwenden wir das 74HC595-Schieberegister, um das 7-Segment-Display anzusteuern und verschiedene Zahlen anzuzeigen. Da der 74HC595 jedoch Binärzahlen empfängt, müssen wir vor dem Programmieren die entsprechenden Binärzahlen für die Ziffern 0 bis 9 kennen.

Angenommen, wir möchten die Ziffer 2 auf dem 7-Segment-Display anzeigen, dann müssen die Segmente f und c ausgeschaltet und die restlichen Segmente eingeschaltet werden.

.. image:: img/23_segment_2.png
    :align: center
    :width: 200

Entsprechend dem Verdrahtungsdiagramm entsprechen die Ausgangspins Q0 bis Q7 des 74HC595 den jeweiligen Pins des 7-Segment-Displays, wie im Diagramm dargestellt. In binärer Form steht 0 für aus (geschlossen) und 1 für ein (offen). Um die Ziffer 2 anzuzeigen, sollten dp, f und c auf 0 gesetzt werden, während die anderen Segmente auf 1 stehen, was die Binärzahl ``B01011011`` ergibt.

.. image:: img/25_display_2_binary.png
    :align: center
    :width: 600

.. note::

    Wenn Sie nur ein 7-Segment-Display haben, wird der DP-Pin immer auf 0 gesetzt. Wenn Sie mehrere 7-Segment-Displays in einer Kaskadenkonfiguration haben, können Sie den DP-Pin verwenden, um den Dezimalpunkt anzuzeigen.

Um die Ziffer 0 anzuzeigen, sollten dp und g auf 0 gesetzt werden, und alle anderen Segmente sollten auf 1 stehen, was die Binärzahl ``B00111111`` ergibt.

**Frage**

Da wir nun die binären Darstellungen für die Ziffern 0 und 2 kennen, füllen Sie bitte die Binärzahlen für die restlichen Ziffern in der folgenden Tabelle aus.

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - Zahl
        - Binär
    *   - 0
        - B00111111
    *   - 1
        -
    *   - 2
        - B01011011
    *   - 3
        -
    *   - 4
        -
    *   - 5
        -
    *   - 6
        -
    *   - 7
        -
    *   - 8
        -
    *   - 9
        -        


Code-Erstellung - Zahlen anzeigen
------------------------------------------

1. Öffnen Sie die zuvor gespeicherte Skizze ``Lesson28_Flowing_Light``. Wählen Sie „Speichern unter...“ im Menü „Datei“ und benennen Sie die Datei in ``Lesson28_Show_Number_Binary`` um. Klicken Sie auf "Speichern".

2. Ändern Sie das ``datArray[]``, um die entsprechenden Binärzahlen für die Ziffern 0 bis 9 anzuzeigen.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int STcp = 12;  //Pin verbunden mit ST_CP des 74HC595
    const int SHcp = 8;   //Pin verbunden mit SH_CP des 74HC595
    const int DS = 11;    //Pin verbunden mit DS des 74HC595
    //zeige 0,1,2,3,4,5,6,7,8,9 an
    int datArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };


3. Da das ``datArray[]``-Array 10 Elemente enthält, ändern Sie den Bereich der Variable ``num`` auf ``num <= 9``.

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        for (int num = 0; num <= 9; num++) {
            digitalWrite(STcp, LOW);                      // ST_CP auf Masse setzen und niedrig halten, während Daten übertragen werden
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Daten ausgeben, MSB zuerst
            digitalWrite(STcp, HIGH);                     // ST_CP auf HIGH setzen, um die Daten zu speichern
            delay(1000);                                  // Eine Sekunde warten
        }
    }

4. Ihr vollständiger Code sollte wie folgt aussehen. Sie können den Code nun auf das Arduino Uno R3 hochladen, und das 7-Segment-Display wird die Ziffern 0 bis 9 durchlaufen.


.. code-block:: Arduino

    const int STcp = 12;  //Pin verbunden mit ST_CP des 74HC595
    const int SHcp = 8;   //Pin verbunden mit SH_CP des 74HC595
    const int DS = 11;    //Pin verbunden mit DS des 74HC595
    //zeige 0,1,2,3,4,5,6,7,8,9 an
    int datArray[] = { B00111111, B00000110, B01011011, B01001111, B01100110, B01101101, B01111101, B00000111, B01111111, B01101111 };

    void setup() {
        //Pins als Ausgang setzen
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop() {
        for (int num = 0; num <= 9; num++) {
            digitalWrite(STcp, LOW);                      // ST_CP auf Masse setzen und niedrig halten, während Daten übertragen werden
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Daten ausgeben, MSB zuerst
            digitalWrite(STcp, HIGH);                     // ST_CP auf HIGH setzen, um die Daten zu speichern
            delay(1000);                                  // Eine Sekunde warten
        }
    }

Binärumrechnung
---------------------

In praktischen Anwendungen kann das Schreiben von Binärzahlen den Zustand jedes Bits in den Daten klarer ausdrücken. Für die allgemeine Zahlenrepräsentation ist es jedoch bequemer, Dezimalzahlen zu schreiben.

.. note::

    Das Schreiben von Binär-, Dezimal- oder sogar Hexadezimalzahlen beeinflusst das Ergebnis des Programms nicht, sondern nur die Lesbarkeit des Codes. Zum Beispiel wird die Dezimalzahl ``91`` intern in die Binärform ``B01011011`` umgewandelt.

Sehen wir uns an, wie man Binärzahlen in Dezimalzahlen umwandelt.

**Umrechnung in Dezimalzahlen**

Im Binärsystem repräsentiert jedes Bit einen entsprechenden Stellenwert. Der Stellenwert ist eine Potenz von 2, wie z.B. 2^0, 2^1, 2^2… usw. Durch Multiplikation jedes Bits mit seinem entsprechenden Stellenwert und das Addieren aller Ergebnisse erhalten wir die Dezimalzahl.

Zum Beispiel wird die Binärzahl ``B01011011`` in die Dezimalzahl 91 umgewandelt.

.. image:: img/25_binary_dec.png
    :align: center
    :width: 600
 
**Verwendung eines Taschenrechners**

In praktischen Anwendungen können Sie den Taschenrechner auf Ihrem Computer verwenden. Wechseln Sie in den Programmierermodus, und Sie können einfach zwischen Binär-, Dezimal- und Hexadezimalzahlen umrechnen.

1. Suchen Sie auf Ihrem Computer nach "Taschenrechner" und wechseln Sie dann in den **Programmierer**-Modus.

.. image:: img/25_calculator_programmer.png
    :align: center

2. Wenn Sie die Binärzahl bereits kennen und sie in eine andere Basis umrechnen möchten, wählen Sie **BIN**.

.. image:: img/25_calculator_binary.png
    :align: center

3. Nun können Sie die Binärzahl eingeben.

* Die effektiven Bits im Binärsystem beziehen sich auf den Bereich vom höchstwertigen Bit (linkes nicht-null Bit) bis zum niedrigstwertigen Bit (rechtes nicht-null Bit).
* Für die Binärzahl ``B00111111`` sind die effektiven Bits ``111111``.
* Geben Sie nun ``111111`` in den Taschenrechner ein, um die entsprechenden Dezimal- und Hexadezimalzahlen zu erhalten.

.. image:: img/25_calculator_binary_0.png
    :align: center
    :width: 300

**Frage**

Bitte konvertieren Sie die Binärzahlen, die die Ziffern 0 bis 9 darstellen, mit einem Taschenrechner in Dezimal- und Hexadezimalzahlen und füllen Sie die Tabelle aus. Dies wird Ihnen als schnelles Nachschlagewerk für Basisumrechnungen dienen.

.. list-table::
    :widths: 20 40 30 30
    :header-rows: 1

    *   - Zahl
        - Binär
        - Dezimal
        - Hexadezimal
    *   - 0
        - B00111111
        - 63
        - 0x3F
    *   - 1
        - B00000110
        -
        -
    *   - 2
        - B01011011
        -
        -
    *   - 3
        - B01001111
        -
        -
    *   - 4
        - B01100110
        -
        -
    *   - 5
        - B01101101
        -
        -
    *   - 6
        - B01111101
        -
        -
    *   - 7
        - B00000111
        -
        -
    *   - 8
        - B01111111
        -
        -
    *   - 9
        - B01101111
        -
        -

**Skizze ändern**

Öffnen Sie nun Ihre Skizze ``Lesson28_Show_Number_Binary`` in der Arduino-IDE. Klicken Sie auf "Datei" -> "Speichern unter...", benennen Sie die Datei in ``Lesson28_Show_Number_Decimal`` um. Klicken Sie auf "Speichern".

Ändern Sie alle Elemente des ``datArray[]`` auf Dezimalwerte, wie im Code gezeigt. Nachdem Sie die Änderungen vorgenommen haben, können Sie den Code auf das Arduino Uno R3 hochladen, um den Effekt zu sehen.

.. code-block:: Arduino

    const int STcp = 12;  //Pin verbunden mit ST_CP des 74HC595
    const int SHcp = 8;   //Pin verbunden mit SH_CP des 74HC595
    const int DS = 11;    //Pin verbunden mit DS des 74HC595
    //zeige 0,1,2,3,4,5,6,7,8,9 an
    int datArray[] = { 63, 6, 91, 79, 102, 109, 125, 7, 127, 111 };

    void setup() {
        //Pins als Ausgang setzen
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
    }

    void loop() {
        for (int num = 0; num <= 9; num++) {
            digitalWrite(STcp, LOW);                      // ST_CP auf Masse setzen und niedrig halten, während Daten übertragen werden
            shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Daten ausgeben, MSB zuerst
            digitalWrite(STcp, HIGH);                     // ST_CP auf HIGH setzen, um die Daten zu speichern
            delay(1000);                                  // Eine Sekunde warten
        }
    }


Code-Erstellung - Serielle Eingabe
-------------------------------------------

Der serielle Monitor ist ein leistungsstarkes Werkzeug, das von der Arduino-IDE zur Kommunikation mit dem Arduino-Board bereitgestellt wird. Wir haben ihn verwendet, um die Datenausgabe vom Arduino zu überwachen, z. B. das Lesen von Analogwerten eines Fotowiderstands. Er kann auch verwendet werden, um Daten an das Arduino zu senden, damit es basierend auf den empfangenen Daten Aktionen ausführt.

In dieser Aktivität werden wir eine Zahl zwischen 0 und 9 in den seriellen Monitor eingeben, um sie auf dem 7-Segment-Display anzuzeigen.

1. Öffnen Sie Ihre Skizze ``Lesson28_Show_Number_Decimal`` in der Arduino-IDE. Klicken Sie auf "Datei" -> "Speichern unter...", benennen Sie die Datei in ``Lesson28_Show_Number_Serial`` um. Klicken Sie auf "Speichern".

2. Starten Sie im ``void setup()`` den seriellen Monitor und setzen Sie dessen Baudrate auf 9600.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        //Pins als Ausgang setzen
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
        Serial.begin(9600);  // Serielle Kommunikation mit 9600 Baud einrichten
    }

3. Bei der Verwendung des seriellen Monitors können Sie Daten, die darin eingegeben werden, über Arduino-Code lesen. Hier müssen Sie zwei Funktionen verstehen:

* ``Serial.available()``: Gibt die Anzahl der Bytes (Zeichen) zurück, die zum Lesen vom seriellen Port verfügbar sind. Dies sind Daten, die bereits eingegangen und im seriellen Empfangspuffer (der 64 Byte fasst) gespeichert wurden.
* ``Serial.read()``: Gibt den ASCII-Code des Zeichens zurück, das über den seriellen Eingang empfangen wurde.

Verwenden Sie nun eine ``if``-Anweisung in der ``void loop()``, um zu prüfen, ob Daten vom Port gelesen wurden, und drucken Sie diese dann aus.

.. note::

    Kommentieren Sie vorübergehend die for-Schleife in der ``void loop()``, die Zeichen auf dem 7-Segment-Display anzeigt, um den Druckvorgang nicht zu beeinträchtigen.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    void loop() {
        if (Serial.available() > 0) {
            //Das über den seriellen Port empfangene Zeichen ausgeben
            Serial.println(Serial.read());
        }

        // for (int num = 0; num <= 9; num++) {
        //   digitalWrite(STcp, LOW);                      // ST_CP auf Masse setzen und niedrig halten, während Daten übertragen werden
        //   shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Daten ausgeben, MSB zuerst
        //   digitalWrite(STcp, HIGH);                     // ST_CP auf HIGH setzen, um die Daten zu speichern
        //   delay(1000);                                  // Eine Sekunde warten
        // }
    }

4. Der vollständige Code wird unten angezeigt. An dieser Stelle können Sie den Code auf das Arduino Uno R3 hochladen.

.. code-block:: Arduino

    const int STcp = 12;  // Pin verbunden mit ST_CP des 74HC595
    const int SHcp = 8;   // Pin verbunden mit SH_CP des 74HC595
    const int DS = 11;    // Pin verbunden mit DS des 74HC595
    // Anzeige der Ziffern 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { 63, 6, 91, 79, 102, 109, 125, 7, 127, 111 };

    void setup() {
        // Pins als Ausgang setzen
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
        Serial.begin(9600);  // Serielle Kommunikation mit 9600 Baud einrichten
    }

    void loop() {
        if (Serial.available() > 0) {
            // Das empfangene Zeichen vom seriellen Port ausgeben
            Serial.println(Serial.read());
        }

        // for (int num = 0; num <= 9; num++) {
        //   digitalWrite(STcp, LOW);                      // ST_CP auf Masse setzen und niedrig halten, während Daten übertragen werden
        //   shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Daten ausgeben, MSB zuerst
        //   digitalWrite(STcp, HIGH);                     // ST_CP auf HIGH setzen, um die Daten zu speichern
        //   delay(1000);                                  // Eine Sekunde warten
        // }
    }

5. Nach dem Hochladen öffnen Sie den seriellen Monitor. Geben Sie in das Eingabefeld die Zahl ``0`` (oder eine andere Ziffer zwischen 0-9) ein und drücken Sie die Eingabetaste. In diesem Moment werden Sie feststellen, dass die serielle Ausgabe die Zahl ``48`` anzeigt.

.. note::

    * Wenn in der Zeilenendungsoption des seriellen Monitors "Neue Zeile" ausgewählt ist, sehen Sie auch eine ``10``.
    * ``10`` ist der ASCII-Code für ein neues Zeilenzeichen (auch LF - Line Feed genannt).

.. image:: img/25_serial_read.png
    :align: center
    :width: 600

Wo ist unsere Eingabe von ``0`` geblieben? Woher kommt die ``48``? Kann es sein, dass ``0`` eigentlich ``48`` ist?

Dies liegt daran, dass die von uns im seriellen Monitor eingegebene ``0`` als "Zeichen" und nicht als "Zahl" betrachtet wird.

Die Zeichenübertragung erfolgt nach einem Codierungsstandard, der als ASCII (American Standard Code for Information Interchange) bekannt ist.

ASCII umfasst gängige Zeichen wie Großbuchstaben (A-Z), Kleinbuchstaben (a-z), Ziffern (0-9) und Satzzeichen (wie Punkte, Kommas, Ausrufezeichen usw.). Es definiert auch einige Steuerzeichen, die zur Steuerung von Geräten und Kommunikationsprotokollen verwendet werden. Diese Steuerzeichen werden normalerweise nicht auf dem Bildschirm angezeigt, sondern zur Steuerung des Verhaltens von Geräten wie Druckern, Terminals usw. verwendet, z. B. Zeilenumbruch, Rückschritt, Wagenrücklauf usw.

Hier ist eine ASCII-Tabelle:

.. image:: img/25_ascii_table.png
    :align: center
    :width: 800

Wenn Sie das Zeichen ``0`` im seriellen Monitor eingeben, wird der ASCII-Code für das Zeichen ``0`` an das Arduino gesendet.
Im ASCII-Code ist der Code für das Zeichen ``0`` dezimal ``48``.

6. Bevor Sie mit dem Codieren fortfahren, müssen Sie den vorherigen Code, der den ASCII-Code ausgibt, auskommentieren, um Konflikte mit dem folgenden Code zu vermeiden.

.. code-block:: Arduino
    :emphasize-lines: 4

    void loop() {
        if (Serial.available() > 0) {
            // Das empfangene Zeichen vom seriellen Port ausgeben
            // Serial.println(Serial.read());
        }

        // for (int num = 0; num <= 9; num++) {
        //   digitalWrite(STcp, LOW);                      // ST_CP auf Masse setzen und niedrig halten, während Daten übertragen werden
        //   shiftOut(DS, SHcp, MSBFIRST, datArray[num]);  // Daten ausgeben, MSB zuerst
        //   digitalWrite(STcp, HIGH);                     // ST_CP auf HIGH setzen, um die Daten zu speichern
        //   delay(1000);                                  // Eine Sekunde warten
        // }
    }

7. Sie müssen eine neue ``char``-Variable erstellen, um das Zeichen zu speichern, das vom seriellen Monitor gelesen wird.

.. code-block:: Arduino
    :emphasize-lines: 6,7

    void loop() {
        if (Serial.available() > 0) {
            // Das empfangene Zeichen vom seriellen Port ausgeben
            // Serial.println(Serial.read());

            // Das empfangene Zeichen vom seriellen Port lesen
            char receivedChar = Serial.read();
        }
    }

8. Konvertieren Sie nun das Zeichen in eine Zahl. Im ASCII-Code ist der Wert für das Zeichen ``'0'`` ``48``, für ``'1'`` ``49`` usw. Durch Subtraktion des ASCII-Codes für ``'0'`` können wir den entsprechenden Zahlenwert erhalten.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        if (Serial.available() > 0) {
            // Das empfangene Zeichen vom seriellen Port ausgeben
            Serial.println(Serial.read());

            // Das empfangene Zeichen vom seriellen Port lesen
            char receivedChar = Serial.read();
            // Das Zeichen in eine Zahl umwandeln
            int digit = receivedChar - '0';
        }
    }

9. In diesem Beispiel gehen wir davon aus, dass die Eingabe numerische Zeichen von ``'0'`` bis ``'9'`` umfasst. Daher interessieren uns nur die Eingabezeichen, die in diesem Bereich liegen. Überprüfen Sie daher, ob die Zahl innerhalb des gültigen Bereichs liegt:

* Wählen Sie die zuvor auskommentierte ``for``-Schleife und drücken Sie ``Ctrl + /``, um sie wieder einzukommentieren.
* Ändern Sie dann die ``for``-Schleife in eine ``if``-Anweisung, um zu überprüfen, ob das Eingabezeichen im Bereich von ``'0'`` bis ``'9'`` liegt. Wenn dies der Fall ist, soll das 7-Segment-Display die entsprechende Zahl anzeigen.

.. code-block:: Arduino
    :emphasize-lines: 9

    void loop() {
        if (Serial.available() > 0) {
            // Das empfangene Zeichen vom seriellen Port ausgeben
            // Serial.println(Serial.read());

            // Das empfangene Zeichen vom seriellen Port lesen
            char receivedChar = Serial.read();
            // Das Zeichen in eine Zahl umwandeln
            int digit = receivedChar - '0';

            if (digit >= 0 && digit <= 9) {
                digitalWrite(STcp, LOW);                        // ST_CP auf Masse setzen und niedrig halten, während Daten übertragen werden
                shiftOut(DS, SHcp, MSBFIRST, datArray[digit]);  // Daten ausgeben, MSB zuerst
                digitalWrite(STcp, HIGH);                       // ST_CP auf HIGH setzen, um die Daten zu speichern
                delay(1000);                                    // Eine Sekunde warten
            }
        }
    }

10. Ihr vollständiger Code sollte wie folgt aussehen. Sie können den Code jetzt auf das Arduino Uno R3 hochladen und den seriellen Monitor öffnen. Geben Sie eine beliebige Zahl zwischen 0 und 9 ein, um zu sehen, ob das 7-Segment-Display die entsprechende Zahl anzeigt.

.. code-block:: Arduino

    const int STcp = 12;  // Pin verbunden mit ST_CP des 74HC595
    const int SHcp = 8;   // Pin verbunden mit SH_CP des 74HC595
    const int DS = 11;    // Pin verbunden mit DS des 74HC595
    // Anzeige der Ziffern 0,1,2,3,4,5,6,7,8,9
    int datArray[] = { 63, 6, 91, 79, 102, 109, 125, 7, 127, 111 };

    void setup() {
        // Pins als Ausgang setzen
        pinMode(STcp, OUTPUT);
        pinMode(SHcp, OUTPUT);
        pinMode(DS, OUTPUT);
        Serial.begin(9600);  // Serielle Kommunikation mit 9600 Baud einrichten
    }   

    void loop() {
        if (Serial.available() > 0) {
            // Das empfangene Zeichen vom seriellen Port ausgeben
            // Serial.println(Serial.read());

            // Das empfangene Zeichen vom seriellen Port lesen
            char receivedChar = Serial.read();
            // Das Zeichen in eine Zahl umwandeln
            int digit = receivedChar - '0';

            if (digit >= 0 und digit <= 9) {
                digitalWrite(STcp, LOW);                        // ST_CP auf Masse setzen und niedrig halten, während Daten übertragen werden
                shiftOut(DS, SHcp, MSBFIRST, datArray[digit]);  // Daten ausgeben, MSB zuerst
                digitalWrite(STcp, HIGH);                       // ST_CP auf HIGH setzen, um die Daten zu speichern
                delay(1000);                                    // Eine Sekunde warten
            }
        }
    }

11. Denken Sie abschließend daran, Ihren Code zu speichern und Ihren Arbeitsplatz aufzuräumen.

**Zusammenfassung**

In dieser Lektion haben Sie gelernt, wie man das 74HC595-Schieberegister verwendet, um ein 7-Segment-Display anzusteuern und die Anzahl der benötigten Pins am Arduino Uno R3 zu reduzieren. Sie haben auch die binären Darstellungen der anzuzeigenden Ziffern erkundet und verstanden, wie man Binärzahlen in Dezimal- und Hexadezimalformate umwandelt, um den Code lesbarer zu machen.

Zusätzlich haben Sie gelernt, wie man den seriellen Monitor für serielle Eingaben verwendet und wie die eingegebenen Zeichen intern in ASCII-Codes umgewandelt werden. Durch das Verständnis dieser Umwandlung konnten Sie Zeichen ihren numerischen Äquivalenten zuordnen, was eine genaue Anzeige auf dem 7-Segment-Display ermöglicht.

Insgesamt hat Ihnen diese Lektion ein umfassendes Verständnis der Verwendung von Schieberegistern, der Steuerung von 7-Segment-Displays und der Handhabung serieller Kommunikation für interaktive Projekte vermittelt.

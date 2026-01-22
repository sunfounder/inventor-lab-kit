.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 zusammen mit anderen Enthusiasten ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitig Zugang zu neuen Produktankündigungen und ersten Einblicken.
    - **Sonderrabatte**: Profitiere von exklusiven Rabatten auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und besonderen Feiertagsaktionen teil.

    👉 Bereit, mit uns zu erkunden und zu erschaffen? Klicke auf [|link_sf_facebook|] und trete noch heute bei!

11. Die Farben des Regenbogens
=======================================
Stell dir vor, du könntest mit Licht malen, indem du Rot, Grün und Blau mischst, um jede erdenkliche Farbe zu erzeugen – ähnlich wie das Mischen von Farben auf einer Palette, aber mit Lichtstrahlen.

.. .. image:: img/12_rgb_mix.png
..     :width: 300
..     :align: center

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/11_rainbow_color.mp4" type="video/mp4">
        Dein Browser unterstützt das Video-Tag nicht.
    </video>

Willkommen zu dieser Lektion, in der du die faszinierende Welt der RGB-LEDs erkunden wirst und erfährst, wie die Kombination von Primärfarben ein lebendiges Farbspektrum erschaffen kann. Dieser praxisorientierte Kurs führt dich durch die Funktionsprinzipien der RGB-LEDs und zeigt dir die praktischen Anwendungen von Programmierung und Schaltungsaufbau.

In dieser Lektion wirst du lernen:

* Die Funktionsweise von RGB-LEDs zu verstehen.
* Wie du in deinem Code Funktionen erstellst und nutzt, um Aufgaben zu vereinfachen und die Lesbarkeit zu verbessern.
* Die Auswirkungen verschiedener Farbkombinationen zu erkunden, indem du die RGB-LED steuerst.
* Pulse Width Modulation (PWM) zur fein abgestimmten Farbmischung mit der RGB-LED anzuwenden.
* Deine Programmierfähigkeiten zu verbessern und den Code durch die Erstellung von Funktionen, die Parameter in Arduino verwenden, effizienter und übersichtlicher zu gestalten.

Aufbau der Schaltung
-----------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB-LED
     - 3 * 220Ω Widerstand
     - Verbindungskabel
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - 1 * Multimeter
     -
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter|
     -
     
**Schritt-für-Schritt Bauanleitung**

Folge dem Verdrahtungsdiagramm oder diesen Schritten, um die Schaltung aufzubauen.

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

1. Beginne mit einer RGB-LED.

RGB-LEDs emittieren Licht in verschiedenen Farben, indem sie rote, grüne und blaue LEDs in einem einzigen Gehäuse integrieren. Durch das Variieren der Spannung an den drei Pins können diese LEDs kombiniert werden, um bis zu 16.777.216 verschiedene Farben zu erzeugen.

.. image:: img/12_mix_color_rgb.png
    :width: 400
    :align: center

Je nach Design können RGB-LEDs entweder gemeinsame Anode oder gemeinsame Kathode haben. Für dieses Projekt verwenden wir eine **gemeinsame Kathoden-RGB-LED**, bei der alle drei LEDs eine negative Verbindung teilen.

* Gemeinsame Kathoden-RGB-LEDs haben eine gemeinsame negative Verbindung.
* Gemeinsame Anoden-RGB-LEDs haben eine gemeinsame positive Verbindung.

.. image:: img/12_rgb_cc_ca.jpg
    :width: 600
    :align: center

Eine RGB-LED hat typischerweise 4 Pins; der längste ist die Masse. Achte beim Platzieren der RGB-LED darauf, dass der längste Pin der zweite von links ist, und ordne die Pins als Rot, GND, Grün und Blau von links nach rechts.

.. image:: img/12_mix_color_rgb_1.jpg
    :width: 200
    :align: center

Du kannst auch ein Multimeter im Dioden-Testmodus verwenden, um die Farbe zu identifizieren, die jeder Pin emittiert.

Stelle das Multimeter auf den **Durchgangstest** für Widerstandsmessungen ein.

.. image:: img/multimeter_diode_measure.png
    :width: 300
    :align: center

Berühre den schwarzen Prüfspitzen des Multimeters an den längsten Pin der RGB-LED und berühre die anderen Pins einzeln mit der roten Prüfspitze. Du wirst sehen, dass die RGB-LED in Rot, Grün oder Blau aufleuchtet.

.. image:: img/12_mix_color_measure_pin.png
    :width: 500
    :align: center

2. Setze die RGB-LED in das Steckbrett ein, wobei der längste Pin in Loch 17D und die anderen drei Pins in 18C, 16C und 15C eingesetzt werden.

.. image:: img/12_mix_color_bb_1.png
    :width: 500
    :align: center

3. Setze drei 220 Ohm-Widerstände wie gezeigt ein, von Löchern 15E bis 15G, 16E bis 16G und 18E bis 18G.

.. image:: img/12_mix_color_bb_2.png
    :width: 500
    :align: center

4. Verbinde diese Widerstände mit den Pins 9, 10 und 11 des Arduino Uno R3 mittels Verbindungskabeln, wie abgebildet.

.. image:: img/12_mix_color_bb_3.png
    :width: 500
    :align: center

5. Verbinde den längsten Pin der RGB-LED mit der negativen Schiene des Steckbretts, indem du ein Verbindungskabel verwendest.

.. image:: img/12_mix_color_bb_4.png
    :width: 500
    :align: center

Codeerstellung - Eine RGB-LED zum Leuchten bringen
---------------------------------------------------------
1. Öffne die Arduino IDE und starte ein neues Projekt, indem du im Menü „Datei“ „Neues Sketch“ auswählst.
2. Speichere dein Sketch als ``Lesson11_Rainbow_Color`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Erstelle drei Variablen, um die drei Pins der RGB-LED zu speichern und setze sie auf OUTPUT.

.. code-block:: Arduino

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // Füge hier deinen Setup-Code ein, der einmal ausgeführt wird:
        pinMode(bluePin, OUTPUT);   // Setze den blauen Pin der RGB-LED auf Ausgang
        pinMode(greenPin, OUTPUT);  // Setze den grünen Pin der RGB-LED auf Ausgang
        pinMode(redPin, OUTPUT);  // Setze den roten Pin der RGB-LED auf Ausgang
    }

    void loop() {
        // Füge hier deinen Hauptcode ein, der wiederholt ausgeführt wird:
    }

4. Setze im ``void loop()`` den roten Pin der RGB-LED auf ``HIGH`` und die anderen beiden Pins auf ``LOW``.

.. note::

    Da wir PWM-Pins 9, 10 und 11 verwenden, hast du die Möglichkeit, entweder ``digitalWrite()`` oder ``analogWrite()`` zu verwenden, um ein hohes oder niedriges Signal auszugeben.
    
    In dieser Lektion setzen wir die Pins einfach auf hoch oder niedrig, daher verwenden wir ``digitalWrite()``.

.. code-block:: Arduino
    :emphasize-lines: 10-12

    void setup() {
        // Füge hier deinen Setup-Code ein, der einmal ausgeführt wird:
        pinMode(bluePin, OUTPUT);   // Setze den blauen Pin der RGB-LED auf Ausgang
        pinMode(greenPin, OUTPUT);  // Setze den grünen Pin der RGB-LED auf Ausgang
        pinMode(redPin, OUTPUT);  // Setze den roten Pin der RGB-LED auf Ausgang
    }

    void loop() {
        // Füge hier deinen Hauptcode ein, der wiederholt ausgeführt wird:
        digitalWrite(bluePin, LOW);    // Schalte den blauen Pin der RGB-LED aus
        digitalWrite(greenPin, LOW);   // Schalte den grünen Pin der RGB-LED aus
        digitalWrite(redPin, HIGH);  // Schalte den roten Pin der RGB-LED ein
    }

5. Speichere den Code und klicke auf „Hochladen“, um ihn an dein Arduino Uno R3 zu senden. Schau dir das Ergebnis an.

6. Du wirst sehen, dass die RGB-LED rot aufleuchtet. Aber was, wenn du auch grün und blau zum Leuchten bringen möchtest? Wie solltest du den Code ändern?

Kopiere die drei ``digitalWrite()``-Befehle zweimal und setze den Pin, den du anzeigen möchtest, auf ``HIGH``, während die anderen auf ``LOW`` gesetzt werden. Jede Farbe sollte für eine Sekunde leuchten.

.. code-block:: Arduino
    :emphasize-lines: 17-25

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // Füge hier deinen Setup-Code ein, der einmal ausgeführt wird:
        pinMode(bluePin, OUTPUT);   // Setze den blauen Pin der RGB-LED auf Ausgang
        pinMode(greenPin, OUTPUT);  // Setze den grünen Pin der RGB-LED auf Ausgang
        pinMode(redPin, OUTPUT);  // Setze den roten Pin der RGB-LED auf Ausgang
    }

    void loop() {
        // Füge hier deinen Hauptcode ein, der wiederholt ausgeführt wird:
        digitalWrite(bluePin, LOW);    // Schalte den blauen Pin der RGB-LED aus
        digitalWrite(greenPin, LOW);   // Schalte den grünen Pin der RGB-LED aus
        digitalWrite(redPin, HIGH);  // Schalte den roten Pin der RGB-LED ein
        delay(1000);              // Warte 1 Sekunde
        digitalWrite(bluePin, LOW);    // Schalte den blauen Pin der RGB-LED aus
        digitalWrite(greenPin, HIGH);  // Schalte den grünen Pin der RGB-LED ein
        digitalWrite(redPin, LOW);   // Schalte den roten Pin der RGB-LED aus
        delay(1000);              // Warte 1 Sekunde
        digitalWrite(bluePin, HIGH);   // Schalte den blauen Pin der RGB-LED ein
        digitalWrite(greenPin, LOW);   // Schalte den grünen Pin der RGB-LED aus
        digitalWrite(redPin, LOW);   // Schalte den roten Pin der RGB-LED aus
        delay(1000);              // Warte 1 Sekunde
    }

7. Lade den Code erneut hoch, um die Effekte zu sehen. Du wirst feststellen, dass die RGB-LED zwischen Rot, Grün und Blau wechselt.

**Fragen**:

1. Wenn du andere Farben erzeugen möchtest, was solltest du tun? Siehe dir das Diagramm unten an und fülle deine Ideen in deinem Handbuch aus.

.. image:: img/12_rgb_mix.png
    :width: 300
    :align: center

.. list-table::
   :widths: 20 20 20 20
   :header-rows: 1

   * - Farbe
     - Roter Pin
     - Grüner Pin
     - Blauer Pin
   * - Rot
     - *HIGH*
     - *LOW*
     - *LOW*
   * - Grün
     - *LOW*
     - *HIGH*
     - *LOW*
   * - Blau
     - *LOW*
     - *LOW*
     - *HIGH*
   * - Gelb
     -
     -
     -
   * - Pink
     -
     -
     -
   * - Cyan
     - 
     -
     -
   * - Weiß
     -
     -
     -

Codeerstellung - Farben anzeigen
------------------------------------

Auf unserem Weg, die Kontrolle über RGB-LEDs zu meistern, haben wir gesehen, wie wir mit ``digitalWrite()`` die LED in Grundfarben leuchten lassen können. Um das volle Farbspektrum, das eine RGB-LED erzeugen kann, zu erkunden, werden wir nun ``analogWrite()`` verwenden, um PWM-Signale (Pulsweitenmodulation) zu senden und so eine Vielzahl von Farbtönen zu erzeugen.

Schauen wir uns an, wie wir dies im Code umsetzen können.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du im Menü „Datei“ „Neues Sketch“ auswählst.
2. Speichere dein Sketch als ``Lesson11_PWM_Color_Mixing`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Erstelle drei Variablen, um die drei Pins der RGB-LED zu speichern und setze sie auf OUTPUT.

.. code-block:: Arduino

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(bluePin, OUTPUT);   // Setze den blauen Pin der RGB-LED auf Ausgang
        pinMode(greenPin, OUTPUT);  // Setze den grünen Pin der RGB-LED auf Ausgang
        pinMode(redPin, OUTPUT);  // Setze den roten Pin der RGB-LED auf Ausgang
    }

4. Verwende ``analogWrite()``, um PWM-Werte an die RGB-LED zu senden. Aus Lektion 9 wissen wir, dass PWM-Werte die Helligkeit einer LED ändern können, und der PWM-Bereich liegt zwischen 0-255. Um Rot anzuzeigen, setzen wir den PWM-Wert des roten Pins der RGB-LED auf 255 und die anderen beiden Pins auf 0.

.. code-block:: Arduino
    :emphasize-lines: 14-16

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(bluePin, OUTPUT);   // Setze den blauen Pin der RGB-LED auf Ausgang
        pinMode(greenPin, OUTPUT);  // Setze den grünen Pin der RGB-LED auf Ausgang
        pinMode(redPin, OUTPUT);  // Setze den roten Pin der RGB-LED auf Ausgang
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        analogWrite(bluePin, 0);    // Setze den PWM-Wert des blauen Pins auf 0
        analogWrite(greenPin, 0);   // Setze den PWM-Wert des grünen Pins auf 0
        analogWrite(redPin, 255);  // Setze den PWM-Wert des roten Pins auf 255
    }

5. Mit dieser Konfiguration wird nach dem Hochladen des Codes auf das Arduino Uno R3 die RGB-LED rot leuchten.

6. Die Funktion ``analogWrite()`` ermöglicht es der RGB-LED, nicht nur die sieben Grundfarben anzuzeigen, sondern auch viele andere verschiedene Farbtöne. Nun kannst du die Werte der Pins 9, 10 und 11 einzeln anpassen und die beobachteten Farben in deinem Handbuch notieren.

.. list-table::
    :widths: 20 20 20 40
    :header-rows: 1

    *   - Roter Pin    
        - Grüner Pin  
        - Blauer Pin
        - Farbe
    *   - 0
        - 128
        - 128
        - 
    *   - 128
        - 0
        - 255
        - 
    *   - 128
        - 128
        - 255
        - 
    *   - 255
        - 128
        - 0
        -     

Codeerstellung - Parametrisierte Funktionen
------------------------------------------------

Die Verwendung der ``analogWrite()``-Funktion zur Anzeige verschiedener Farben kann den Code lang und unübersichtlich machen, wenn du viele Farben gleichzeitig anzeigen möchtest. Daher müssen wir Funktionen erstellen.

Im Gegensatz zur vorherigen Lektion bereiten wir uns darauf vor, eine Funktion mit Parametern zu erstellen.

Eine parametrisierte Funktion ermöglicht es dir, spezifische Werte an die Funktion zu übergeben, die dann diese Werte verwendet, um ihre Aufgaben auszuführen. Dies ist äußerst nützlich, um Eigenschaften wie die Farbintensität dynamisch anzupassen. Es macht deinen Code flexibler und leichter lesbar.

Beim Definieren einer parametrisierten Funktion gibst du an, welche Werte sie benötigt, um zu arbeiten, indem du die Parameter in Klammern direkt nach dem Funktionsnamen auflistest. Diese Parameter fungieren als Platzhalter, die durch tatsächliche Werte ersetzt werden, wenn die Funktion aufgerufen wird.

So definierst du eine parametrisierte Funktion, um die Farbe einer RGB-LED einzustellen:

1. Öffne das zuvor gespeicherte Sketch ``Lesson11_PWM_Color_Mixing``. Klicke auf „Speichern unter...“ im Menü „Datei“ und benenne es in ``Lesson11_PWM_Color_Mixing_Function`` um. Klicke auf "Speichern".

2. Beginne damit, die Funktion nach dem ``void loop()`` mit dem Schlüsselwort ``void``, gefolgt vom Funktionsnamen und den Parametern in Klammern, zu deklarieren. Für unsere ``setColor``-Funktion verwenden wir drei Parameter – ``red``, ``green`` und ``blue`` –, die jeweils die Intensität der entsprechenden Farbkomponente der RGB-LED darstellen.

.. code-block:: Arduino
    :emphasize-lines: 5,6

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
    }

    void setColor(int red, int green, int blue) {
    }

   
3. Im Funktionskörper verwenden wir den Befehl ``analogWrite()``, um PWM-Signale an die Pins der RGB-LED zu senden. Die an ``setColor`` übergebenen Werte bestimmen die Helligkeit jeder Farbe. Die Parameter ``red``, ``green`` und ``blue`` werden hier direkt verwendet, um die Intensität jedes LED-Pins zu steuern.

.. code-block:: Arduino

    // Funktion zur Einstellung der Farbe der RGB-LED
    void setColor(int red, int green, int blue) {
        // PWM-Wert für rot, grün und blau an die RGB-LED senden
        analogWrite(redPin, red);
        analogWrite(greenPin, green);
        analogWrite(bluePin, blue);
    }

4. Nun kannst du die neu erstellte ``setColor()``-Funktion im ``void loop()`` aufrufen. Da du eine Funktion mit Parametern erstellt hast, musst du die Argumente in die Klammern ``()`` einfügen, z. B. ``(255, 0, 0)``. Vergiss nicht, Kommentare hinzuzufügen.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        setColor(255, 0, 0); // Anzeige der Farbe Rot
    }

    // Funktion zur Einstellung der Farbe der RGB-LED
    void setColor(int red, int green, int blue) {
        // PWM-Wert für rot, grün und blau an die RGB-LED senden
        analogWrite(redPin, red);
        analogWrite(greenPin, green);
        analogWrite(bluePin, blue);
    }

5. Wir wissen bereits, dass wir durch die Angabe verschiedener Werte für die drei Pins der RGB-LED unterschiedliche Farben erzeugen können. Aber wie können wir die RGB-LED genau in der gewünschten Farbe zum Leuchten bringen? Dafür benötigen wir eine Farbpalette. Öffne **Paint** (diese Software ist in Windows enthalten) oder eine beliebige Zeichenanwendung auf deinem Computer.

.. image:: img/13_mix_color_paint.png

6. Wähle eine Farbe aus, die dir gefällt, und notiere ihre RGB-Werte.

.. note::

    Beachte, dass du vor der Farbauswahl die Helligkeit auf die gewünschte Position einstellen solltest.

.. image:: img/13_mix_color_paint_2.png

7. Füge die ausgewählte Farbe in die ``setColor()``-Funktion im ``void loop()`` ein und verwende die ``delay()``-Funktion, um die Anzeigedauer jeder Farbe festzulegen.

.. code-block:: Arduino

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        setColor(255, 0, 0);      // Anzeige der Farbe Rot
        delay(1000);              // Warte 1 Sekunde
        setColor(0, 128, 128);    // Anzeige der Farbe Türkis
        delay(1000);              // Warte 1 Sekunde
        setColor(128, 0, 255);    // Anzeige der Farbe Lila
        delay(1000);              // Warte 1 Sekunde
        setColor(128, 128, 255);  // Anzeige der Farbe Hellblau
        delay(1000);              // Warte 1 Sekunde
        setColor(255, 128, 0);    // Anzeige der Farbe Orange
        delay(1000);              // Warte 1 Sekunde
    }

8. Unten findest du den vollständigen Code; du kannst auf "Hochladen" klicken, um den Code auf das Arduino Uno R3 hochzuladen und die Effekte zu sehen.

.. code-block:: Arduino

    const int redPin = 11;
    const int greenPin = 10;
    const int bluePin = 9;

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(bluePin, OUTPUT);   // Setze den blauen Pin der RGB-LED auf Ausgang
        pinMode(greenPin, OUTPUT);  // Setze den grünen Pin der RGB-LED auf Ausgang
        pinMode(redPin, OUTPUT);  // Setze den roten Pin der RGB-LED auf Ausgang
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        setColor(255, 0, 0);      // Anzeige der Farbe Rot
        delay(1000);              // Warte 1 Sekunde
        setColor(0, 128, 128);    // Anzeige der Farbe Türkis
        delay(1000);              // Warte 1 Sekunde
        setColor(128, 0, 255);    // Anzeige der Farbe Lila
        delay(1000);              // Warte 1 Sekunde
        setColor(128, 128, 255);  // Anzeige der Farbe Hellblau
        delay(1000);              // Warte 1 Sekunde
        setColor(255, 128, 0);    // Anzeige der Farbe Orange
        delay(1000);              // Warte 1 Sekunde
    }

    // Funktion zur Einstellung der Farbe der RGB-LED
    void setColor(int red, int green, int blue) {
        // PWM-Wert für rot, grün und blau an die RGB-LED senden
        analogWrite(redPin, red);
        analogWrite(greenPin, green);
        analogWrite(bluePin, blue);
    }

9. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Zusammenfassung**

Durch eine Reihe von Codierübungen wirst du Sketche schreiben, die die Farbe der RGB-LED dynamisch ändern. Beginnend mit einfachen Befehlen zur Steuerung jeder Farbe wirst du dann deinen Code refaktorisieren, um Funktionen zu verwenden, wodurch dein Setup modularer und wartungsfreundlicher wird. Dieser Ansatz macht den Code nicht nur sauberer, sondern vermittelt dir auch die Bedeutung von Funktionen in der Programmierung.


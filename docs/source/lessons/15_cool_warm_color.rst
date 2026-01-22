.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 zusammen mit Gleichgesinnten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte vorab Informationen über neue Produktankündigungen und Einblicke.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und Sonderaktionen teil.

    👉 Bereit, mit uns zu erkunden und zu kreieren? Klicke auf [|link_sf_facebook|] und trete noch heute bei!

15. Kühle oder warme Farben
================================

Farben sind nicht nur ein Teil unserer visuellen Erfahrung – sie beeinflussen auch unsere Emotionen und Gefühle. In dieser Lektion tauchen wir in die psychologischen Auswirkungen von Farben ein und lernen, wie man eine RGB-LED verwendet, um zwischen warmen und kühlen Farben zu wechseln und so die Effekte wechselnder Lichttemperaturen zu simulieren.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/15_cool_warm_color.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>


**Überblick**

Das Konzept von kühlen und warmen Farben bezieht sich auf die psychologischen Effekte, die Farben auf unsere Wahrnehmung haben. Rottöne, Orangetöne, Gelb- und Brauntöne lösen typischerweise Gefühle von Wärme und Aufregung aus und werden als warme Farben klassifiziert. Im Gegensatz dazu vermitteln Grüntöne, Blautöne und Violetttöne oft beruhigende, erfrischende und großzügige Gefühle und gelten als kühle Farben. Orange und Blau befinden sich an den entgegengesetzten Enden dieses warm-kalt-Spektrums.

.. image:: img/15_mix_color_warm_cool.png
    :width: 400
    :align: center

Zu Hause oder in Freizeitumgebungen bevorzugen Menschen Beleuchtung in hellgelben oder cremeweißen Tönen, die eine gemütliche Atmosphäre schaffen, ähnlich wie bei Sonnenuntergang oder Kerzenlicht.

.. image:: img/15_mix_color_warm_room.png
    :width: 400
    :align: center

In Bibliotheken, Klassenzimmern, Büros und Krankenhäusern werden kühlere Lichttöne bevorzugt, da sie die Konzentration und Frische fördern, die für das Arbeiten und Lernen förderlich sind.

.. image:: img/15_mix_color_cool_room.png
    :width: 400
    :align: center

Die Wärme oder Kühle des Lichts ist eine unmittelbare Erfahrung, die unsere psychologische Reaktion und unseren visuellen Komfort beeinflusst. Designer und Lichtingenieure wählen sorgfältig die Farbtemperaturen aus, die zur Funktion eines Raums und zur gewünschten Atmosphäre passen, um sowohl ästhetisch ansprechende als auch praktische Lichtumgebungen zu schaffen. Durch die wissenschaftliche Anwendung dieser Prinzipien können wir die Qualität unserer Lebens- und Arbeitsräume verbessern und so eine gesündere und angenehmere Atmosphäre schaffen.

In dieser Lektion schlüpfen wir in die Rolle von Lichtingenieuren, um ein Beleuchtungssystem zu erstellen, das zwischen Farbtemperaturen wechseln kann.

**Lernziele**

- Verstehen der psychologischen Effekte von kühlen und warmen Farben.
- Erforschen, wie Lichttemperaturen Stimmung und Ambiente beeinflussen.
- Erlernen, wie RGB-LEDs verwendet werden, um verschiedene Farbtemperaturen mit Arduino zu simulieren.
- Entwickeln praktischer Fähigkeiten im Umgang mit der ``map()``-Funktion, um zwischen Farbtemperaturen zu wechseln.


Den Schaltkreis aufbauen
------------------------------------

**Benötigte Komponenten**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB-LED
     - 3 * 220Ω Widerstand
     - 1 * Potentiometer
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - Steckbrücken
     -
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     -

     
**Bauanleitung**

Dieser Schaltkreis baut auf dem aus Lektion 12 auf, indem ein Potentiometer hinzugefügt wird.

.. image:: img/15_cool_warm_color.png
    :width: 500
    :align: center

1. Entferne das Steckbrückenkabel, das den GND-Pin des Arduino Uno R3 mit dem GND-Pin der RGB-LED verbindet, und stecke es in den Minuspol des Steckbretts. Verbinde dann ein weiteres Steckbrückenkabel vom Minuspol des Steckbretts mit dem GND-Pin der RGB-LED.

.. image:: img/15_cool_warm_color_gnd.png
    :width: 500
    :align: center

2. Setze das Potentiometer in die Löcher 25G, 26F und 27G ein.

.. image:: img/15_cool_warm_color_pot.png
    :width: 500
    :align: center

3. Verbinde den mittleren Pin des Potentiometers mit dem A0-Pin des Arduino Uno R3.

.. image:: img/15_cool_warm_color_a0.png
    :width: 500
    :align: center

4. Schließe schließlich den linken Pin des Potentiometers an den 5V-Pin des Arduino Uno R3 und den rechten Pin an den Minuspol des Steckbretts an.

.. image:: img/15_cool_warm_color.png
    :width: 500
    :align: center



Code-Erstellung
---------------------

**Verständnis von warmen und kühlen Farben**

Bevor wir die Farbtemperatur anpassen, müssen wir die Unterschiede zwischen den RGB-Werten für kühle und warme Farben verstehen.

Die Wahrnehmung von Wärme bei der Beleuchtung ist etwas subjektiv, aber unbestritten sollten warme Farben eher in Richtung Orange-Rot und kühle Farben eher in Richtung Blau tendieren.

1. Öffne **Paint** oder ein beliebiges Farb-Auswahl-Tool, finde die Farben, die du als am wärmsten und am kühlsten empfindest, und notiere deren RGB-Werte in deinem Notizbuch.

.. note::

    Beachte, dass du vor der Auswahl einer Farbe die Lumenzahl auf die richtige Position einstellst.

.. list-table::
   :widths: 25 25 50 25
   :header-rows: 1

   * - Farbtyp
     - Rot
     - Grün
     - Blau
   * - Warme Farbe
     -
     -
     -
   * - Kühle Farbe
     -
     -
     -

2. Hier sind Beispiele für warme und kühle Töne sowie deren RGB-Werte:

* Rot (Rot: 246, Grün: 52, Blau: 8)

.. image:: img/15_mix_color_tone_warm.png

* Hellblau (Rot: 100, Grün: 150, Blau: 255)

.. image:: img/15_mix_color_tone_cool.png

Der Hauptunterschied zwischen warmen und kühlen Farben liegt im Verhältnis der Intensitäten der drei Primärfarben. Als nächstes speichern wir diese warmen und kühlen RGB-Werte in unserem Sketch.

3. Öffne den zuvor gespeicherten Sketch ``Lesson11_PWM_Color_Mixing``. Wähle „Speichern unter...“ aus dem „Datei“-Menü und benenne ihn in ``Lesson15_Cool_Warm_Color`` um. Klicke auf „Speichern“.

4. Deklariere vor dem ``void setup()`` sechs Variablen, um die RGB-Werte dieser beiden Farben zu speichern. Verwende die Farben, die du ausgewählt hast.

.. code-block:: Arduino
    :emphasize-lines: 1-4,6-9

    // RGB-Werte für eine warme Farbe
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // RGB-Werte für eine kühle Farbe
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);   // Setze den Blau-Pin der RGB-LED als Ausgang
        pinMode(10, OUTPUT);  // Setze den Grün-Pin der RGB-LED als Ausgang
        pinMode(11, OUTPUT);  // Setze den Rot-Pin der RGB-LED als Ausgang
    }

**Verwendung der map() Funktion**

Um von warmer zu kühler Beleuchtung zu wechseln, musst du lediglich die Intensität des roten Lichts reduzieren, das blaue Licht erhöhen und die Intensität des grünen Lichts feinjustieren.

In früheren Projekten haben wir gelernt, wie man die Helligkeit einer LED in Abhängigkeit von der Drehung eines Potentiometers variiert.

In diesem Projekt bewirkt die Drehung des Potentiometers jedoch, dass sich die Intensitäten der RGB-Pins innerhalb eines bestimmten Bereichs ändern, wodurch einfache Division nicht ausreicht. Daher benötigen wir die neue Funktion ``map()``.

In der Arduino-Programmierung ist die ``map()``-Funktion äußerst nützlich, da sie es ermöglicht, einen numerischen Bereich in einen anderen umzuwandeln.

So verwendest du sie:

* ``map(value, fromLow, fromHigh, toLow, toHigh)``: Ordnet eine Zahl einem anderen Bereich zu. Das bedeutet, dass ein Wert von ``fromLow`` zu ``toLow`` wird, ein Wert von ``fromHigh`` zu ``toHigh``, Zwischenwerte werden proportional skaliert, etc.

    **Parameter**
        * ``value``: Die Zahl, die umgerechnet werden soll.
        * ``fromLow``: Untere Grenze des aktuellen Bereichs.
        * ``fromHigh``: Obere Grenze des aktuellen Bereichs.
        * ``toLow``: Untere Grenze des Zielbereichs.
        * ``toHigh``: Obere Grenze des Zielbereichs.

    **Rückgabewert**
        Der umgerechnete Wert. Datentyp: long.

Die ``map()``-Funktion skaliert einen Wert von seinem ursprünglichen Bereich (fromLow bis fromHigh) in einen neuen Bereich (toLow bis toHigh). Zuerst berechnet sie die Position des ``value`` innerhalb seines ursprünglichen Bereichs und wendet dann dieselbe Proportion an, um diese Position in den neuen Bereich zu skalieren.

.. image:: img/15_map_pic.png
    :width: 400
    :align: center

Dies kann als Formel wie unten gezeigt geschrieben werden:

.. code-block::

    (value-fromLow)/(fromHigh-fromLow) = (y-toLow)/(toHigh-toLow)

Unter Verwendung der Algebra kannst du diese Gleichung umstellen, um ``y`` zu berechnen:

.. code-block::

    y = (value-fromLow) * (toHigh-toLow) / (fromHigh-fromLow) + toLow

.. image:: img/15_map_format.png

Zum Beispiel unter Verwendung von ``y = map(value, 0, 1023, 246, 100);``, wenn ``value`` 434 beträgt, dann ``y = (434-0) * (100 - 246) / (1023-0) + 246``, was ungefähr 152 ergibt.


5. Entferne den ursprünglichen Code in ``void loop()``, und schreibe dann den Code, um den Wert des Potentiometers zu lesen und ihn in der Variablen ``potValue`` zu speichern.

.. code-block:: Arduino

    void loop() {
        // Hauptschleife, die wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Lese den Wert vom Potentiometer
    }

6. Verwende dann die ``map()``-Funktion, um den Wert des Potentiometers von dem Bereich 0~1023 auf den Bereich 255 (``warm_r``) ~ 100 (``cool_r``) zu skalieren.

.. code-block:: Arduino

    void loop() {
        // Hauptschleife, die wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Lese den Wert vom Potentiometer
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappe den Potentiometer-Wert auf die Rot-Intensität
    }

7. Du kannst den seriellen Monitor verwenden, um den ``potValue`` und den gemappten Wert ``value_r`` anzuzeigen, um dein Verständnis der ``map()``-Funktion zu vertiefen. Starte jetzt den seriellen Monitor in ``void setup()``.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);   // Setze den Blau-Pin der RGB-LED als Ausgang
        pinMode(10, OUTPUT);  // Setze den Grün-Pin der RGB-LED als Ausgang
        pinMode(11, OUTPUT);  // Setze den Rot-Pin der RGB-LED als Ausgang
        Serial.begin(9600);        // Setze die serielle Kommunikation auf 9600 Baud ein
    }

8. Drucke die Variablen ``potValue`` und ``value_r`` in derselben Zeile, getrennt durch "|".

.. code-block:: Arduino
    :emphasize-lines: 23-26

    // RGB-Werte für eine warme Farbe
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // RGB-Werte für eine kühle Farbe
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);   // Setze den Blau-Pin der RGB-LED als Ausgang
        pinMode(10, OUTPUT);  // Setze den Grün-Pin der RGB-LED als Ausgang
        pinMode(11, OUTPUT);  // Setze den Rot-Pin der RGB-LED als Ausgang
        Serial.begin(9600);        // Setze die serielle Kommunikation auf 9600 Baud ein
    }

    void loop() {
        // Hauptschleife, die wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Lese den Wert vom Potentiometer
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappe den Potentiometer-Wert auf die Rot-Intensität
        Serial.print(potValue);
        Serial.print(" | ");
        Serial.println(value_r);
        delay(500);  // Warte 500 ms
    }

    // Funktion zum Setzen der Farbe der RGB-LED
    void setColor(int red, int green, int blue) {
        analogWrite(11, red);    // Schreibe PWM auf den Rot-Pin
        analogWrite(10, green);  // Schreibe PWM auf den Grün-Pin
        analogWrite(9, blue);    // Schreibe PWM auf den Blau-Pin
    }

9. Du kannst jetzt deinen Code verifizieren und hochladen, den seriellen Monitor öffnen, und du wirst sehen, dass zwei Spalten von Daten gedruckt werden.

.. code-block::

    434 | 152
    435 | 152
    434 | 152
    434 | 152
    434 | 152
    434 | 152

Anhand der Daten wird deutlich, dass die Position des Werts 434 im Bereich von 0~1023 der Position von 152 im Bereich von 246~100 entspricht.

**Anpassen der Farbtemperatur**

Hier verwenden wir die Funktion ``map()``, um die Intensität der drei Pins der RGB-LED mit der Drehung des Potentiometers zu verändern und dabei die wärmsten bis kältesten Farbtöne zu durchlaufen. 

Genauer gesagt, wie in dem Beispiel mit den Referenzwerten, die ich angegeben habe, ändert sich bei Drehung des Potentiometers der R-Wert der RGB-LED allmählich von 246 zu 100, der G-Wert von 8 zu 150 (obwohl die Änderung des G-Werts nicht sehr auffällig ist), und der B-Wert von 8 zu 255.

10. Wir benötigen vorübergehend keine serielle Ausgabe, und die serielle Ausgabe kann den gesamten Codeablauf beeinträchtigen. Verwende also ``Ctrl + /``, um den zugehörigen Code auszukommentieren.

    .. note::

        Der Grund, warum nicht direkt gelöscht wird, ist, dass wenn du später eine Ausgabe benötigst, du diese Zeilen einfach durch Drücken von ``Ctrl + /`` wieder einfügen kannst.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void loop() {
        // Hauptschleife, die wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Lese den Wert vom Potentiometer
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappe den Potentiometer-Wert auf die Rot-Intensität
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Warte 500 ms
    }

11. Führe die ``map()``-Funktion weiter aus, um die gemappten Werte ``value_g`` und ``value_b`` basierend auf dem Wert des Potentiometers zu erhalten.

.. code-block:: Arduino
    :emphasize-lines: 9,10

    void loop() {
        // Hauptschleife, die wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Lese den Wert vom Potentiometer
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappe den Potentiometer-Wert auf die Rot-Intensität
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Warte 500 ms
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Mappe den Potentiometer-Wert auf die Grün-Intensität
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Mappe den Potentiometer-Wert auf die Blau-Intensität
    }

12. Rufe schließlich die Funktion ``setColor()`` auf, um die gemappten RGB-Werte auf der RGB-LED anzuzeigen.

.. code-block:: Arduino
    :emphasize-lines: 11,12

    void loop() {
        // Hauptschleife, die wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Lese den Wert vom Potentiometer
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappe den Potentiometer-Wert auf die Rot-Intensität
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Warte 500 ms
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Mappe den Potentiometer-Wert auf die Grün-Intensität
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Mappe den Potentiometer-Wert auf die Blau-Intensität
        setColor(value_r, value_g, value_b);                   // Setze die LED-Farbe
        delay(500);
    }

13. Dein vollständiger Code sieht wie folgt aus; du kannst jetzt auf den Upload-Button klicken, um den Code auf das Arduino Uno R3 hochzuladen. Danach kannst du das Potentiometer drehen, und du wirst bemerken, wie die RGB-LED allmählich von einem kühlen zu einem warmen Farbton oder von einem warmen zu einem kühlen Farbton übergeht.

.. code-block:: Arduino

    // RGB-Werte für eine warme Farbe
    int warm_r = 246;
    int warm_g = 52;
    int warm_b = 8;

    // RGB-Werte für eine kühle Farbe
    int cool_r = 100;
    int cool_g = 150;
    int cool_b = 255;

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(9, OUTPUT);   // Setze den Blau-Pin der RGB-LED als Ausgang
        pinMode(10, OUTPUT);  // Setze den Grün-Pin der RGB-LED als Ausgang
        pinMode(11, OUTPUT);  // Setze den Rot-Pin der RGB-LED als Ausgang
    }

    void loop() {
        // Hauptschleife, die wiederholt ausgeführt wird:
        int potValue = analogRead(A0);                         // Lese den Wert vom Potentiometer
        int value_r = map(potValue, 0, 1023, warm_r, cool_r);  // Mappe den Potentiometer-Wert auf die Rot-Intensität
        // Serial.print(potValue);
        // Serial.print(" | ");
        // Serial.println(value_r);
        // delay(500);  // Warte 500 ms
        int value_g = map(potValue, 0, 1023, warm_g, cool_g);  // Mappe den Potentiometer-Wert auf die Grün-Intensität
        int value_b = map(potValue, 0, 1023, warm_b, cool_b);  // Mappe den Potentiometer-Wert auf die Blau-Intensität
        setColor(value_r, value_g, value_b);                   // Setze die LED-Farbe
        delay(500);                                            // Warte 500 ms
    }

    // Funktion zum Setzen der Farbe der RGB-LED
    void setColor(int red, int green, int blue) {
        analogWrite(11, red);    // Schreibe PWM auf den Rot-Pin
        analogWrite(10, green);  // Schreibe PWM auf den Grün-Pin
        analogWrite(9, blue);    // Schreibe PWM auf den Blau-Pin
    }

14. Speichere schließlich deinen Code und räume deinen Arbeitsplatz auf.

**Tipps**

Während des Experiments könntest du feststellen, dass der Wechsel zwischen warmen und kühlen Farbtönen nicht so deutlich ist, wie er auf dem Bildschirm erscheint. Zum Beispiel kann ein erwartetes warmes Licht weiß erscheinen. Dies ist normal, da die Farbmischung in einer RGB-LED nicht so fein abgestimmt ist wie auf einem Display.

In solchen Fällen kannst du die Intensität der G- und B-Werte in der warmen Farbe reduzieren, um die RGB-LED eine passendere Farbe anzeigen zu lassen.

**Frage**

Beachte, dass die „unteren Grenzen“ beider Bereiche größer oder kleiner als die „oberen Grenzen“ sein können, sodass die Funktion ``map(value, fromLow, fromHigh, toLow, toHigh)`` auch verwendet werden kann, um einen Zahlenbereich umzukehren, zum Beispiel:

.. code-block::

    y = map(x, 1, 50, 50, 1);

Die Funktion verarbeitet auch negative Zahlen gut, sodass dieses Beispiel ebenfalls gültig ist:

.. code-block::

    y = map(x, 1, 50, 50, -100);

Für ``y = map(x, 1, 50, 50, -100);``, wenn ``x`` 20 beträgt, was sollte ``y`` sein? Verwende die folgende Formel, um es zu berechnen.

.. image:: img/15_map_format.png

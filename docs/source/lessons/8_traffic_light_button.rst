.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein, zusammen mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Sneak Peeks.
    - **Sonderrabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu erkunden und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

8. Ampel mit Fußgängerknopf
===============================================

Willkommen zur nächsten Phase unserer Arduino-Reise. In der vorherigen Lektion haben wir ein grundlegendes Ampelsystem aufgebaut, das den Verkehr mit roten, gelben und grünen Lichtern steuert. Jetzt fügen wir eine Ebene der Interaktion hinzu, die die Komplexität der realen Welt widerspiegelt: einen Fußgängerknopf. Diese Funktion fügt eine menschliche Komponente zu unserer elektronischen Kreuzung hinzu, die eine dynamische Interaktion zwischen Gehwegen und Fahrbahnen an unseren belebten Kreuzungen ermöglicht.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/8_traffic_light_button.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In dieser Lektion lernst du:

* Verstehen, wie Taster funktionieren und welche Rolle sie in Schaltungen spielen.
* Den Einsatz von ``digitalRead()`` zur Erkennung von Pin-Eingangspegeln.
* Implementiere ``if``-Anweisungen, um bedingte Verhaltensweisen in Ampelsystemen zu schaffen.

Während wir in dieses Projekt eintauchen, erkunden wir nicht nur den technischen Aufbau, sondern auch die Logik und Programmierung, die solche Systeme ermöglichen und effizient den Fußgänger- und Fahrzeugverkehr steuern.

Schaltung aufbauen
-----------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Rote LED
     - 1 * Gelbe LED
     - 1 * Grüne LED
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_yellow_led| 
     - |list_green_led| 
   * - 1 * Taster
     - 1 * Steckbrett
     - 3 * 220Ω Widerstand
     - 1 * 10K Ohm Widerstand
   * - |list_button| 
     - |list_breadboard| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * USB-Kabel
     - Jumper-Kabel
     - 1 * Multimeter
     - 
   * - |list_usb_cable| 
     - |list_wire| 
     - |list_meter|
     - 


**Schritt-für-Schritt Aufbau**

Folge dem Verdrahtungsdiagramm oder den folgenden Schritten, um deine Schaltung aufzubauen.

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center  

1. Beginne mit der Ampelschaltung aus der vorherigen Lektion.

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

2. Finde einen Taster.

.. image:: img/8_traffic_button.png
    :width: 500
    :align: center

Taster sind allgegenwärtige Komponenten in der Elektronik und fungieren als Schalter, um Schaltungen zu schließen oder zu unterbrechen. Unten siehst du den inneren Aufbau eines Tasters und sein häufig verwendetes Symbol in Schaltplänen.

.. image:: img/8_traffic_button_symbol.png
    :width: 500
    :align: center

Obwohl Taster vier Pins haben, sind die Pins 1 und 2 sowie 3 und 4 miteinander verbunden. Durch Drücken des Tasters werden alle vier Pins verbunden, wodurch die Schaltung geschlossen wird.

3. Setze den Taster in das Steckbrett über die mittlere Kerbe ein, wobei die Pins in den Löchern 18e, 18f, 20e und 20f sitzen.

.. note::

    Wenn du unsicher bist, wie der Taster eingesetzt werden soll, probiere beide Ausrichtungen aus. In einer Richtung wird der Pinabstand leicht zu schmal sein, um zu passen.

.. image:: img/8_traffic_light_button_button.png
    :width: 600
    :align: center

4. Verbinde den rechten oberen Pin des Tasters mit dem digitalen Pin 8 des Arduino Uno R3 mit einem langen Jumper-Kabel. Stecke ein Ende in Loch 18j und das andere Ende in Pin 8.

.. image:: img/8_traffic_light_button_pin8.png
    :width: 600
    :align: center

5. Platziere einen 10K Ohm Widerstand zwischen dem linken oberen Pin des Tasters und dem Ground. Verbinde ein Ende mit Loch 18a und das andere mit der negativen Schiene des Steckbretts. Dieser Widerstand zieht Pin 8 auf Ground herunter und stabilisiert ihn auf LOW, wenn der Taster nicht gedrückt wird.

    .. image:: img/8_traffic_light_button_10k.png
        :width: 600
        :align: center

Pin 8 dient als Eingang, um den Zustand des Tasters zu lesen. Arduino-Boards lesen Spannungen zwischen 0 und etwa 5 Volt an den Eingangspins und interpretieren sie je nach Schwellenwert als LOW oder HIGH. Damit ein Pin als HIGH gelesen wird, muss er mehr als 3 Volt haben. Um als LOW gelesen zu werden, muss er weniger als 1,5 Volt haben.

Ohne den 10K-Widerstand würde Pin 8 nur mit dem Taster verbunden sein und zwischen 0 und 5V schwanken, wodurch sein Zustand zufällig zwischen HIGH und LOW wechseln würde.

Der 10K-Widerstand, der Pin 8 mit Ground verbindet, zieht die Spannung des Pins auf Ground herunter, was sicherstellt, dass er als LOW gelesen wird, wenn der Taster nicht gedrückt ist.

6. Schließlich versorge den Taster mit Strom, indem du die positive Schiene des Steckbretts mit dem 5V-Pin des Arduino Uno R3 verbindest, und zwar mit einem roten Stromkabel.

.. image:: img/8_traffic_light_button.png
    :width: 600
    :align: center


**Frage:**

Deine Ampel ist eine Mischung aus Serien- und Parallelschaltungen. Diskutiere, welche Teile deiner Schaltung in Serie sind und warum. Erkläre dann, welche Teile parallel sind und warum.


Codeerstellung
-------------------

**Pins initialisieren**

Bisher hast du die Ampeln so programmiert, dass die grünen, gelben und roten LEDs nacheinander aufleuchten. In dieser Lektion wirst du deinen Fußgängerknopf so programmieren, dass beim Drücken die roten und gelben LEDs ausgehen, während die grüne LED blinkt, um anzuzeigen, dass es für Fußgänger sicher ist, die Straße zu überqueren.

1. Öffne den zuvor gespeicherten Sketch, ``Lesson7_Traffic_Light``. Wähle „Speichern unter...“ aus dem Menü „Datei“ und benenne ihn in ``Lesson8_Traffic_Light_Button`` um. Klicke auf "Speichern".

2. Füge in der Funktion ``void setup()`` einen weiteren ``pinMode()``-Befehl hinzu, um Pin 8 als Eingang (``INPUT``) zu deklarieren. Füge dann einen Codekommentar hinzu, um deinen neuen Befehl zu erklären.

.. code-block:: Arduino
    :emphasize-lines: 6

    void setup() {
        // Setup-Code hier, der einmal ausgeführt wird:
        pinMode(3, OUTPUT); // Setze Pin 3 auf Ausgang
        pinMode(4, OUTPUT); // Setze Pin 4 auf Ausgang
        pinMode(5, OUTPUT); // Setze Pin 5 auf Ausgang
        pinMode(8, INPUT);  // Deklariere Pin 8 (Taster) als Eingang
    }
    
    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        digitalWrite(3, HIGH);  // Schalte die LED an Pin 3 ein
        digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
        digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
        delay(10000);           // Warte 10 Sekunden
        digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
        digitalWrite(4, HIGH);  // Schalte die LED an Pin 4 ein
        digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
        delay(3000);            // Warte 3 Sekunden
        digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
        digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
        digitalWrite(5, HIGH);  // Schalte die LED an Pin 5 ein
        delay(10000);           // Warte 10 Sekunden
    }

3. Nachdem du den Code geschrieben hast, überprüfe deinen Sketch und lade den Code auf den Arduino Uno R3 hoch.

**Messen der Spannung an Pin 8**

Aus der vorherigen Lektion wissen wir bereits, wie der LED-Abschnitt unserer Schaltung funktioniert. Jede LED, die als Ausgang fungiert, wird von verschiedenen Pins auf dem Arduino Uno R3 gesteuert.

Der an Pin 8 angeschlossene Taster ist jedoch anders. Er ist ein Eingabegerät. Pin 8 liest die eingehende Spannung, anstatt Spannung auszugeben.

Lass uns ein Multimeter verwenden, um die Spannung an Pin 8 zu testen, wenn der Taster gedrückt und losgelassen wird. Du benötigst möglicherweise die Hilfe eines Freundes, um den Taster während dieser Messung zu drücken.

1. Stelle das Multimeter auf den Gleichspannungsbereich von 20 Volt ein.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Wenn der Taster nicht gedrückt ist, miss die Spannung an Pin 8. Berühre die rote Messleitung des Multimeters an Pin 8 und die schwarze Messleitung an GND.

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

3. Trage die gemessene Spannung in die Tabelle ein.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Zustand des Tasters
     - Spannung an Pin 8
     - Zustand
   * - Losgelassen
     - *0,00 Volt*
     - 
   * - Gedrückt
     -
     - 

4. Lass dir von deinem Freund helfen, den Taster zu drücken, und fahre fort, die Spannung an Pin 8 zu messen.

.. image:: img/8_traffic_voltage.png
    :width: 600
    :align: center

5. Wenn der Taster gedrückt ist, trage die Spannung an Pin 8 in die Tabelle ein.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Zustand des Tasters
     - Spannung an Pin 8
     - Zustand
   * - Losgelassen
     - *0,00 Volt*
     - 
   * - Gedrückt
     - *≈4,97 Volt*
     - 

6. Arduino-Boards lesen Spannungen zwischen 0 und ungefähr 5 Volt an den Eingangspins und interpretieren sie als entweder ``LOW`` oder ``HIGH``, basierend auf einer Schwellenwertspannung. Damit ein Pin als ``HIGH`` gelesen wird, muss er über 3 Volt haben. Um als ``LOW`` gelesen zu werden, muss er weniger als 1,5 Volt haben.

   Basierend auf der gemessenen Spannung fülle den Zustand für Pin 8 aus.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Zustand des Tasters
     - Spannung an Pin 8
     - Zustand Pin 8
   * - Losgelassen
     - *0,00 Volt*
     - *LOW*
   * - Gedrückt
     - *≈4,97 Volt*
     - *HIGH*


**Bedingte Anweisungen**

Die Ampel sollte zwei verschiedene Verhaltensweisen zeigen, je nachdem, ob der Taster gedrückt wird oder nicht:

* Wenn der Taster gedrückt wird, sollte der Code für die Fußgängerampel ausgeführt werden, und die grüne LED sollte blinken.
* Wenn der Taster nicht gedrückt wird, sollte die Ampel normal funktionieren, wie du es programmiert hast.

Um diese Verhaltensweisen zu programmieren, wirst du eine neue Programmierfunktion namens bedingte Anweisungen verwenden.

Bedingte Anweisungen werden manchmal als ``if-then``-Anweisungen bezeichnet oder einfach als ``if``-Anweisungen.
Bedingte Anweisungen ermöglichen es dir, bestimmte Codezeilen auszuführen, wenn eine bestimmte Bedingung oder ein Szenario wahr ist.

.. image:: img/if.png
    :width: 300
    :align: center

.. note::

    Du verwendest bedingte Anweisungen oft im Alltag, um Entscheidungen zu treffen, wie zum Beispiel:

    .. code-block:: Arduino

        start;
        if kalt;
        dann zieh einen Mantel an;
        end;
        
Im Arduino-IDE sieht eine bedingte Anweisung so aus:

    .. code-block:: Arduino

        if (Bedingung) {
            Befehle, die ausgeführt werden, wenn die Bedingung wahr ist 
        }

Die ``condition`` steht in Klammern und verwendet Vergleichsoperatoren, um zwei oder mehr Werte zu vergleichen. Diese Werte können Zahlen, Variablen oder Eingaben sein, die in den Arduino Uno R3 gelangen.

Hier ist eine Liste von Vergleichsoperatoren und deren Verwendung im Bedingungsteil einer if-Anweisung:

.. list-table::
    :widths: 20 20 60
    :header-rows: 1

    *   - Comparison Operator
        - Meaning
        - Example
    *   - ==
        - Equals
        - if (digitalRead(8) == HIGH) {do something}
    *   - !=
        - Not equal
        - if (digitalRead(5) != LOW) {do something}
    *   - <
        - Less than
        - if (distance < 100) {do something}
    *   - >
        - Greater than
        - if (count > 5) {do something}
    *   - <=
        - Less than or equal to
        - if (number <= minValue) {do something}
    *   - >=
        - Greater than or equal to
        - if (number >= maxValue) {do something}

.. note::

    Der Vergleich von Gleichheit erfolgt mit zwei Gleichheitszeichen (``==``). Ein einzelnes Gleichheitszeichen (``=``) wird verwendet, um einer Variablen einen Wert zuzuweisen (dies wird in späteren Abschnitten erklärt), während zwei Gleichheitszeichen zum Vergleich von zwei Werten verwendet werden.

Beim Vergleich zweier Werte in einer Bedingung kann das Ergebnis ``True`` oder ``False`` sein. Wenn die Bedingung ``True`` ist, werden die Befehle innerhalb der geschweiften Klammern ausgeführt. Wenn die Bedingung ``False`` ist, werden die Befehle innerhalb der geschweiften Klammern übersprungen.

In der Programmierung können bedingte Anweisungen einfach oder komplex sein, wobei mehrere Bedingungen und Szenarien berücksichtigt werden. Im nächsten Schritt werden wir die grundlegende Form von ``if``-Anweisungen verwenden.

**Taster nicht gedrückt**

Aufbauend auf unserem Verständnis von bedingten Anweisungen wenden wir dieses Konzept an, um unseren Ampelsketch zu verbessern. Da das Drücken eines Tasters den Verkehrsfluss verändert, fügen wir eine Bedingung hinzu, um den Zustand des Tasters zu überwachen.

1. Aus unseren früheren Messungen der Spannung an Pin 8 wissen wir, dass wenn der Taster nicht gedrückt ist, Pin 8 auf ``LOW`` steht. Wenn also der Zustand von Pin 8 als ``LOW`` gelesen wird, bedeutet das, dass der Taster nicht gedrückt ist. Füge nun am Anfang der ``void loop()``-Funktion in deinem vorherigen Code die folgende Anweisung ein:

    .. code-block:: Arduino
        :emphasize-lines: 11,13

        void setup() {
            // Setup-Code, der einmal ausgeführt wird:
            pinMode(3, OUTPUT); // Setze Pin 3 als Ausgang
            pinMode(4, OUTPUT); // Setze Pin 4 als Ausgang
            pinMode(5, OUTPUT); // Setze Pin 5 als Ausgang
            pinMode(8, INPUT);  // Deklariere Pin 8 (Taster) als Eingang
        }

        void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            if (digitalRead(8) == LOW) {
                
            }

            digitalWrite(3, HIGH);  // Schalte die LED an Pin 3 ein
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus

            ...

Genauso wie der Befehl ``digitalWrite()`` für Ausgangspins verwendet wird, wird der Befehl ``digitalRead()`` für Eingangspins verwendet. ``digitalRead(pin)`` ist der Befehl, um zu lesen, ob ein digitaler Pin auf ``HIGH`` oder ``LOW`` steht.

Hier ist seine Syntax:

    * ``digitalRead(pin)``: Liest den Wert eines angegebenen digitalen Pins, entweder ``HIGH`` oder ``LOW``.

        **Parameter**
            - ``pin``: die Nummer des Arduino-Pins, den du lesen möchtest
        
        **Rückgabewert**
            ``HIGH`` oder ``LOW``

2. Füge als nächstes die Befehle hinzu, die ausgeführt werden, wenn der Taster nicht gedrückt ist. Diese Befehle hast du bereits erstellt, um die normale Funktion der Ampel auszuführen.

    * Du kannst diese Befehle in die geschweiften Klammern der ``if``-Anweisung kopieren und einfügen,
    * Oder du könntest einfach die rechte geschweifte Klammer der ``if``-Anweisung nach der letzten Verzögerung verschieben.
    * Verwende die Methode, die dir am besten passt. Nachdem du dies getan hast, sollte deine ``void loop()``-Funktion in etwa so aussehen:

.. code-block:: Arduino
    :emphasize-lines: 11,24

    void setup() {
        // Setup-Code, der einmal ausgeführt wird:
        pinMode(3, OUTPUT); // Setze Pin 3 als Ausgang
        pinMode(4, OUTPUT); // Setze Pin 4 als Ausgang
        pinMode(5, OUTPUT); // Setze Pin 5 als Ausgang
        pinMode(8, INPUT);  // Deklariere Pin 8 (Taster) als Eingang
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        if (digitalRead(8) == LOW) {
            digitalWrite(3, HIGH);  // Schalte die LED an Pin 3 ein
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
            delay(10000);           // Warte 10 Sekunden
            digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
            digitalWrite(4, HIGH);  // Schalte die LED an Pin 4 ein
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
            delay(3000);            // Warte 3 Sekunden
            digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, HIGH);  // Schalte die LED an Pin 5 ein
            delay(10000);           // Warte 10 Sekunden
        }
    }

Beachte, wie die Befehle innerhalb der ``if``-Anweisung eingerückt sind. Das Verwenden von Einrückungen hilft, deinen Code übersichtlich zu halten und verdeutlicht, welche Befehle innerhalb einer Funktion ausgeführt werden. Auch wenn es ein paar Sekunden mehr dauert, helfen dir Einrückungen, Zeilenumbrüche und Kommentare, die Ästhetik deines Codes zu bewahren, was auf lange Sicht von Vorteil sein wird.

Ein häufiger Syntaxfehler ist das Vergessen der erforderlichen Anzahl von geschweiften Klammern. Manchmal fehlt die rechte Klammer in einer Funktion, oder es werden zu viele rechte Klammern hinzugefügt. In deinem Sketch benötigt jede linke Klammer eine rechte Klammer. Eine ordnungsgemäße Einrückung hilft dir auch, falsche Klammern zu beheben.


**Wenn der Taster gedrückt ist**

Jetzt ist es an der Zeit, den Code zu schreiben, der es Fußgängern ermöglicht, die Straße zu überqueren, wenn der Taster gedrückt wird.

Dafür benötigst du eine zweite bedingte Anweisung. Allerdings musst du diesmal den ``digitalRead()``-Wert von Pin 8 mit ``HIGH`` anstelle von ``LOW`` vergleichen.

Wenn der Taster gedrückt wird, muss die Ampel den gesamten Verkehr anhalten und signalisieren, dass es für Fußgänger sicher ist, die Straße zu überqueren. Um dies zu erreichen, musst du die rote und gelbe LED ausschalten und die grüne LED blinken lassen. Innerhalb der geschweiften Klammern deiner zweiten bedingten Anweisung fügst du drei ``digitalWrite()``-Befehle ein:


* Schalte die grüne LED an Pin 3 ein.
* Schalte die gelbe LED an Pin 4 aus.
* Schalte die rote LED an Pin 5 aus.

Lass dann die grüne LED blinken. Denk daran, dass die Blinkfrequenz durch deine ``delay()``-Anweisungen bestimmt wird.

Dein Sketch sollte in etwa so aussehen:


.. code-block:: Arduino
    :emphasize-lines: 24-31

    void setup() {
        pinMode(3, OUTPUT);  // Deklariere Pin 3 (grüne LED) als Ausgang
        pinMode(4, OUTPUT);  // Deklariere Pin 4 (gelbe LED) als Ausgang
        pinMode(5, OUTPUT);  // Deklariere Pin 5 (rote LED) als Ausgang
        pinMode(8, INPUT);   // Deklariere Pin 8 (Taster) als Eingang
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        if (digitalRead(8) == LOW) {
            digitalWrite(3, HIGH);  // Schalte die LED an Pin 3 ein
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
            delay(10000);           // Warte 10 Sekunden
            digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
            digitalWrite(4, HIGH);  // Schalte die LED an Pin 4 ein
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
            delay(3000);            // Warte 3 Sekunden
            digitalWrite(3, LOW);   // Schalte die LED an Pin 3 aus
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, HIGH);  // Schalte die LED an Pin 5 ein
            delay(10000);           // Warte 10 Sekunden
        }
        if (digitalRead(8) == HIGH) {  // Wenn der Taster gedrückt ist:
            digitalWrite(3, HIGH);       // Schalte die LED an Pin 3 ein
            digitalWrite(4, LOW);        // Schalte die LED an Pin 4 aus
            digitalWrite(5, LOW);        // Schalte die LED an Pin 5 aus
            delay(500);                  // Warte eine halbe Sekunde
            digitalWrite(3, LOW);        // Schalte die LED an Pin 3 aus
            delay(500);                  // Warte eine halbe Sekunde
        }
    }

Lade deinen Code auf den Arduino Uno R3 hoch. Sobald der Sketch vollständig übertragen ist, wird der Code ausgeführt.

Beobachte das Verhalten deiner Ampel. Drücke den Taster und warte, bis die Ampel ihren Zyklus abgeschlossen hat. Blinkt das Fußgängergrünlicht? Wenn der Taster losgelassen wird, kehrt die Ampel dann in ihren normalen Betriebsmodus zurück? Wenn nicht, nimm Anpassungen an deinem Sketch vor und lade ihn erneut auf den R3 hoch.

Speichere deinen Sketch, sobald du fertig bist.

**Frage:**

Während des Tests wirst du vielleicht feststellen, dass die grüne LED nur blinkt, solange der Fußgängertaster gedrückt bleibt. 
Da Fußgänger jedoch nicht in der Lage sind, die Straße zu überqueren, während sie den Taster gedrückt halten, wie kannst du den Code ändern, um sicherzustellen, dass die grüne LED 
lange genug leuchtet, damit Fußgänger sicher überqueren können, ohne den Taster ständig gedrückt zu halten? Bitte schreibe die Pseudocode-Lösung in dein Handbuch.

**Zusammenfassung**

In dieser Lektion haben wir uns mit der Integration eines Fußgängertasters in ein Ampelsystem befasst, um ein Szenario aus der realen Welt zu simulieren, das den Verkehrsfluss sowohl für Fußgänger als auch für Fahrzeuge berücksichtigt. Wir haben untersucht, wie ein Taster in einer elektronischen Schaltung funktioniert, und die ``digitalRead()``-Funktion verwendet, um Eingaben des Tasters zu überwachen. Durch die Implementierung von bedingten Anweisungen mit ``if``-Strukturen haben wir die Ampel programmiert, um dynamisch auf Fußgängereingaben zu reagieren und unser Verständnis für interaktive Systeme zu vertiefen. Diese Lektion hat nicht nur unsere Fähigkeiten in der Arduino-Programmierung gestärkt, sondern auch die praktische Anwendung dieser Technologien im effizienten Umgang mit alltäglichen Situationen hervorgehoben.

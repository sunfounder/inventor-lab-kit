.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum mitmachen?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Vorschauen.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und festlichen Aktionen teil.

    👉 Bereit, mit uns zu entdecken und zu erschaffen? Klicke auf [|link_sf_facebook|] und trete noch heute bei!

6. LED Blinken lassen
=========================

Willkommen zu dieser Lektion! Hier lernst du, die digitalen Pins des Arduino Uno R3 zu steuern, um eine LED programmatisch ein- und auszuschalten, ohne manuelles Eingreifen. Diese Fähigkeit ist sowohl für Heim- als auch für Industrieelektronikanwendungen von grundlegender Bedeutung.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/6_blink_led.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In dieser Lektion wirst du lernen:

* Sketche mit der Arduino IDE zu erstellen und zu speichern.
* Die Funktionen ``pinMode()`` und ``digitalWrite()`` zu verwenden, um Schaltungselemente zu steuern.
* Sketche auf den Arduino Uno R3 hochzuladen und deren Echtzeiteffekte zu verstehen.
* Die Funktion ``delay()`` in Sketchen einzusetzen, um das Verhalten der Schaltung zu steuern.

Am Ende dieser Lektion wirst du in der Lage sein, eine Schaltung zu bauen, die nicht nur eine LED zum Leuchten bringt, sondern sie auch in von dir festgelegten Intervallen blinken lässt. Dies gibt dir ein grundlegendes Verständnis dafür, wie Software mit Hardware interagiert.

Aufbau der Schaltung
--------------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Rote LED
     - 1 * 220Ω Widerstand
     - Jumperkabel
   * - |list_uno_r3| 
     - |list_red_led| 
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

**Schritt-für-Schritt-Aufbau**

Nimm die im Abschnitt :ref:`2_first_circuit` aufgebaute Schaltung und verbinde das Kabel von Pin 5V mit Pin 3, wie im Bild unten gezeigt.

.. image:: img/6_led_circuit.png
    :width: 600
    :align: center

Falls du die vorherige Schaltung abgebaut hast, kannst du sie anhand der folgenden Schritte neu aufbauen:

1. Verbinde den 220-Ohm-Widerstand mit dem Steckbrett. Ein Draht sollte am negativen Anschluss und der andere Draht sollte in Loch 1B sein.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

2. Füge eine rote LED zum Steckbrett hinzu. Die Anode der LED (das lange Bein) sollte in Loch 1F sein. Die Kathode (das kurze Bein) sollte in Loch 1E sein. Manchmal ist es schwierig, die Anode von der Kathode anhand der Beinlänge zu unterscheiden. Denke daran, dass die Kathodenseite der LED auch eine flache Kante an der farbigen Linse hat, während die Anodenseite eine runde Kante hat.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

3. Verwende ein kurzes Jumperkabel, um die LED und die Stromquelle zu verbinden. Ein Ende des Jumperkabels sollte in Loch 1J sein, das andere Ende sollte am positiven Anschluss sein.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

4. Verbinde den positiven Anschluss des Steckbretts mit Pin 3 des Arduino Uno R3.

.. image:: img/6_led_circuit_3.png
    :width: 600
    :align: center

5. Verbinde den negativen Anschluss des Steckbretts mit einem der Masse-Pins des Arduino Uno R3. Die Masse-Pins sind mit "GND" markiert.

.. image:: img/6_led_circuit.png
    :width: 600
    :align: center

LED zum Leben erwecken
-----------------------------

Los geht's, es ist Zeit, die LED in Aktion zu bringen! Anstatt direkt das Blink-Beispiel von Arduino zu verwenden, fangen wir von Grund auf an und erstellen einen völlig neuen Sketch. Los geht's!

**1. Einen Sketch erstellen und speichern**

1. Starte die Arduino IDE. Gehe zum Menüpunkt „Datei“ und wähle „Neuer Sketch“, um einen neuen Sketch zu beginnen. Du kannst alle anderen geöffneten Sketch-Fenster schließen.

    .. image:: img/6_blink_ide_new.png
        :align: center

2. Ordne das Arduino IDE-Fenster neben diesem Online-Tutorial an, damit du beides gleichzeitig sehen kannst. Es mag vielleicht etwas klein wirken, aber es erspart dir das ständige Hin- und Herschalten zwischen den Fenstern.

    .. image:: img/6_blink_ide_tutorials.png

3. Jetzt ist es Zeit, deinen Sketch zu speichern. Klicke im Menü „Datei“ auf „Speichern“ oder drücke ``Strg + S``.

    .. image:: img/6_blink_ide_save.png

4. Du kannst deinen Sketch am Standardort oder an einem anderen Ort speichern. Benenne deinen Sketch sinnvoll, z. B. ``Lesson6_Light_up_LED``, und klicke auf „Speichern“.

    * Benenne deinen Sketch nach seiner Funktion, um ihn später leichter wiederzufinden.
    * Arduino-Sketch-Dateinamen dürfen keine Leerzeichen enthalten.
    * Wenn du wesentliche Änderungen vornimmst, speichere sie als neue Version (z. B. V1) zur Sicherung.

    .. image:: img/6_blink_ide_name.png

5. Dein neuer Sketch besteht aus zwei Hauptteilen, ``void setup()`` und ``void loop()``, die in allen Arduino-Sketches verwendet werden.

    * ``void setup()`` wird einmal ausgeführt, wenn das Programm startet, und richtet die Anfangsbedingungen ein.
    * ``void loop()`` wird fortlaufend ausgeführt und führt kontinuierliche Aktionen aus.
    * Befehle für jede Funktion werden innerhalb ihrer geschweiften Klammern ``{}`` platziert.
    * Jede Zeile, die mit ``//`` beginnt, ist ein Kommentar. Diese dienen deinen Notizen und beeinflussen die Codeausführung nicht.

    .. code-block:: Arduino

        void setup() {
        // Setup-Code hier, der einmal ausgeführt wird:

        }

        void loop() {
        // Hauptcode hier, der wiederholt ausgeführt wird:

        }

**2. Das Board und den Port auswählen**

1. Verbinde dein Arduino Uno R3 mit dem Computer über ein USB-Kabel. Die Stromanzeige auf dem Arduino wird leuchten.

    .. image:: img/1_connect_uno_pc.jpg
        :width: 600
        :align: center

2. Teile der IDE mit, dass wir ein **Arduino Uno** verwenden. Gehe zu **Werkzeuge** -> **Board** -> **Arduino AVR Boards** -> **Arduino Uno**.

    .. image:: img/6_blink_ide_board.png
        :width: 600
        :align: center

3. Wähle in der Arduino IDE den Port aus, an den dein Arduino angeschlossen ist.

    .. note::

        * Sobald ein Port ausgewählt ist, sollte die Arduino IDE ihn jedes Mal automatisch erkennen, wenn das Arduino über USB angeschlossen ist.
        * Wenn ein anderes Arduino-Board angeschlossen wird, musst du möglicherweise einen neuen Port auswählen.
        * Überprüfe immer zuerst den Port, wenn Verbindungsprobleme auftreten.

    .. image:: img/6_blink_ide_port.png
        :width: 600
        :align: center

**3. Den Code schreiben**

1. In unserem Projekt verwenden wir den digitalen Pin 3 auf dem Board, um eine LED zu steuern. Jeder Pin kann entweder als Ausgang, der 5 Volt sendet, oder als Eingang, der eingehende Spannung liest, fungieren. Um die LED zu konfigurieren, setzen wir den Pin als Ausgang, indem wir die Funktion ``pinMode(pin, mode)`` verwenden.

Tauchen wir in die Syntax von ``pinMode()`` ein.

    * ``pinMode(pin, mode)``: Setzt einen spezifischen Pin auf ``INPUT`` oder ``OUTPUT``.

    **Parameter**
        - ``pin``: die Nummer des Pins, den du einstellen möchtest.
        - ``mode``: ``INPUT``, ``OUTPUT`` oder ``INPUT_PULLUP``.

    **Rückgabewert**
        Kein Rückgabewert

2. Nun fügen wir unsere erste Codezeile in der Funktion ``void setup()`` hinzu.
        
    .. note::

        - Arduino-Code ist case-sensitiv. Stelle sicher, dass du die Funktionen genau so schreibst, wie sie sind.
        - Beachte, dass der Befehl mit einem Semikolon endet. In der Arduino-IDE muss jeder Befehl mit einem Semikolon enden.
        - Kommentare im Code sind hilfreich, um sich selbst daran zu erinnern, was eine Zeile oder ein Abschnitt des Codes tut.

    .. code-block:: Arduino
        :emphasize-lines: 3

        void setup() {
            // Setup-Code hier, der einmal ausgeführt wird:
            pinMode(3,OUTPUT); // Pin 3 als Ausgang setzen
        }
    
        void loop() {
        // Hauptcode hier, der wiederholt ausgeführt wird:

        }



**4. Den Code verifizieren**

Bevor wir unsere Ampeln aktivieren, verifizieren wir den Code. Dies überprüft, ob die Arduino-IDE deine Befehle verstehen und in Maschinensprache übersetzen kann.

1. Um deinen Code zu verifizieren, klicke auf das **Häkchen** in der oberen linken Ecke des Fensters.

    .. image:: img/6_blink_ide_verify.png
        :width: 600
        :align: center


2. Wenn dein Code maschinenlesbar ist, erscheint unten eine Nachricht, die anzeigt, dass der Code erfolgreich kompiliert wurde. In diesem Bereich wird auch angezeigt, wie viel Speicherplatz dein Programm belegt.

    .. image:: img/6_blink_ide_verify_done.png
        :width: 600
        :align: center


3. Falls ein Fehler in deinem Code vorliegt, wird eine orangefarbene Fehlermeldung angezeigt. Die IDE hebt oft hervor, wo das Problem liegen könnte, normalerweise in der Nähe der hervorgehobenen Zeile. Zum Beispiel wird ein fehlendes Semikolon einen Fehler in der Zeile direkt nach dem Fehler anzeigen.

    .. image:: img/6_blink_ide_verify_error.png
        :width: 600
        :align: center


4. Wenn du auf Fehler stößt, ist es Zeit zum Debuggen – das Finden und Beheben von Fehlern in deinem Code. Überprüfe häufige Probleme wie:

    - Ist das ``M`` in ``pinMode`` großgeschrieben?
    - Hast du ``OUTPUT`` in Großbuchstaben geschrieben?
    - Hast du in deiner ``pinMode``-Funktion sowohl eine öffnende als auch eine schließende Klammer?
    - Hast du deine ``pinMode``-Funktion mit einem Semikolon beendet?
    - Ist deine Rechtschreibung korrekt? Wenn du Fehler findest, korrigiere sie und verifiziere deinen Code erneut. Debugge weiter, bis dein Sketch fehlerfrei ist.

Die Arduino-IDE stoppt das Kompilieren beim ersten Fehler, also musst du möglicherweise mehrmals verifizieren, um mehrere Fehler zu beheben. Regelmäßiges Verifizieren deines Codes ist eine gute Praxis.

Debugging ist ein großer Teil des Programmierens. Professionelle Programmierer verbringen oft viel mehr Zeit mit dem Debuggen als mit dem Schreiben neuer Codes. Fehler sind normal, also lass dich nicht entmutigen. Ein guter Problemlöser zu werden, ist der Schlüssel zu einem großartigen Programmierer.

**5. Den Sketch weiter schreiben**

1. Jetzt bist du bereit, die Funktion ``void loop()`` zu starten. Hier passiert die Hauptaktion deines Sketches oder Programms. Um die LED, die mit dem Arduino Uno R3 verbunden ist, zum Leuchten zu bringen, müssen wir der Schaltung mit ``digitalWrite()`` Spannung zuführen.

    * ``digitalWrite(pin, value)``: Sendet ein ``HIGH`` (5V) oder ``LOW`` (0V) Signal an einen digitalen Pin, um den Betriebszustand der Komponente zu ändern.

    **Parameter**
        - ``pin``: die Nummer des Arduino-Pins.
        - ``value``: ``HIGH`` oder ``LOW``.

    **Rückgabewert**
        Kein Rückgabewert

5. Schreibe unter den Kommentar in der Funktion ``void loop()`` einen Befehl, um die LED, die mit Pin 3 verbunden ist, einzuschalten. Vergiss nicht, den Befehl mit einem Semikolon zu beenden. Verifiziere und debugge deinen Code bei Bedarf.

    .. code-block:: Arduino
        :emphasize-lines: 8

        void setup() {
            // Setup-Code hier, der einmal ausgeführt wird:
            pinMode(3, OUTPUT);  // Pin 3 als Ausgang setzen
        }

        void loop() {
            // Hauptcode hier, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);
        }

6. Füge nach dem ``digitalWrite()``-Befehl einen Kommentar hinzu, der erklärt, was diese Zeile bewirkt. Zum Beispiel:

    .. code-block:: Arduino
        :emphasize-lines: 8

        void setup() {
            // Setup-Code hier, der einmal ausgeführt wird: 
            pinMode(3, OUTPUT);  // Pin 3 als Ausgang setzen
        }

        void loop() {
            // Hauptcode hier, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // Die LED an Pin 3 einschalten
        }


**6. Den Code hochladen**

Nachdem dein Code fehlerfrei und verifiziert ist, ist es an der Zeit, ihn auf den Arduino Uno R3 hochzuladen und deine Ampel zum Leben zu erwecken.

1. In der IDE klicke auf den „Upload“-Button. Der Computer wird den Code kompilieren und dann auf den Arduino Uno R3 übertragen. Während der Übertragung solltest du einige Lichter auf dem Board blinken sehen, was auf die Kommunikation mit dem Computer hinweist.

.. image:: img/6_blink_ide_upload.png
    :width: 600
    :align: center


2. Eine Nachricht „Done Uploading“ bedeutet, dass dein Code keine Probleme aufweist und du das richtige Board und den richtigen Port ausgewählt hast.

.. image:: img/6_blink_ide_upload_done.png
    :width: 600
    :align: center


3. Sobald die Übertragung abgeschlossen ist, wird der Code ausgeführt, und du solltest sehen, wie die LED auf dem Steckbrett aufleuchtet.
**7. Messung der Spannung über der LED**

Lass uns ein Multimeter verwenden, um die Spannung an Pin 3 zu messen und zu verstehen, was der ``HIGH``-Zustand im Code tatsächlich bedeutet.

1. Stelle das Multimeter auf die Einstellung 20 Volt Gleichspannung (DC) ein.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Beginne mit der Messung der Spannung an Pin 3. Berühre mit der roten Messleitung des Multimeters Pin 3 und mit der schwarzen Messleitung den GND-Pin.

.. image:: img/6_blink_wiring_measure_high.png
    :width: 600
    :align: center

3. Trage die gemessene Spannung in die Tabelle für Pin 3 unter der Zeile "HIGH" ein.

.. list-table::
   :widths: 25 25
   :header-rows: 1

   * - Zustand
     - Pin 3 Spannung
   * - HIGH
     - *≈4,95 Volt*
   * - LOW
     - 


4. Nach der Messung solltest du das Multimeter ausschalten, indem du es auf die "OFF"-Position stellst.

Unsere Messungen zeigen, dass die Spannung an allen drei Pins nahe 5V liegt. Dies bedeutet, dass das Setzen eines Pins auf ``HIGH`` im Code dazu führt, dass die Ausgangsspannung an diesem Pin nahe 5V liegt.

Die Spannung des Pin 3 am Arduino R3 beträgt 5V, sodass das Setzen auf ``HIGH`` fast 5V erreicht. Allerdings arbeiten einige Boards bei 3,3V, was bedeutet, dass ihr ``HIGH``-Zustand nahe 3,3V liegt.


LED zum Blinken bringen
------------------------------
Nun, da deine LED leuchtet, ist es an der Zeit, sie zum Blinken zu bringen.

1. Öffne den Sketch, den du zuvor gespeichert hast, ``Lesson6_Light_up_LED``. Wähle im Menü "Datei" die Option "Speichern unter..." und benenne den Sketch in ``Lesson6_Blink_LED`` um. Klicke auf "Speichern".

2. In der Funktion ``void loop()`` deines Sketches kopierst du die ``digitalWrite()``-Befehle und fügst sie nach den Originalen ein. Um die LED zum Blinken zu bringen, hast du sie zuvor eingeschaltet; nun setze ihren Zustand auf ``LOW``, um sie auszuschalten.

    .. note::
       * Kopieren und Einfügen kann ein großer Vorteil für Programmierer sein. Repliziere einen sauberen Codeabschnitt an einer neuen Position und passe die Parameter schnell und sauber an.
       * Vergiss nicht, die Kommentare zu aktualisieren, um die ausgeführte Aktion besser zu beschreiben.
       * Verwende ``Ctrl+T``, um deinen Code mit einem Klick ordentlich zu formatieren und besser lesbar zu machen.

    .. code-block:: Arduino
       :emphasize-lines: 8,9

       void setup() {
            // Setup-Code hier, der einmal ausgeführt wird:
            pinMode(3, OUTPUT);  // Pin 3 als Ausgang setzen
       }

       void loop() {
            // Hauptcode hier, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // LED an Pin 3 einschalten   
            digitalWrite(3, LOW);  // LED an Pin 3 ausschalten
       }

3. Drücke die „Upload“-Taste, um den Sketch auf den Arduino Uno R3 zu übertragen. Nach der Übertragung stellst du vielleicht fest, dass die LED nicht blinkt oder so schnell blinkt, dass es nicht wahrnehmbar ist.

4. Um das Blinken sichtbar zu machen, kannst du den ``delay()``-Befehl verwenden, um den Arduino Uno R3 für eine von dir festgelegte Zeitspanne in Millisekunden warten zu lassen.

    * ``delay(ms)``: Pausiert das Programm für die im Parameter angegebene Zeitspanne (in Millisekunden). (Es gibt 1000 Millisekunden in einer Sekunde.)

    **Parameter**
        - ``ms``: die Anzahl der Millisekunden, die das Programm pausieren soll. Zulässige Datentypen: unsigned long.

    **Rückgabewert**
        Kein Rückgabewert

5. Füge nun den ``delay(time)``-Befehl nach jedem Satz von EIN- und AUS-Befehlen hinzu und setze die Wartezeit auf 3000 Millisekunden (3 Sekunden). Du kannst diese Dauer anpassen, um die LED schneller oder langsamer blinken zu lassen.

    .. note::

        Während dieser Verzögerung kann der Arduino Uno R3 keine Aufgaben ausführen oder andere Befehle ausführen, bis die Verzögerung endet.
        
    .. code-block:: Arduino
       :emphasize-lines: 10,11

       void setup() {
            // Setup-Code hier, der einmal ausgeführt wird:
            pinMode(3, OUTPUT);  // Pin 3 als Ausgang setzen
       }

       void loop() {
            // Hauptcode hier, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // LED an Pin 3 einschalten
            delay(3000); // 3 Sekunden warten   
            digitalWrite(3, LOW);  // LED an Pin 3 ausschalten
            delay(3000); // 3 Sekunden warten
       }

6. Lade deinen Sketch auf den Arduino Uno R3 hoch. Nach Abschluss sollte deine LED in einem Intervall von 3 Sekunden blinken.

7. Überprüfe, ob alles wie erwartet funktioniert, und speichere dann deinen Sketch.

8. Lass uns ein Multimeter verwenden, um die Spannung an den drei Pins zu messen und zu verstehen, was der ``LOW``-Zustand im Code tatsächlich bedeutet. Stelle das Multimeter auf die Einstellung 20 Volt Gleichspannung (DC) ein.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

9. Beginne mit der Messung der Spannung an Pin 3. Berühre mit der roten Messleitung des Multimeters Pin 3 und mit der schwarzen Messleitung den GND-Pin.

.. image:: img/6_blink_wiring_measure_high.png
    :width: 600
    :align: center

10. Wenn alle drei LEDs ausgeschaltet sind, trage die gemessene Spannung für Pin 3 in die Zeile "LOW" deiner Tabelle ein.

.. list-table::
   :widths: 25 25
   :header-rows: 1

   * - Zustand
     - Pin 3 Spannung 
   * - HIGH
     - *≈4,95 Volt*
   * - LOW
     - *0,00 Volt*

Durch unsere Messungen haben wir festgestellt, dass, wenn die LEDs ausgeschaltet sind, die Spannung an Pin 3 auf 0V sinkt. Dies zeigt, dass das Setzen eines Pins auf "LOW" im Code die Ausgangsspannung an diesem Pin effektiv auf 0V reduziert und die angeschlossene LED ausschaltet. Dieses Prinzip ermöglicht es uns, die Ein- und Aus-Zustände der LED mit präzisem Timing zu steuern, was das Verhalten einer Ampel simuliert.

**Frage**

Lade den obigen Code hoch, und du wirst feststellen, dass die LED in einem Intervall von 3 Sekunden wiederholt blinkt. Wenn du möchtest, dass sie sich nur einmal ein- und ausschaltet, was musst du tun?

**Zusammenfassung**

Herzlichen Glückwunsch zum Abschluss dieser Lektion, in der du erfolgreich eine LED programmiert hast, um mit dem Arduino Uno R3 zu blinken. Diese Lektion diente als Einführung in das Schreiben und Hochladen von Arduino-Sketches, das Setzen von Pin-Modi und das Manipulieren von Ausgaben, um gewünschte elektrische Reaktionen zu erzielen. Durch den Bau der Schaltung und die Programmierung des Arduino Uno R3 hast du wertvolle Einblicke in die Interaktion zwischen Softwarebefehlen und physikalischen Hardwareverhalten gewonnen.

Deine Fähigkeit, eine LED zu steuern, ist nur der Anfang – stelle dir vor, was du erreichen kannst, wenn du auf diesen Grundlagen aufbaust!

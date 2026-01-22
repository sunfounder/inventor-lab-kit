.. note::

  Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein – gemeinsam mit anderen Technikbegeisterten.

  **Warum beitreten?**

  - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
  - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
  - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Vorschauen.
  - **Exklusive Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
  - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und saisonalen Aktionen teil.

  👉 Bereit, mit uns zu erkunden und zu kreieren? Klicke [|link_sf_facebook|] und trete noch heute bei!

26. Cyber-Würfel
=======================

In dieser Lektion begeben wir uns auf eine spannende Reise durch zwei Projekte, die digitale Elektronik und Programmierung miteinander verbinden.

.. image:: img/23_dice.jpg
    :align: center
    :width: 500

Zunächst beschäftigen wir uns mit der Funktionsweise einer 7-Segment-Anzeige und lernen Schritt für Schritt, wie wir diese steuern, um Zahlen anzuzeigen. Anschließend erstellen wir einen elektronischen Würfel! Durch einfaches Drücken einer Taste erscheint eine Zufallszahl zwischen 1 und 6 auf der 7-Segment-Anzeige – eine digitale Variante des klassischen Würfels.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/26_cycle_dice.mp4" type="video/mp4">
        Ihr Browser unterstützt das Video-Tag nicht.
    </video>

Während dieser Lektion wirst du lernen:

* Die Funktionsprinzipien einer 7-Segment-Anzeige und wie man sie zum Laufen bringt.
* Die Verwendung von switch-case-Anweisungen zur Vereinfachung der Code-Logik.
* Wie man eine while-Schleife nutzt, um den aktuellen Zustand beizubehalten, bis eine Änderung erforderlich ist.
* Wie man das Cyber-Würfel-Projekt erstellt und einfache Elektronik mit interaktiver Programmierung für praktische Anwendungen kombiniert.

Der Ursprung der Würfel
-----------------------

Würfel gehören zu den ältesten Glücksspielwerkzeugen der Welt und haben eine Geschichte, die Tausende von Jahren vor der christlichen Zeitrechnung zurückreicht. Sie entstanden um 3000 v. Chr. im alten Ägypten und wurden typischerweise aus Knochen, Elfenbein oder anderen natürlichen Materialien hergestellt. Diese frühen Würfel waren oft unregelmäßig geformt und manchmal nicht ganz symmetrisch.

.. image:: img/23_dice.png
    :width: 500
    :align: center

Würfel wurden zur gleichen Zeit auch im antiken Mesopotamien (dem heutigen Irak) gefunden. Antike Wahrsager und religiöse Führer nutzten Würfel, um Entscheidungen zu treffen oder die Zukunft vorherzusagen, was ihre Bedeutung in religiösen und mystischen Riten unterstreicht.

Mit der Zeit wurden die Form und die Herstellungstechniken von Würfeln standardisiert. Bis zum 1. Jahrhundert v. Chr. waren Würfel im Römischen Reich weit verbreitet und wurden nicht nur zum Glücksspiel, sondern auch zu sozialen und unterhaltsamen Zwecken verwendet.

In Asien, insbesondere in Indien, ist die Nutzung von Würfeln in dem alten Epos Mahabharata dokumentiert, wo ein entscheidendes Würfelspiel eine zentrale Rolle in der Handlung spielt.

Während der Renaissance wurde die Würfelproduktion weiter verfeinert, und die Materialien diversifizierten sich, darunter Holz, Knochen, Elfenbein und sogar Metall. Heute sind Würfel nicht nur Werkzeuge für Unterhaltung und Glücksspiel, sondern werden auch in der Bildung, zur Entscheidungsfindung und in verschiedenen Tischspielen verwendet. Ihre Geschichte und Vielfalt spiegeln die Entwicklung der menschlichen Kultur und Technologie wider und bieten ein faszinierendes Fenster in die Erforschung von Zufall und Glück.

.. _learn_7segment:

Lerne die 7-Segment-Anzeige kennen
-------------------------------------------

1. Suche eine 7-Segment-Anzeige.

Eine 7-Segment-Anzeige ist ein 8-förmiges Bauteil, das 7 LEDs enthält. Jede der LEDs in der Anzeige hat ein eigenes Positionssegment, wobei einer ihrer Anschlussstifte aus dem rechteckigen Kunststoffgehäuse herausgeführt wird. Diese LED-Stifte sind von "a" bis "g" beschriftet und repräsentieren jede einzelne LED. 
Die anderen LED-Stifte sind miteinander verbunden und bilden einen gemeinsamen Anschluss. Eine zusätzliche achte LED wird im selben Gehäuse verwendet, sodass bei der Verbindung von zwei oder mehr 7-Segment-Anzeigen zur Anzeige von Zahlen über zehn ein Dezimalpunkt (DP) angezeigt werden kann.

.. image:: img/23_7_segment.png
    :width: 300
    :align: center

Der gemeinsame Pin der Anzeige gibt im Allgemeinen ihren Typ an. Es gibt zwei Arten von Pin-Verbindungen: eine mit verbundenen Kathoden und eine andere mit verbundenen Anoden, was auf Common Cathode (CC) und Common Anode (CA) hinweist. Wie der Name schon sagt, haben bei einer CC-Anzeige alle 7 LEDs eine gemeinsame Kathode, während bei einer CA-Anzeige alle Anoden der 7 Segmente miteinander verbunden sind.

.. note::

    Normalerweise befindet sich auf der Seite der 7-Segment-Anzeige ein Etikett, das entweder xxxAx oder xxxBx lautet. Im Allgemeinen steht xxxAx für Common Cathode und xxxBx für Common Anode. Die Anzeigen in unserem Kit sind Common Cathode.

.. image:: img/23_segment_cathode_1.png
    :align: center
    :width: 600

Um festzustellen, ob eine 7-Segment-Anzeige Common Cathode oder Common Anode ist, kannst du ein Multimeter verwenden. Du kannst auch ein Multimeter verwenden, um zu testen, ob jedes Segment der Anzeige ordnungsgemäß funktioniert, wie folgt:

1. Stelle das Multimeter auf den Diodentestmodus ein. Der Diodentest ist eine Funktion des Multimeters, um die Vorwärtsleitung von Dioden oder ähnlichen Halbleiterbauteilen (wie LEDs) zu prüfen. Das Multimeter lässt einen kleinen Strom durch die Diode fließen. Wenn die Diode intakt ist, wird sie den Strom durchlassen.

.. image:: img/multimeter_diode.png
    :width: 300
    :align: center

2. Setze die 7-Segment-Anzeige in ein Steckbrett ein, beachte, dass der Dezimalpunkt unten rechts ist, und achte darauf, dass sie die mittlere Lücke überbrückt. Stecke einen Draht in die gleiche Reihe wie Pin 1 der Anzeige und berühre ihn mit der roten Prüfspitze des Multimeters. Stecke einen anderen Draht in die gleiche Reihe wie einen beliebigen "-" Pin der Anzeige und berühre ihn mit der schwarzen Prüfspitze.

.. image:: img/23_7_segment_test.png
    :align: center
    :width: 500

3. Beobachte, ob ein LED-Segment aufleuchtet. Wenn ja, zeigt dies an, dass die Anzeige eine Common Cathode ist. Wenn nicht, vertausche die rote und schwarze Prüfspitze; wenn ein Segment nach dem Vertauschen aufleuchtet, zeigt dies an, dass die Anzeige eine Common Anode ist.

4. Wenn ein Segment aufleuchtet, beziehe dich auf dieses Diagramm, um die Pin-Nummer des Segments und die ungefähre Position in der Tabelle deines Handbuchs zu notieren.

.. image:: img/23_segment_2.png
    :align: center

.. list-table::
    :widths: 20 20 40
    :header-rows: 1

    *   - Pin
        - Segmentnummer
        - Position
    *   - 1
        - a
        - Das obere Segment
    *   - 2
        -
        - 
    *   - 3
        -
        - 
    *   - 4
        -
        - 
    *   - 5
        -
        - 
    *   - 6
        -
        - 
    *   - 7
        -
        - 
    *   - 8
        -
        -     


5. Wiederhole die obigen Schritte und halte das schwarze Kabel am "-" Pin. Verbinde das rote Kabel mit den anderen Pins, um herauszufinden, welche Steuerpins den LED-Segmenten der Anzeige entsprechen.


**Frage**

Aus den obigen Tests geht hervor, dass das Display im Kit eine gemeinsame Kathode ist. Das bedeutet, dass du den gemeinsamen Pin nur mit GND verbinden musst und eine hohe Spannung an die anderen Pins anlegst, um die entsprechenden Segmente zum Leuchten zu bringen. Wenn das Display die Zahl 2 anzeigen soll, welche Pins müssen dann mit einer hohen Spannung versorgt werden? Warum?

.. image:: img/23_segment_2.png
    :align: center



Schaltung Aufbau
--------------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * 7-Segment-Anzeige
     - 1 * 220Ω Widerstand
     - 1 * 10KΩ Widerstand
   * - |list_uno_r3| 
     - |list_7segment| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * Taster
     - 1 * Breadboard
     - Jumperkabel
     - 1 * USB-Kabel
   * - |list_button| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_usb_cable| 
   * - 1 * Multimeter
     - 
     - 
     - 
   * - |list_meter| 
     - 
     - 
     - 



**Schritt-für-Schritt Aufbau**

Folge dem Schaltplan oder den folgenden Schritten, um deine Schaltung aufzubauen.

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

1. Setze die 7-Segment-Anzeige in das Breadboard ein, wobei der Dezimalpunkt unten rechts liegt.

.. image:: img/23_segment_segment.png
    :align: center
    :width: 500

2. Stecke ein Ende eines 220Ω Widerstands in das negative („-") Terminal der 7-Segment-Anzeige und das andere Ende in die Minus-Schiene des Breadboards. Verbinde dann die Minus-Schiene des Breadboards mit dem GND-Pin des Arduino Uno R3 mithilfe eines Jumperkabels.

.. image:: img/23_segment_resistor_gnd.png
    :align: center
    :width: 500

3. Verbinde die Pins, die die a-, b- und c-Segmente der LED steuern, mit den Pins 2, 3 und 4 auf dem Arduino Uno R3.

.. image:: img/23_segment_abc.png
    :align: center
    :width: 500

4. Verbinde die Pins, die die d-, e-, f- und g-Segmente der LED steuern, mit den Pins 5, 6, 7 und 8 auf dem Arduino Uno R3.

.. image:: img/23_segment_defg.png
    :align: center
    :width: 500

5. Setze nun einen Taster in das Breadboard ein.

.. image:: img/23_segment_button.png
    :align: center
    :width: 500

6. Verbinde den unteren rechten Pin des Tasters mit Pin 9 des R3 mithilfe eines Kabels.

.. image:: img/23_segment_pin9.png
    :align: center
    :width: 500

7. Verbinde einen 10KΩ Pull-Down-Widerstand mit dem Taster, damit Pin 9 auf einem niedrigen Pegel bleibt, wenn der Taster nicht gedrückt wird, und kein Prellen auftritt.

.. image:: img/23_segment_10k_resistor.png
    :align: center
    :width: 500

8. Verbinde den unteren linken Pin des Tasters mit dem 5V-Pin des Arduino Uno R3.

.. image:: img/23_segment_5v.png
    :align: center
    :width: 500

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - 7-Segment-Anzeige
        - Arduino UNO R3
    *   - a
        - 2
    *   - b
        - 3 
    *   - c
        - 4
    *   - d
        - 5
    *   - e
        - 6
    *   - f
        - 7
    *   - g
        - 8


Code-Erstellung - Zahlen anzeigen
-------------------------------------
1. Öffne die Arduino IDE und starte ein neues Projekt, indem du im Menü „Datei“ die Option „Neues Sketch“ auswählst.
2. Speichere dein Sketch als ``Lesson26_Show_Number`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Definiere die Pins, die mit der 7-Segment-Anzeige verbunden sind, und setze alle Pins als Ausgänge.

.. code-block:: Arduino

    // Definiere Pins, die mit der 7-Segment-Anzeige verbunden sind
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Setze alle Pins als Ausgänge
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

4. Schreibe nun den Code, damit die 7-Segment-Anzeige eine Zahl anzeigt, z. B. die Zahl 2. Um die Zahl 2 anzuzeigen, setze die Segmente F und C auf LOW (aus), die anderen Segmente auf HIGH (ein).

.. code-block:: Arduino
  :emphasize-lines: 22-29

    // Definiere Pins, die mit der 7-Segment-Anzeige verbunden sind
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Setze alle Pins als Ausgänge
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {
        // Setze die Segmente F und C auf LOW (aus), die anderen Segmente auf HIGH (ein)
        digitalWrite(pinA, HIGH);
        digitalWrite(pinB, HIGH);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, HIGH);
        digitalWrite(pinE, HIGH);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, HIGH);
    }

5. Jetzt kannst du den Code auf das Arduino Uno R3 hochladen und die Zahl 2 auf der 7-Segment-Anzeige sehen.

6. Wenn du andere Zahlen anzeigen möchtest, zum Beispiel von 1 bis 6 zyklisch durchgehen, würde die Verwendung von ``digitalWrite()`` zur Steuerung jedes Segments den Code sehr lang machen und die Logik weniger klar. Daher verwenden wir eine Methode zur Funktionserstellung.

7. Erstelle eine Funktion mit einem Parameter - ``displayDigit()``, die zuerst alle LED-Segmente der 7-Segment-Anzeige ausschaltet.

.. code-block:: Arduino

    void displayDigit(int digit) {
        // Schalte alle Segmente aus
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);
    }

8. Als Nächstes steuere die verschiedenen LED-Segmente, um Zahlen anzuzeigen. Hier könnten wir ``if-else``-Anweisungen verwenden, was jedoch umständlich sein könnte. Daher bietet eine ``switch``-Anweisung eine klarere und organisiertere Möglichkeit, zwischen mehreren möglichen unterschiedlichen Verhaltensweisen zu wählen, als mehrere ``if-else``-Anweisungen.

In der Programmierung ist eine ``switch``-Anweisung eine Kontrollstruktur, die verwendet wird, um verschiedene Codeabschnitte basierend auf dem Wert einer Variablen auszuführen.

Die grundlegende Syntax einer ``switch``-Anweisung sieht normalerweise wie folgt aus:

.. code-block:: Arduino

    switch (expression) {
        case value1:
            // Code
            break;
        case value2:
            // Code
            break;
        default:
            // Code
    }

* ``expression``: Dies ist ein Ausdruck, der typischerweise einen Integer oder ein Zeichen zurückgibt, basierend auf dem die ``switch``-Anweisung entscheidet, welcher ``case`` ausgeführt werden soll.
* ``case``: Jeder ``case``-Schlüsselwort wird von einem Wert gefolgt, der mit dem Ergebnis von ``expression`` übereinstimmen kann. Wenn eine Übereinstimmung erfolgreich ist, wird der Code ab diesem Punkt bis zu einer ``break``-Anweisung ausgeführt.
* ``break``: Die ``break``-Anweisung wird verwendet, um den ``switch``-Block zu verlassen. Ohne ``break`` würde das Programm den Code des nächsten ``case`` ausführen, unabhängig von der Übereinstimmung, was als "Fall-Through" bekannt ist.
* ``default``: Der ``default``-Teil ist optional und wird ausgeführt, wenn kein ``case`` übereinstimmt, ähnlich wie ``else`` in einer ``if-else``-Struktur.

.. image:: img/23_flow_swtich.png
    :align: center
    :width: 600

9. Verwende die ``switch-case``-Anweisung in der ``displayDigit()``-Funktion, um die Anzeige der Zahlen auf der 7-Segment-Anzeige abzuschließen. Um beispielsweise eine 1 anzuzeigen, müssen nur die Segmente B und C auf HIGH gesetzt werden; um eine 2 anzuzeigen, müssen die Segmente F und C auf LOW gesetzt werden, während die anderen auf HIGH gesetzt werden.

.. code-block:: Arduino

    void displayDigit(int digit) {
        // Schalte alle Segmente aus
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Setze die Segmente auf HIGH, um die gewünschte Zahl anzuzeigen
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }


10. Jetzt kannst du die Funktion ``displayDigit()`` in der ``void loop()`` aufrufen, um bestimmte Zahlen anzuzeigen, wie beispielsweise zyklisch zwischen 3 und 6 zu wechseln, mit einem Intervall von einer Sekunde.

.. code-block:: Arduino

    void loop() {

        displayDigit(3);  // Zeige die 3 auf der 7-Segment-Anzeige an
        delay(1000);
        displayDigit(6);  // Zeige die 6 auf der 7-Segment-Anzeige an
        delay(1000);
    }

11. Unten findest du deinen vollständigen Code. Jetzt kannst du den Code auf das Arduino Uno R3 hochladen, und du wirst sehen, wie die 7-Segment-Anzeige zwischen 3 und 6 wechselt.

.. code-block:: Arduino

    // Definiere die Pins, die mit der 7-Segment-Anzeige verbunden sind
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    void setup() {
        // Setze alle Pins als Ausgänge
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);
    }

    void loop() {

        displayDigit(3);  // Zeige die 3 auf der 7-Segment-Anzeige an
        delay(1000);
        displayDigit(6);  // Zeige die 6 auf der 7-Segment-Anzeige an
        delay(1000);
    }

    void displayDigit(int digit) {
        // Schalte alle Segmente aus
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Schalte die Segmente ein, die für die gewünschte Zahl benötigt werden (HIGH schaltet die Segmente für den gemeinsamen Kathodenmodus ein)
        switch (digit) {
            case 1:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                break;
            case 2:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 3:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 4:
                digitalWrite(pinB, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 5:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
            case 6:
                digitalWrite(pinA, HIGH);
                digitalWrite(pinC, HIGH);
                digitalWrite(pinD, HIGH);
                digitalWrite(pinE, HIGH);
                digitalWrite(pinF, HIGH);
                digitalWrite(pinG, HIGH);
                break;
        }
    }


Codeerstellung - Cyber Dice
-------------------------------------
Jetzt, da wir wissen, wie man Zahlen von 1 bis 6 auf der 7-Segment-Anzeige anzeigt, wie können wir den Effekt eines Cyber Dice erzielen?

Dies erfordert das Drücken eines Knopfes, um die Anzeige von 1 bis 6 durchlaufen zu lassen, und das Loslassen des Knopfes, um eine stabile Zahl anzuzeigen. Sehen wir uns an, wie wir dies mit Code erreichen können.

1. Öffne die zuvor gespeicherte Skizze ``Lesson26_Show_Number``. Wähle „Speichern unter...“ im „Datei“-Menü und benenne sie in ``Lesson26_Cyber_Dice`` um. Klicke auf „Speichern“.

2. Definiere den Knopf-Pin und setze ihn als Eingang.

.. code-block:: Arduino
    :emphasize-lines: 10-11,23-24

    // Definiere die Pins, die mit den Segmenten der 7-Segment-Anzeige verbunden sind
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // Definiere den Pin, der mit dem Knopf verbunden ist
    int buttonPin = 9;

    void setup() {
        // Setze alle Pins als Ausgänge
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // Setze den Knopf-Pin als Eingang
        pinMode(buttonPin, INPUT);
    }

3. Überprüfe, ob der Knopf gedrückt wird, wenn die ``void loop()``-Funktion ausgeführt wird. Wenn der Knopf nicht gedrückt wird, wird der Code innerhalb des ``if``-Blocks übersprungen.

.. code-block:: Arduino
    :emphasize-lines: 3,4

    void loop() {
        // Überprüfe, ob der Knopf gedrückt wird
        if (digitalRead(buttonPin) == HIGH) {
        }
    }

4. In der Arduino-Programmierung oder bei ähnlichen Mikrocontrollern ist ein häufiges Problem beim Umgang mit Knopf-Eingaben, dass jeder Tastendruck nur eine Aktion auslösen soll, insbesondere wenn Ereignisse oder Befehle (wie das Generieren einer Zufallszahl) erzeugt werden. Um dies zu lösen, können wir eine Technik namens "wait-for-release" verwenden.

**wait-for-release**

Die Kernidee dieser Methode besteht darin, dass nachdem ein Knopf gedrückt wurde und eine Aktion ausgeführt wurde, das Programm eine Schleife betritt, die den Knopfzustand weiter überwacht, bis er losgelassen wird. Dies stellt sicher, dass keine zusätzlichen Aktionen aufgrund von Tastenprellern oder dem Halten des Knopfes ausgelöst werden.

Wir können dies mit einer ``while``-Schleife im Code implementieren.


.. image:: img/while_loop.png
    :width: 400
    :align: center



.. code-block:: Arduino
    :emphasize-lines: 4-6

    void loop() {
        // Überprüfe, ob der Knopf gedrückt wird
        if (digitalRead(buttonPin) == HIGH) {
            // Warte, bis der Knopf losgelassen wird, bevor du weitermachst
            while (digitalRead(buttonPin) == HIGH) {
            }
        }
    }

5. Verwende nun die Funktion ``random()``, um eine Zufallszahl zwischen 1 und 6 zu generieren, und nutze ``displayDigit()``, um diese Zahl auf der 7-Segment-Anzeige anzuzeigen. Du wirst sehen, wie die Anzeige schnell durch verschiedene Zahlen läuft, während der Knopf gedrückt gehalten wird.

In der physischen Welt ist Zufälligkeit allgegenwärtig, aber in der Programmierung werden sogenannte "Zufallszahlen" normalerweise durch einen deterministischen Algorithmus berechnet. Dieser Algorithmus benötigt typischerweise einen Ausgangspunkt, der als "Seed" bezeichnet wird, wodurch diese Zahlen vorhersehbar werden und daher als "Pseudo-Zufallszahlen" bezeichnet werden. Das Präfix "Pseudo" deutet darauf hin, dass diese Zahlen zufällig erscheinen, aber tatsächlich einem Muster folgen.

Interessanterweise können wir auf einem Arduino Uno R3 physikalische Messungen aus der realen Welt als Seeds verwenden. Während deiner Messungen mit einem Multimeter könntest du leichte Schwankungen in den Spannungs- und Stromwerten des Schaltkreises bemerken. Diese Schwankungen können dazu beitragen, unsere Zufallszahlen unvorhersehbar zu machen.

Arduinos Ansatz zur Zufälligkeit umfasst mehrere Funktionen:

* ``randomSeed();``: Initialisiert den Seed-Wert des Zufallszahlengenerators. Diese Funktion stellt sicher, dass der Ausgangspunkt der Zufallszahlensequenz bei jedem Programmstart variiert und somit unterschiedliche Sequenzen erzeugt.

    **Parameter**
        * ``seed``: Ein Wert, der zur Initialisierung des Zufallszahlengenerators verwendet wird. Dieser Wert vom Typ unsigned long setzt den Startpunkt der Zufallssequenz.
    **Rückgabewert**
        Keiner.

* ``long random(long max);``: Erzeugt eine Zufallszahl innerhalb eines angegebenen Bereichs.

    **Parameter**
        ``max``: Die obere Grenze der Zufallszahl (``max`` selbst nicht eingeschlossen), was bedeutet, dass die Zufallszahl zwischen 0 (einschließlich) und ``max-1`` (einschließlich) liegt.
    
    **Rückgabewert**
        Eine Zahl vom Typ long zwischen 0 und max-1.

* ``long random(long min, long max);``: Erzeugt eine Zufallszahl innerhalb eines angegebenen Bereichs.

    **Parameter**
        ``min``: Die untere Grenze der Zufallszahl (einschließlich).
        ``max``: Die obere Grenze der Zufallszahl (``max`` selbst nicht eingeschlossen), was bedeutet, dass die Zufallszahl zwischen min (einschließlich) und max-1 (einschließlich) liegt.
    
    **Rückgabewert**
        Eine Zahl vom Typ long zwischen min und max-1.

.. code-block:: Arduino
    :emphasize-lines: 6-12

    void loop() {
        // Überprüfe, ob der Knopf gedrückt wird
        if (digitalRead(buttonPin) == HIGH) {
            // Warte, bis der Knopf losgelassen wird, bevor du weitermachst
            while (digitalRead(buttonPin) == HIGH) {
                // Generiere eine Zufallszahl zwischen 1 und 6
                int num = random(1, 7);
                
                // Zeige die Zufallszahl auf der 7-Segment-Anzeige an
                displayDigit(num);
                // Verzögerung, um sichtbare Anzeigeaktualisierungen zu ermöglichen
                delay(100);
            }
        }
    }


6. Fügen Sie schließlich eine Verzögerung hinzu, um den Taster zu entprellen und mehrere schnelle Eingaben zu verhindern.

.. code-block:: Arduino
    :emphasize-lines: 15

    void loop() {
        // Überprüfen, ob der Taster gedrückt wurde
        if (digitalRead(buttonPin) == HIGH) {
            // Warten, bis der Taster losgelassen wird, bevor es weitergeht
            while (digitalRead(buttonPin) == HIGH) {
                // Eine Zufallszahl zwischen 1 und 6 generieren
                int num = random(1, 7);
                
                // Die Zufallszahl auf dem 7-Segment-Display anzeigen
                displayDigit(num);
                // Kurze Verzögerung, um sichtbare Display-Aktualisierungen zu ermöglichen
                delay(100);
            }
            // Verzögerung hinzufügen, um den Taster zu entprellen und mehrere schnelle Eingaben zu verhindern
            delay(500);
        }
    }

7. Ihr vollständiger Code sollte jetzt so aussehen, und Sie können ihn auf das Arduino Uno R3 hochladen. Sobald der Code hochgeladen ist, werden beim Gedrückthalten des Tasters die Zahlen auf dem Display schnell durchlaufen, und wenn Sie den Taster loslassen, wird eine Zahl angezeigt.

.. code-block:: Arduino

    // Definition der Pins, die mit den Segmenten des 7-Segment-Displays verbunden sind
    int pinA = 2;
    int pinB = 3;
    int pinC = 4;
    int pinD = 5;
    int pinE = 6;
    int pinF = 7;
    int pinG = 8;

    // Definition des Pins, der mit dem Taster verbunden ist
    int buttonPin = 9;

    void setup() {
        // Setze alle Pins als Ausgänge
        pinMode(pinA, OUTPUT);
        pinMode(pinB, OUTPUT);
        pinMode(pinC, OUTPUT);
        pinMode(pinD, OUTPUT);
        pinMode(pinE, OUTPUT);
        pinMode(pinF, OUTPUT);
        pinMode(pinG, OUTPUT);

        // Setze den Taster-Pin als Eingang
        pinMode(buttonPin, INPUT);
    }

    void loop() {
        // Überprüfen, ob der Taster gedrückt wurde
        if (digitalRead(buttonPin) == HIGH) {
            // Warten, bis der Taster losgelassen wird, bevor es weitergeht
            while (digitalRead(buttonPin) == HIGH) {
                // Eine Zufallszahl zwischen 1 und 6 generieren
                int num = random(1, 7);

                // Die Zufallszahl auf dem 7-Segment-Display anzeigen
                displayDigit(num);
                // Kurze Verzögerung, um sichtbare Display-Aktualisierungen zu ermöglichen
                delay(100);
            }
            // Verzögerung hinzufügen, um den Taster zu entprellen und mehrere schnelle Eingaben zu verhindern
            delay(500);
        }
    }

    void displayDigit(int digit) {
        // Schalte alle Segmente aus
        digitalWrite(pinA, LOW);
        digitalWrite(pinB, LOW);
        digitalWrite(pinC, LOW);
        digitalWrite(pinD, LOW);
        digitalWrite(pinE, LOW);
        digitalWrite(pinF, LOW);
        digitalWrite(pinG, LOW);

        // Schalte die Segmente für die gewünschte Zahl ein (LOW schaltet die Segmente bei einer gemeinschaftlichen Kathode ein)
        switch (digit) {
            case 1:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            break;
            case 2:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 3:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 4:
            digitalWrite(pinB, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 5:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
            case 6:
            digitalWrite(pinA, HIGH);
            digitalWrite(pinC, HIGH);
            digitalWrite(pinD, HIGH);
            digitalWrite(pinE, HIGH);
            digitalWrite(pinF, HIGH);
            digitalWrite(pinG, HIGH);
            break;
        }
    }

8. Vergessen Sie nicht, Ihren Code zu speichern und Ihren Arbeitsplatz aufzuräumen.

**Zusammenfassung**

In dieser Lektion haben wir erfolgreich das Cyber Dice Projekt abgeschlossen, das Ihnen ermöglicht, freundschaftliche Wettkämpfe zu veranstalten, um zu sehen, wer die höchste Zahl würfeln kann. Während dieser Lektion haben wir die Funktionsweise eines 7-Segment-Displays erkundet und gelernt, wie man es effektiv ansteuert. Wir haben unseren Code durch die Verwendung von switch-case-Anweisungen vereinfacht, um die Lesbarkeit und Effizienz zu verbessern.

Darüber hinaus haben wir Logik implementiert, um die Anzeige von Zufallszahlen auf dem 7-Segment-Display basierend auf dem Zustand eines Tastendrucks zu steuern, was unserem Projekt eine dynamische Interaktion verleiht. Diese praktische Erfahrung macht Sie nicht nur mit grundlegenden elektronischen Komponenten und Codierungsstrategien vertraut, sondern zeigt auch praktische Anwendungen dieser Fähigkeiten bei der Erstellung von ansprechenden und interaktiven Projekten.

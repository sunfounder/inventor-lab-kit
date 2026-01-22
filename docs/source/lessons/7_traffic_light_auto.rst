.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Vorschauen.
    - **Sonderrabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und festlichen Aktionen teil.

    👉 Bereit, mit uns zu experimentieren und zu kreieren? Klicke auf [|link_sf_facebook|] und trete noch heute bei!


7. Lass uns Ampeln bauen!
==============================

.. .. image:: img/5_traffic_light_pic.png
..     :width: 400
..     :align: center

Willkommen zu dieser Lektion! Diese spannende Lektion überbrückt die Kluft zwischen theoretischen Konzepten und praktischer Anwendung in Elektronik und Programmierung. Wir werden den Prozess der Umwandlung von Pseudo-Code—einer vereinfachten Form einer Programmiersprache—in funktionale Arduino-Sketches erkunden. Diese Übung simuliert den Betrieb von Ampeln und bietet dir praktische Erfahrungen in der Programmierung und Schaltungsentwicklung. Während du lernst, Pseudo-Code zu interpretieren und umzusetzen, wirst du tiefere Einblicke in die Logik hinter der Steuerung elektronischer Geräte durch Code gewinnen.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/7_traffic_light.mp4" type="video/mp4">
        Dein Browser unterstützt das Video-Tag nicht.
    </video>

In dieser Lektion lernst du:

* Pseudo-Code zu schreiben und zu interpretieren, um die Funktionalität elektronischer Schaltungen zu planen.
* Pseudo-Code in Arduino-Sketches umzuwandeln, um Ampelsimulationen zu steuern.
* Ein Ampelsystem mit LEDs und einem Arduino-Board zu bauen und zu programmieren.

Durch das Beherrschen dieser Fähigkeiten wirst du in der Lage sein, grundlegende elektronische Systeme zu entwerfen, zu programmieren und zu warten und den Weg für komplexere Projekte zu ebnen.

Die Ampeln vorbereiten
------------------------------------------
Hey! Bereit, deine eigene Ampel mit einem Arduino zu erstellen? Hier ist, was wir brauchen:

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
   * - 1 * USB-Kabel
     - 1 * Breadboard
     - 3 * 220Ω Widerstände
     - Verbindungskabel
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_220ohm| 
     - |list_wire| 


**Schritt-für-Schritt Aufbau**

Lass uns alles zusammenbauen, wie bei einem LEGO-Set!

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

1. Schließe einen 220Ω Widerstand an das Breadboard an. Ein Ende sollte im negativen Anschluss und das andere Ende in Loch 1B stecken.

.. image:: img/7_traffic_light_resistor.png
    :width: 600
    :align: center

2. Füge eine grüne LED zum Breadboard hinzu. Die Anode der LED (langer Anschluss) sollte in Loch 1F und die Kathode (kurzer Anschluss) in Loch 1E stecken.

.. image:: img/7_traffic_light_green.png
    :width: 600
    :align: center

3. Verbinde die grüne LED mit Pin 3 des Arduino Uno R3 mit einem Kabel. Stecke ein Jumperkabel in Loch 1J und das andere Ende des Kabels in Pin 3 des Arduino Uno R3.

.. image:: img/7_traffic_light_pin3.png
    :width: 600
    :align: center

4. Nimm einen weiteren 220Ω Widerstand, verbinde ein Ende mit dem negativen Anschluss und das andere Ende mit Loch 6B.

.. image:: img/7_traffic_light_yellow_resistor.png
    :width: 600
    :align: center

5. Nimm eine gelbe LED. Die Anode der LED (langer Anschluss) sollte in Loch 6F und die Kathode (kurzer Anschluss) in Loch 6E stecken.

.. image:: img/7_traffic_light_yellow.png
    :width: 600
    :align: center

6. Verbinde die gelbe LED mit Pin 4 des Arduino Uno R3.

.. image:: img/7_traffic_light_pin4.png
    :width: 600
    :align: center

7. Verbinde die rote LED auf die gleiche Weise. Die rote LED ist mit Pin 5 des Arduino Uno R3 verbunden.

.. image:: img/7_traffic_light_red.png
    :width: 600
    :align: center

8. Oh! Wir haben fast vergessen, die Schaltung zu erden. Verbinde die negative Seite des Breadboards mit einem GND-Pin am Arduino Uno R3 mit einem schwarzen Kabel. Jetzt ist alles fertig!

.. image:: img/7_traffic_light.png
    :width: 600
    :align: center

.. note::

    Es gibt drei GND-Pins auf dem Arduino Uno R3. Du kannst jeden von ihnen verwenden; sie funktionieren alle auf die gleiche Weise.

Und so hast du eine komplette Ampelsteuerung! Jede farbige Lampe wird von ihrem eigenen Schalter auf dem R3 gesteuert und ist bereit, den Autos zu zeigen, wann sie stoppen, warten oder fahren sollen. Ist es nicht großartig, etwas zu bauen, das wie echte Ampeln funktioniert? Tolle Arbeit!

Pseudo-Code für eine Ampelschaltung schreiben
------------------------------------------------

Jetzt ist es an der Zeit, deinen LEDs einen Zweck zu geben. In dieser Aktivität programmierst du sie so, dass sie wie eine Ampel funktionieren und den Verkehrsfluss an einer belebten Kreuzung steuern.

Ampeln erfordern eine präzise Steuerung, um in einer festen Reihenfolge zwischen drei Farben zu wechseln, was dieses Projekt ideal für den Einstieg in die Arduino-Programmierung macht. Um unsere Ampel perfekt zu machen, müssen wir dem Arduino klar Anweisungen geben, was zu tun ist.

Die Kommunikation zwischen Menschen erfolgt durch Hören, Sprechen, Lesen, Schreiben, Gesten oder Mimik. Die Kommunikation mit Mikrocontrollern (wie dem auf deinem Arduino-Board) erfolgt durch das Schreiben von Code.

Wir können dem Arduino nicht einfach in natürlicher Sprache sagen: "Mach eine Ampel". Allerdings können wir natürliche Sprache verwenden, um einen "Pseudo-Code" zu schreiben, der bei der eigentlichen Arduino-Code-Entwicklung hilft.

.. note::
    
    Es gibt keine richtigen oder falschen Antworten beim Schreiben von Pseudo-Code. Je detaillierter dein Pseudo-Code ist, desto einfacher wird es sein, ihn in ein funktionierendes Programm umzuwandeln.

Überlege dir, was geschehen muss, damit deine Schaltung wie eine Ampel funktioniert. Schreibe den Pseudo-Code, der beschreibt, wie deine Ampel funktionieren soll, in deinem Logbuch auf. Verwende einfaches Englisch.

Hier sind einige Fragen, die dir beim Schreiben deines Pseudo-Codes helfen können:

* Sollten zwei oder mehr Lichter gleichzeitig eingeschaltet sein?
* Was ist die Reihenfolge der Lichter?
* Was passiert mit den anderen Lichtern, wenn eines eingeschaltet ist?
* Was passiert, nachdem das dritte Licht ausgegangen ist?
* Wie lange soll jedes Licht eingeschaltet bleiben?

Hier sind einige Beispiele für Pseudo-Code:

.. code-block::

    1) Setze alle LED-Pins auf Ausgang.
    2) Starte die Hauptschleife.
    a) Schalte alle Lichter aus.
    b) Schalte das grüne Licht für 10 Sekunden ein.
    c) Schalte alle Lichter aus.
    d) Schalte das gelbe Licht für 3 Sekunden ein.
    e) Schalte alle Lichter aus.
    f) Schalte das rote Licht für 10 Sekunden ein.
    3) Gehe zum Anfang der Schleife zurück.

.. code-block::

    Setup:
        Definiere alle LED-Pins als Ausgang.
    Hauptschleife:
        Schalte das grüne Licht ein.
        Schalte das rote und gelbe Licht aus.
        Warte 10 Sekunden.
        Schalte das gelbe Licht ein.
        Schalte das rote und grüne Licht aus.
        Warte 3 Sekunden.
        Schalte das rote Licht ein.
        Schalte das grüne und gelbe Licht aus.
        Warte 10 Sekunden.

Pseudo-Code hat kein strenges Format und ermöglicht es dir, deine Gedanken zu klären und logisch zu ordnen. Diese logische Reihenfolge wird als Algorithmus bezeichnet. Du verwendest täglich Algorithmen, ohne es vielleicht zu merken. Betrachte einen Algorithmus wie ein Rezept; in der Programmierung sind die Zutaten Schlüsselwörter und Befehle, und die Kochschritte sind der Algorithmus. Ein Algorithmus ist eine Reihe von Schritten oder Anweisungen. Wenn ein Algorithmus von Pseudo-Code in die Arduino-Programmiersprache übersetzt wird, gibt er dem Arduino-Board genau vor, was es wann tun soll.

.. note::
    
    Das Verwenden von Haftnotizen oder Karteikarten kann beim Schreiben von Pseudo-Code hilfreich sein. Schreibe jeden Schritt deines Algorithmus auf eine separate Notiz. Auf diese Weise kannst du die Schritte deines Algorithmus leicht neu anordnen, einfügen oder entfernen.

Pseudo-Code in einen Arduino-Sketch umwandeln
-------------------------------------------------

Es ist an der Zeit, den geschriebenen Code zu verfeinern und zusätzliche ``digitalWrite()``- und ``delay()``-Befehle hinzuzufügen. Hier ist eine Anleitung zur Strukturierung deines Codes: Deine Funktion ``void loop()`` sollte separate Segmente für die grünen, gelben und roten LEDs enthalten, die jeweils von einer spezifischen Verzögerungszeit gefolgt werden. Nicht alle Verzögerungen müssen gleich lang sein. Aktualisiere deine Codekommentare, um klarzustellen, was jede Zeile bewirkt.

1. Öffne den zuvor gespeicherten Sketch, ``Lesson6_Blink_LED``. Wähle „Speichern unter...“ aus dem Menü „Datei“ und benenne ihn in ``Lesson7_Traffic_Light`` um. Klicke auf "Speichern".

2. Setze nun gemäß unserem Pseudo-Code alle drei Pins in ``void setup()`` auf Ausgang. Kopiere den ``pinMode()``-Befehl zweimal, füge ihn darunter ein und passe die Pinnummern für jeden Pin an.

    .. code-block:: Arduino
        :emphasize-lines: 4,5

        void setup() {
            // Setup-Code hier, der einmal ausgeführt wird:
            pinMode(3, OUTPUT); // Setze Pin 3 auf Ausgang
            pinMode(4, OUTPUT); // Setze Pin 4 auf Ausgang
            pinMode(5, OUTPUT); // Setze Pin 5 auf Ausgang
        }

3. In ``void loop()``, schalte zuerst die grüne LED ein und schalte die anderen beiden LEDs aus. Kopiere also die ``digitalWrite()``-Befehle zweimal, passe die Pinnummern auf 4 und 5 an, ändere ``HIGH`` in ``LOW`` für die LEDs, die du ausschalten möchtest, und aktualisiere die Kommentare entsprechend dem aktuellen Szenario. Der modifizierte Code sieht wie folgt aus:

    .. code-block:: Arduino
        :emphasize-lines: 4,5

        void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // Schalte die LED an Pin 3 ein
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
            delay(3000);           // Warte 3 Sekunden
        }

4. Vielleicht möchtest du die grüne LED länger eingeschaltet lassen. In unserem Ampelsystem könnte das etwa eine Minute dauern, aber hier simulieren wir es mit 10 Sekunden.

    .. code-block:: Arduino
        :emphasize-lines: 6

        void loop() {
            // Hauptcode, der wiederholt ausgeführt wird:
            digitalWrite(3, HIGH);  // Schalte die LED an Pin 3 ein
            digitalWrite(4, LOW);   // Schalte die LED an Pin 4 aus
            digitalWrite(5, LOW);   // Schalte die LED an Pin 5 aus
            delay(10000);           // Warte 10 Sekunden
        }

5. Jetzt lass die gelbe LED aufleuchten und schalte die anderen beiden LEDs aus. Kopiere erneut die 4 Zeilen aus ``void loop()``, setze Pin 4 auf HIGH und die anderen auf LOW. Ändere die Verzögerung für die gelbe LED auf 3 Sekunden.

    .. code-block:: Arduino
        :emphasize-lines: 7-10

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
        }

6. Schließlich lass die rote LED für 10 Sekunden aufleuchten und schalte die anderen beiden LEDs aus. Dein vollständiger Code sieht wie folgt aus:

    .. code-block:: Arduino

        void setup() {
            // Setup-Code hier, der einmal ausgeführt wird:
            pinMode(3, OUTPUT); // Setze Pin 3 auf Ausgang
            pinMode(4, OUTPUT); // Setze Pin 4 auf Ausgang
            pinMode(5, OUTPUT); // Setze Pin 5 auf Ausgang
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

**Frage**

Schau dir die Kreuzungen in deiner Umgebung an. Wie viele Ampeln gibt es normalerweise? Wie werden sie miteinander koordiniert?

**Zusammenfassung**

Herzlichen Glückwunsch zum Abschluss von Lektion 7! Du hast es geschafft, Pseudo-Code in ein voll funktionsfähiges, Arduino-gesteuertes Ampelsystem umzusetzen. Hier ist eine kurze Zusammenfassung dessen, was du erreicht hast:

* Beherrschung des Pseudo-Codes: Du hast gelernt, Pseudo-Code zu verwenden, um die Funktionsweise elektronischer Systeme zu skizzieren, was dein logisches Denken und deine Planungsfähigkeiten verbessert.
* Vom Pseudo-Code zum echten Code: Du hast erfahren, wie ein strukturierter Ansatz im Pseudo-Code zu einer effektiven und genauen Arduino-Programmierung führt.
* Praktische Anwendung: Durch den Aufbau und die Programmierung eines Ampelsystems hast du die praktische Anwendung deines Wissens demonstriert und gezeigt, wie Software direkt Hardware steuert.

Diese Lektion hat sowohl deine technischen Fähigkeiten als auch dein analytisches Denken geschärft und dich für komplexere Projekte in der Elektronik und Programmierung gerüstet. Baue weiter auf diesen Fähigkeiten auf, um weitere Möglichkeiten in der Technologieintegration zu erschließen!


.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein und tausche dich mit anderen Enthusiasten aus.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezielle Rabatte**: Profitiere von exklusiven Rabatten auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und Sonderaktionen zu Feiertagen teil.

    👉 Bereit, gemeinsam mit uns zu entdecken und zu erschaffen? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

.. _onoff_desk_lamp:

18. EIN/AUS-Schreibtischlampe
====================================

Willkommen zu unserem praktischen Tutorial, in dem du lernst, wie du eine schaltbare Schreibtischlampe mit einem Relais und einem Arduino Uno R3 baust. Dieses Projekt simuliert reale Anwendungen von Relais zur Steuerung von Hochleistungsgeräten durch Niederspannungssteuerungssysteme.

.. .. image:: img/10_desk_lamp_button.jpg
..     :width: 500
..     :align: center

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/18_on_off_lamp.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Aus Sicherheitsgründen werden wir keine Hochleistungsleuchte direkt mit dem Lastanschluss des Relais verbinden, sondern eine LED verwenden, um das Ein- und Ausschalten der Lampe durch Drücken des Knopfes zu simulieren.

Am Ende dieser Lektion wirst du in der Lage sein:

* Das Relaismodul mit einem Arduino zu verstehen und zu bedienen.
* Sicherheitsmaßnahmen für die Steuerung von Hochstromlasten zu implementieren.
* Den Modus ``INPUT_PULLUP`` für eine effiziente Tastensteuerung zu nutzen.
* Zustandsänderungen zu erkennen, um Ausgaben reaktionsschnell zu steuern.


Das Relaismodul verstehen
-------------------------------------------

Finde das Relaismodul.

Relais sind elektrisch betriebene Schalter, die dafür ausgelegt sind, einen kleinen Strom zu nutzen, um einen viel größeren zu steuern. Diese Fähigkeit macht sie ideal für die Verbindung von Niederspannungssteuerungssystemen, wie sie in Arduino-Platinen (normalerweise im Bereich von 3,3V bis 5V) zu finden sind, mit Hochspannungsgeräten. In den meisten Wohn- und Büroumgebungen, in denen Standardspannungen zwischen 110V und 240V liegen, bieten Relaismodule eine praktische Lösung zur sicheren Steuerung dieser höheren Spannungen.

.. image:: img/10_relay_module.png
    :width: 300
    :align: center

Der Aufbau eines Relais umfasst typischerweise einen Elektromagneten, einen Anker, eine Feder und ein Paar Kontaktpunkte. Der Elektromagnet entsteht durch eine Spule, die um einen Eisenkern gewickelt ist. Wenn die Spule stromlos ist, verliert der Elektromagnet seine Magnetkraft, lässt den Anker los und stellt eine Verbindung zwischen den Kontaktpunkten Normal geschlossen (NC) und Common (COM) her.

.. image:: img/10_relay_nc.jpg
    :width: 500
    :align: center

* **NC**: Normal geschlossen. Standardmäßig mit dem COM-Pin verbunden, wenn nicht aktiviert.
* **COM**: Gemeinsamer Pin
* **NO**: Normal offen. Standardmäßig vom COM-Pin getrennt, wenn nicht aktiviert.
* **Spulenpin**: Diese sind die Anschlüsse an beiden Enden der Spule und haben keine Richtung.

Wenn die Spule aktiviert wird, erzeugt der Elektromagnet ein Magnetfeld, das den Anker anzieht und die Metallkontaktpunkte zwischen COM und NO verbindet. Sobald die Spule stromlos ist, zieht die Federspannung die Kontakte von COM und NC wieder zusammen.

.. image:: img/10_relay_no.jpg
    :width: 500
    :align: center

Das Relaismodul besteht aus einem Relais, einem Transistor, einer LED, einem Widerstand und drei Schraubklemmen, die auf einer Leiterplatte (PCB) montiert sind. Hier ist eine kurze Beschreibung der Pins des Moduls:

.. image:: img/10_relay_pinout.jpg
    :width: 500
    :align: center

* **-**: GND
* **+**: VCC
* **S**: Signal-Pin, wird verwendet, um dieses Relais zu steuern. Eingang Hoch und das Relais schließt, Eingang Niedrig und das Relais öffnet.
* **COM**: Gemeinsamer Pin
* **NC**: Normal geschlossen
* **NO**: Normal offen

Das Schaltbild des Moduls sieht folgendermaßen aus:

Wenn ein hohes Signal an den **S**-Pin angelegt wird, passiert es die Kontrollleuchte und den Strombegrenzungswiderstand und schaltet den NPN-Transistor ein. Dieser Strom aktiviert die Spule des Relais, erzeugt ein Magnetfeld, das den Anker anzieht, wodurch ein "Klick"-Geräusch entsteht und die COM- und NO-Anschlüsse verbunden werden, wodurch der Stromkreis geschlossen wird.

.. image:: img/10_relay_circuit.png
    :width: 600
    :align: center


Baue die Schaltung
------------------------------------
Jetzt bauen wir eine Schaltung, um eine LED zu steuern und das Funktionsprinzip des Relaismoduls zu erkunden.

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Rote LED
     - 1 * 220Ω Widerstand
     - 1 * Relaismodul
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm|  
     - |list_relay_module| 
   * - 1 * Knopf
     - 1 * USB-Kabel
     - 1 * Steckbrett
     - Jumperkabel
   * - |list_button| 
     - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire|


**Aufbauschritte**

Normalerweise könntest du ein Relais verwenden, um deine Heimlampe so umzubauen, dass sie programmatisch gesteuert werden kann.

    .. warning::

        Versuche diese Modifikation nicht ohne vorherige elektrische Kenntnisse, da sie den Umgang mit 220V Spannung erfordert, die äußerst gefährlich ist.

.. image:: img/10_relay_lamp.jpg
    :width: 600
    :align: center

Aus Sicherheitsgründen verwenden wir in diesem Kurs eine LED, um eine Hochlast zu simulieren. Folge dem Schaltplan oder den untenstehenden Schritten, um deine Schaltung aufzubauen.

.. image:: img/10_relay_led.png
    :width: 500
    :align: center

1. Verbinde auf dem Steckbrett den 5V-Anschluss des Arduino Uno R3 mit der positiven Schiene des Steckbretts und GND mit der negativen Schiene.

.. image:: img/10_relay_led_power.png
    :width: 600
    :align: center

2. Verbinde den S-Pin des Relaismoduls mit Pin 2 des Arduino Uno R3. Verbinde die "+"- und "-" Pins mit der positiven bzw. negativen Schiene des Steckbretts.

.. image:: img/10_relay_led_relay_module.png
    :width: 600
    :align: center

3. Normalerweise wird der COM-Anschluss des Relaismoduls an eine externe Stromquelle angeschlossen, aber für diese Lektion stecke ihn einfach in die positive Schiene des Steckbretts, um eine LED zu beleuchten.

.. image:: img/10_relay_led_relay_com.png
    :width: 600
    :align: center

4. Setze eine rote LED auf das Steckbrett, wobei die Anode in Loch 41E und die Kathode in Loch 40E steckt.

.. image:: img/10_relay_led_led.png
    :width: 600
    :align: center

5. Verbinde nun die Kathode der LED mit GND.

.. image:: img/10_relay_led_gnd.png
    :width: 600
    :align: center

6. Setze einen 220Ω-Widerstand zwischen die Löcher 41C und 45C, um als Strombegrenzungswiderstand für die Anode der LED zu dienen.

.. image:: img/10_relay_led_resistor.png
    :width: 600
    :align: center

7. Verbinde Loch 45A mit dem NO-Anschluss des Relaismoduls mit einem Jumperkabel.

.. image:: img/10_relay_led.png
    :width: 600
    :align: center

8. Setze einen Taster zwischen die Löcher 13E, 13F, 15E und 15F auf dem Steckbrett.

.. image:: img/10_relay_led_button_wire.png
    :width: 600
    :align: center

9. Verbinde abschließend ein Jumperkabel von 13A zur negativen Schiene und ein weiteres von 15A zu Pin 7.

.. image:: img/10_relay_led_button.png
    :width: 600
    :align: center


**Test des Relaismoduls**

Nun verwende ein Multimeter, um die Durchgangsspannung zwischen COM, NO und NC zu messen und das Funktionsprinzip des Relaismoduls zu überprüfen.

1. Stelle das Multimeter auf **Durchgang** ein, die Einstellung mit dem Diodensymbol und einem Lautsprechersymbol dient zur Messung des Durchgangs.

.. image:: img/multimeter_diode.png
    :width: 300
    :align: center

2. Berühre die Prüfspitzen des Multimeters an den COM- und NC-Anschlüssen des Relaismoduls, du wirst einen "Piep"-Ton vom Multimeter hören, was anzeigt, dass diese beiden Anschlüsse verbunden sind.

.. image:: img/10_relay_led_com_nc.png
    :width: 600
    :align: center

3. Trage die Messergebnisse in die untenstehende Tabelle ein.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Zustand
     - NO oder NC verbunden mit dem COM-Anschluss?
   * - Standard
     - *NC*
   * - S-Pin Hoch
     - 

4. Verbinde den S-Pin des Relaismoduls mit der positiven Schiene des Steckbretts. Du wirst ein "Klick"-Geräusch hören und die Signal-LED am Relaismodul sowie die Last-LED leuchten auf.

.. image:: img/10_relay_led_s_5v.png
    :width: 600
    :align: center

5. Berühre erneut die Prüfspitzen des Multimeters an den COM- und NO-Anschlüssen des Relaismoduls, du wirst einen "Piep"-Ton vom Multimeter hören, was anzeigt, dass diese beiden Anschlüsse verbunden sind.

.. image:: img/10_relay_led_com_no.png
    :width: 600
    :align: center

6. Trage die Messergebnisse in die untenstehende Tabelle ein.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Zustand
     - NO oder NC verbunden mit dem COM-Anschluss?
   * - Standard
     - *NC*
   * - S-Pin Hoch
     - *NO*

Diese Tests bestätigen, dass das Relaismodul durch ein hohes Signal aktiviert wird. Wenn der S-Pin ein hohes Signal erhält, bewirkt dies, dass die COM- und NO-Anschlüsse verbunden werden, wodurch die Schaltung in der Lage ist, Hochleistungslasten effektiv zu steuern.

Codeerstellung
---------------------------------

Lass uns nun den Code schreiben, um den Zustand des Relaismoduls mithilfe eines Tastendrucks umzuschalten. Auf diese Weise kannst du sehen, wie das Relais schließt und die LED aufleuchtet, wenn du den Knopf drückst, und das Relais öffnet sich wieder und die LED erlischt, wenn du den Knopf erneut drückst. Dieser Vorgang wiederholt sich kontinuierlich.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „New Sketch“ im „File“-Menü auswählst.
2. Speichere dein Sketch unter dem Namen ``Lesson18_Desk_Lamp_Relay`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Initialisiere die Pins, die mit dem Taster und dem Relaismodul verbunden sind. In Lektion 8 haben wir einen Taster mit einem manuell verbundenen 10K Pull-Down-Widerstand zwischen GND und dem Taster verwendet. In dieser Schaltung haben wir jedoch keinen Widerstand angeschlossen. Stattdessen nutzen wir die Software-Pull-Up-Funktion des Arduino. Du musst den Pin, der mit dem Taster verbunden ist, als Eingang festlegen und gleichzeitig auf ``PULLUP`` setzen.

.. code-block:: Arduino
    :emphasize-lines: 6

    int potValue = 0;

    void setup() {
        // Setup-Code wird einmal ausgeführt:
        pinMode(2, OUTPUT);        // Setze Pin 2 als Ausgang
        pinMode(7, INPUT_PULLUP);  // Setze Pin 7 als Eingang mit internem Pull-Up-Widerstand
    }

4. Bevor du die ``void loop()`` betrittst, müssen wir auch zwei Variablen erstellen, um die Zustände des Tasters und des Relaismoduls zu initialisieren. Der Anfangszustand des Relais ist LOW. Da der Taster einen internen Pull-Up-Widerstand verwendet, wird er als HIGH gelesen, wenn er nicht gedrückt wird.

.. code-block:: Arduino
    :emphasize-lines: 1,2

    int relayState = LOW;          // Anfangszustand des Relais
    int lastButtonState = HIGH;  // Die letzte bekannte Lesung vom Eingangs-Pin

    void setup() {
        pinMode(2, OUTPUT);        // Setze Pin 2 als Ausgang
        pinMode(7, INPUT_PULLUP);  // Setze Pin 7 als Eingang mit internem Pull-Up-Widerstand
    }

5. Nun liest du in der ``void loop()``-Funktion zunächst den Zustand des Tasters mit ``digitalRead()`` und speicherst ihn in der Variable ``buttonState``.

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int buttonState = digitalRead(7);  // Lies den Zustand des Tasters
    }

6. Beginnen wir mit der Kernfunktion, die den Tastendruck überwacht.

Zuvor haben wir gelernt, wie man erkennt, ob ein Taster gedrückt wird, indem man seinen Zustand als ``HIGH`` oder ``LOW`` liest. Diese Lektion zielt jedoch darauf ab, auf einen einzelnen Tastendruck zu reagieren, ohne dass der Taster gedrückt gehalten werden muss. Dazu müssen wir eine Zustandsänderung des Tasters erkennen.

Um dies zu erreichen, verwenden wir eine ``if``-Anweisung, die den vorherigen Zustand des Tasters (``lastButtonState``) mit dem aktuellen Zustand (``buttonState``) vergleicht. Der logische Operator ``&&`` wird hier verwendet, was bedeutet, dass beide Bedingungen erfüllt sein müssen, damit der Codeblock innerhalb der ``if``-Anweisung ausgeführt wird.

.. code-block:: Arduino
    :emphasize-lines: 4

    void loop() {
        int buttonState = digitalRead(7);  // Lies den Zustand des Tasters
        // Überprüfe, ob sich der Tasterzustand seit der letzten Schleifeniteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Tastendruck erkannt
        }
    }

7. Wenn ein Tastendruck erkannt wird, schalten wir den Zustand des Relais um. Das bedeutet, wenn das Relais ausgeschaltet war, wird es eingeschaltet, und wenn es eingeschaltet war, wird es ausgeschaltet. Der Operator ``!`` wird verwendet, um den Zustand der Variablen ``relayState`` zu invertieren.

.. code-block:: Arduino
    :emphasize-lines: 5

    void loop() {
        int buttonState = digitalRead(7);  // Lies den Zustand des Tasters
        // Überprüfe, ob sich der Tasterzustand seit der letzten Schleifeniteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Tastendruck erkannt
            relayState = !relayState;                               // Zustand des Relais umschalten
        }
    }

8. Verwende dann die Funktion ``digitalWrite()``, um ``relayState`` auf Pin 2 zu schreiben.

.. code-block:: Arduino
    :emphasize-lines: 6

    void loop() {
        int buttonState = digitalRead(7);  // Lies den Zustand des Tasters
        // Überprüfe, ob sich der Tasterzustand seit der letzten Schleifeniteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Tastendruck erkannt
            relayState = !relayState;                               // Zustand des Relais umschalten
            digitalWrite(2, relayState);                        // Setze den Zustand des Relais
        }
    }

9. Nachdem der Tasterzustand überprüft und das Relais entsprechend aktualisiert wurde, müssen wir den aktuellen Zustand des Tasters als neuen 'letzten bekannten Zustand' speichern. Dieser Schritt ist entscheidend, um die nächste Zustandsänderung zu erkennen.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        int buttonState = digitalRead(7);  // Lies den Zustand des Tasters
        // Überprüfe, ob sich der Tasterzustand seit der letzten Schleifeniteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Tastendruck erkannt
            relayState = !relayState;                           // Zustand des Relais umschalten
            digitalWrite(2, relayState);                        // Setze den Zustand des Relais
        }
        lastButtonState = buttonState;  // Aktualisiere lastButtonState auf den aktuellen Zustand
        delay(200);                     // Optional: Einfache Software-Entprellung
    }

10. Dein vollständiger Code lautet wie folgt. Du kannst nun auf die **Upload**-Schaltfläche klicken, um den Code auf den Arduino Uno R3 hochzuladen.

Nachdem der Code erfolgreich hochgeladen wurde, schließt das Relais beim Drücken des Knopfes mit einem „Klick“-Geräusch, und die Kontrollleuchte auf dem Relaismodul sowie die externe LED leuchten auf. Drücke den Knopf erneut, und du hörst dasselbe „Klick“-Geräusch, die Kontrollleuchte und die LED erlöschen. Dieser Zyklus wiederholt sich.

.. code-block:: Arduino

    int relayState = LOW;        // Anfangszustand des Relaismoduls
    int lastButtonState = HIGH;  // Die letzte bekannte Lesung vom Eingangs-Pin

    void setup() {
        pinMode(2, OUTPUT);        // Setze Pin 2 als Ausgang
        pinMode(7, INPUT_PULLUP);  // Setze Pin 7 als Eingang mit internem Pull-Up-Widerstand
    }

    void loop() {
        int buttonState = digitalRead(7);  // Lies den Zustand des Tasters
        // Überprüfe, ob sich der Tasterzustand seit der letzten Schleifeniteration geändert hat
        if (lastButtonState == HIGH && buttonState == LOW) {  // Tastendruck erkannt
            relayState = !relayState;                           // Zustand des Relais umschalten
            digitalWrite(2, relayState);                        // Setze den Zustand des Relais
        }
        lastButtonState = buttonState;  // Aktualisiere lastButtonState auf den aktuellen Zustand
        delay(200);                     // Optional: Einfache Software-Entprellung
    }

11. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.


**Frage**

1. Was würde passieren, wenn du den digitalen Pin 7 nur auf INPUT setzen würdest? Warum?

.. code-block::
    :emphasize-lines: 3

    void setup() {
        pinMode(9, OUTPUT);        // Setze Pin 9 als Ausgang
        pinMode(7, INPUT);  // Setze Pin 7 als Eingang ohne internen Pull-Up-Widerstand
        Serial.begin(9600);        // Serielle Kommunikation auf 9600 Baudrate einrichten
    }

2. Wenn Pin 7 nur auf ``INPUT`` gesetzt ist, welche Anpassungen müssten an der Schaltung vorgenommen werden?

**Zusammenfassung**

In diesem Kurs hast du eine Schaltung mit einem relaisgesteuerten System aufgebaut, das eine Schreibtischlampe simuliert, wobei eine LED als Stellvertreter für Hochlasten verwendet wird. Das Projekt beinhaltete den Aufbau einer Schaltung auf einem Steckbrett, das Verdrahten von Komponenten und das Programmieren eines Arduino zur Steuerung des Relais basierend auf Tastereingaben. Durch Tests mit einem Multimeter hast du die Funktionalität des Relaismoduls überprüft und dessen Betrieb unter verschiedenen Signalbedingungen verstanden.

Der Codeerstellungsabschnitt verstärkte das Konzept von Zustandsänderungen und die Verwendung von bedingter Logik zur Steuerung physischer Geräte durch Programmierung. Durch den Abschluss dieses Kurses hast du dein Verständnis sowohl der theoretischen als auch der praktischen Aspekte der Verwendung von Relais in elektronischen Projekten vertieft und bist nun in der Lage, diese Konzepte auf komplexere und vielfältigere Anwendungen in der Zukunft anzuwenden.

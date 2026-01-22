.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche gemeinsam mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum mitmachen?**

    - **Experten-Support**: Lösen Sie nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Tutorials aus, um Ihre Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und Sneak Peeks.
    - **Spezielle Rabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nehmen Sie an Verlosungen und saisonalen Aktionen teil.

    👉 Bereit, mit uns zu erkunden und zu kreieren? Klicken Sie auf [|link_sf_facebook|] und treten Sie noch heute bei!

9. Dimmbare Schreibtischlampe
=============================================

Stell dir jede Schreibtischlampe zu Hause vor, die sanft Licht über deine abendlichen Lektüren oder nächtlichen Projekte wirft. Hast du dich jemals gefragt, wie diese Lampen es schaffen, ihre Helligkeit so nahtlos anzupassen? In dieser Lektion tauchen wir in die Mechanik und Elektronik hinter einer Schreibtischlampe ein und verwandeln Neugier in Wissen, indem wir eine von Grund auf mit Arduino bauen.

.. .. image:: img/9_desk_lamp_pot.jpg
..     :width: 500
..     :align: center

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/9_dimmble_led.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>
    
Mach dich bereit:

* Die Rolle von Variablen beim Speichern und Manipulieren von Daten in Arduino-Sketches zu verstehen.
* Das Lesen analoger Signale mit ``analogRead()`` zu meistern.
* PWM (Pulsweitenmodulation) durch ``analogWrite()`` zu erkunden, um die Helligkeit einer LED fein einzustellen.

Am Ende dieser Lektion wirst du nicht nur eine voll funktionsfähige elektronische Schreibtischlampe gebaut haben, sondern auch ein tieferes Verständnis dafür gewonnen haben, wie Software mit Hardware interagiert, um alltägliche Objekte zum Leben zu erwecken. Lass uns unser Wissen erhellen, indem wir eine Schreibtischlampe bauen, die auf deine Berührung reagiert.


Schalte den Stromkreis ein
------------------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Rote LED
     - 1 * 220Ω Widerstand
     - 1 * Potentiometer
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_potentiometer| 
   * - 1 * USB-Kabel
     - 1 * Breadboard
     - Jumperkabel
     - 1 * Multimeter
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_meter|

**Schritt-für-Schritt Aufbau**

1. Finde ein Potentiometer.

Ein Potentiometer, oft auch als „Poti“ bezeichnet, fungiert als verstellbarer Widerstand. Das bedeutet, dass es seinen Widerstand von fast Null bis zu seinem maximalen Wert einstellen kann. Die meisten Potentiometer sind mit ihrem Widerstandsbereich markiert. Das in deinem Kit enthaltene Potentiometer ist als 103 (10K) Potentiometer gekennzeichnet, was 10 Kiloohm oder 10.000 Ohm entspricht.

.. image:: img/9_dimmer_pot.png
    :width: 200
    :align: center

Im Inneren des Potentiometers befindet sich ein Streifen aus Widerstandsmaterial mit einem Schieberegler, der sich entlang des Streifens bewegt. Jedes Ende des Widerstandsmaterials ist mit einem Anschluss oder Pin verbunden, die unten als Pins A und B dargestellt sind. Der Widerstand zwischen den Pins A und B ist fest und stellt den maximalen Widerstand dar, den das Potentiometer bieten kann. Für die Potentiometer in deinem Kit beträgt der maximale Widerstand 10 Kiloohm.

.. image:: img/9_dimmer_pot_2.png
    :width: 400
    :align: center

* **A**: Verbinde mit der Stromversorgung
* **B**: Verbinde mit der Masse (GND)
* **C**: Verbinde mit dem analogen Pin
* **D**: Schieberegler
* **E**: Widerstandsband

Der Pin C ist mit dem Schieberegler verbunden. Der Widerstand über den Schieberegler oder Pin C hängt von der Position des Schiebers entlang des Widerstandsmaterials ab.

.. image:: img/9_dimmer_pot_3.png
    :width: 400
    :align: center

In Schaltplänen sieht das Symbol für ein Potentiometer typischerweise wie ein Widerstand mit einem Pfeil durch die Mitte aus.

.. image:: img/9_dimmer_pot_4.png
    :width: 200
    :align: center


Lass uns nun erkunden, wie das Potentiometer den Widerstand in einem Stromkreis anpasst.

2. Schließe ein Potentiometer an das Breadboard an. Stecke seine drei Pins in die Löcher 30G, 29F, 28G.

.. note::
    Das Potentiometer ist mit „P 103“ beschriftet, was auf seinen Widerstandsbereich hinweist. Bitte stecke das Potentiometer wie abgebildet in das Breadboard, mit der beschrifteten Seite zu dir gewandt.

.. image:: img/9_dimmer_test_pot.png
    :width: 500
    :align: center


3. Um den Widerstand des Potentiometers zu messen, musst du ein Kabel in 29J einstecken und dann mit dem roten Messkabel berühren, sowie ein weiteres Kabel in 28J einstecken und mit dem schwarzen Messkabel berühren.

.. image:: img/9_dimmer_test_wore.png
    :width: 500
    :align: center

4. Stelle das Multimeter auf den Messbereich für Widerstände im Bereich von 20 Kiloohm (20K) ein.

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

5. Drehe das Potentiometer in die Position „1“, wie im Diagramm angegeben.

.. image:: img/9_pot_direction.png
    :width: 300
    :align: center
    
6. Notiere die gemessenen Widerstandswerte in der Tabelle.

.. note::
    Die Werte in der Tabelle sind meine Messwerte; deine Ergebnisse können abweichen. Fülle sie entsprechend deinen tatsächlichen Ergebnissen aus.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Messpunkt
     - Widerstand (Kiloohm)
   * - 1
     - *1,52*
   * - 2
     -
   * - 3
     -

7. Drehe das Potentiometer im Uhrzeigersinn in die Positionen 2 und 3, um den Widerstand an jedem Punkt zu messen und trage die Ergebnisse in die Tabelle ein.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Messpunkt
     - Widerstand (Kiloohm)
   * - 1
     - *1,52*
   * - 2
     - *5,48*
   * - 3
     - *9,01*

Aus den Messergebnissen:

* Wenn du das Potentiometer **im Uhrzeigersinn** von Position 1 zu Position 3 drehst, erhöht sich der Widerstand zwischen den Positionen 2 und 1.
* Umgekehrt verringert sich der Widerstand zwischen den Positionen 2 und 1, wenn du **gegen den Uhrzeigersinn** von Position 3 zu Position 1 drehst.

8. Stecke das andere Ende des Kabels von 28J in den negativen Anschluss des Breadboards.

.. image:: img/9_dimmer_led1_pot_gnd.png
    :width: 500
    :align: center

9. Dann stecke das andere Ende des Kabels von 29J in den A0-Pin des Arduino Uno R3.

.. image:: img/9_dimmer_led1_pot_a0.png
    :width: 500
    :align: center

10. Verbinde schließlich das Potentiometer mit 5V, indem du ein Jumperkabel zwischen Loch 30J auf dem Breadboard und dem 5V-Pin des Arduino Uno R3 einsteckst.

.. image:: img/9_dimmer_led1_pot_5v.png
    :width: 500
    :align: center


11. Verbinde den GND-Pin des Arduino Uno R3 mit dem negativen Anschluss des Breadboards mit einem langen Jumperkabel.

.. image:: img/9_dimmer_led1_gnd.png
    :width: 500
    :align: center

12. Nimm eine LED heraus. Stecke ihre Anode (längerer Pin) in Loch 13A und ihre Kathode (kürzerer Pin) in den negativen Anschluss des Breadboards.

.. image:: img/9_dimmer_led1_led.png
    :width: 500
    :align: center

13. Platziere einen 220 Ohm-Widerstand zwischen den Löchern 13E und 13G.

.. image:: img/9_dimmer_led1_resistor.png
    :width: 500
    :align: center

14. Verbinde Loch 13J auf dem Breadboard mit Pin 9 auf dem Arduino Uno R3 mit einem Kabel.

.. image:: img/9_dimmer_led1_pin9.png
    :width: 500
    :align: center


**Frage**

Wie denkst du, dass sich die Spannung an A0 ändert, wenn das Potentiometer im Uhrzeigersinn und gegen den Uhrzeigersinn gedreht wird?


Code-Erstellung
-------------------------------------

In dieser Lektion wollen wir die Helligkeit der LED basierend auf der Drehung des Potentiometers anpassen.

Hier könnte der Pseudocode so aussehen:

.. code-block::

    Erstelle eine Variable, um die Eingabewerte zu speichern.
    Setze einen Pin als Ausgang.
    Beginne die Hauptschleife:
        Speichere den Wert des Potentiometers in einer Variablen.
        Setze die LED-Helligkeit basierend auf der Potentiometer-Variablen.
    Ende der Hauptschleife.

**Pin-Initialisierung**

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „New Sketch“ aus dem Menü „File“ auswählst.
2. Speichere deinen Sketch als ``Lesson9_Desk_Lamp`` durch Drücken von ``Strg + S`` oder Klicken auf „Speichern“.

3. Die LED in deinem Schaltkreis ist an einen digitalen Pin des Arduino Uno R3 angeschlossen und als Ausgang definiert. Vergiss nicht, einen Kommentar hinzuzufügen.

.. note::

    Das Potentiometer ist ein analoges Eingabegerät und ist an den analogen Pin A0 angeschlossen. Alle analogen Pins auf Arduino sind Eingabepins, was bedeutet, dass sie nicht wie digitale Pins als INPUT deklariert werden müssen.
    
.. code-block:: Arduino
    :emphasize-lines: 3

    void setup() {
        // Füge deinen Setup-Code hier ein, um ihn einmal auszuführen:
        pinMode(9, OUTPUT);  // Setze Pin 9 als Ausgang
    }

    void loop() {
        // Füge deinen Hauptcode hier ein, um ihn wiederholt auszuführen:
    }

**Variablendeklaration**

Um die LED mit einem Potentiometer zu dimmen, benötigst du eine **Variable**, um den Wert des Potentiometers zu speichern.

Tauchen wir in das Konzept von Variablen in der Programmierung ein. Eine Variable fungiert wie ein Container in deinem Programm, in dem du Informationen speichern und später abrufen kannst.

.. image:: img/9_variable_define.png
    :width: 400
    :align: center

Bevor eine Variable verwendet werden kann, muss sie deklariert werden, was als Variablendeklaration bekannt ist.

Um eine Variable zu deklarieren, musst du ihren Typ und Namen definieren. Es ist nicht notwendig, der Variablen sofort einen Wert zuzuweisen – dies kannst du später in deinem Sketch tun. Hier ist ein Beispiel, wie man eine Variable deklariert:

.. code-block:: Arduino

    int var;

Hier ist ``int`` der Datentyp für Ganzzahlen, der Werte von -32768 bis 32767 speichern kann. Variablen können verschiedene Datentypen speichern, einschließlich ``float``, ``byte``, ``boolean``, ``char`` und ``string``.

Variablennamen können beliebig gewählt werden, wie z.B. ``i``, ``apple``, ``Bruce``, ``R2D2`` oder ``Sectumsempra``. Es gibt jedoch Regeln für die Namensgebung:

* Namen können Buchstaben, Ziffern und Unterstriche enthalten, aber keine Leerzeichen oder Sonderzeichen wie !, #, %, usw.

  .. image:: img/9_variable_name1.png
    :width: 400
    :align: center

* Namen müssen mit einem Buchstaben oder einem Unterstrich (_) beginnen. Sie können nicht mit einer Zahl beginnen.

  .. image:: img/9_variable_name2.png
    :width: 400
    :align: center

* Namen sind groß- und kleinschreibungsempfindlich. ``myCat`` und ``mycat`` würden als unterschiedliche Variablen angesehen werden.

* Vermeide die Verwendung von Schlüsselwörtern, die die Arduino IDE erkennt und hervorhebt, wie ``int``, das speziell farblich markiert wird. Wenn der Name eine Farbe wie Orange oder Blau annimmt, handelt es sich um ein Schlüsselwort und sollte nicht als Variablenname verwendet werden.

Der Geltungsbereich einer Variablen bestimmt, wo sie in deinem Sketch verwendet werden kann, basierend auf ihrer Deklaration.

* Eine Variable, die außerhalb aller Funktionen (d.h. außerhalb von Klammern) deklariert wird, ist eine globale Variable und kann überall in deinem Sketch verwendet werden.
* Eine Variable, die innerhalb einer Funktion (innerhalb einer Reihe von Klammern) deklariert wird, ist eine lokale Variable und kann nur innerhalb dieser Funktion verwendet werden.

.. code-block:: Arduino
    :emphasize-lines: 1,4,9

    int global_variable = 0; // Dies ist eine globale Variable

    void setup() {
        int variable = 0; // Dies ist eine lokale Variable
    }

    void loop() {
        int variable = 0; // Dies ist eine andere lokale Variable
    }

.. note::

    Lokale Variablen können nur innerhalb der Funktionen verwendet werden, in denen sie deklariert sind. Das bedeutet, dass du Variablen mit demselben Namen in verschiedenen Funktionen deklarieren kannst, ohne Probleme zu bekommen. Es wird jedoch empfohlen, denselben Namen für lokale und globale Variablen zu vermeiden, um Verwechslungen zu verhindern.

Typischerweise sollte ein Arduino-Sketch einem konsistenten Muster folgen: Globale Variablen zuerst deklarieren, dann die Funktion ``void setup()`` definieren und schließlich die Funktion ``void loop()``.

4. Gehe ganz an den Anfang deines Sketches, vor die Funktion ``void setup()``. Hier wirst du deine Variable deklarieren, um den Wert des Potentiometers zu speichern.

.. code-block:: Arduino
    :emphasize-lines: 1

    int potValue = 0;

    void setup() {
        // Füge deinen Setup-Code hier ein, um ihn einmal auszuführen:
        pinMode(9, OUTPUT);  // Setze Pin 9 als Ausgang
    }

    void loop() {
        // Füge deinen Hauptcode hier ein, um ihn wiederholt auszuführen:
    }

Du hast gerade eine Ganzzahl-Variable namens ``potValue`` deklariert und auf Null gesetzt. Diese Variable wird später in deinem Sketch verwendet, um den Ausgang des Potentiometers zu speichern.

**Lesen von Analogwerten**

Du bist nun bereit, in die Hauptschleife des Programms einzusteigen. Das erste, was du in der Funktion ``void loop()`` tun wirst, ist den Wert des Potentiometers zu bestimmen.

Das Potentiometer ist an einen 5-Volt-Strom-Pin angeschlossen, was bedeutet, dass die Spannung an Pin A0 zwischen 0 und 5 Volt variieren kann. Diese Spannung wird dann vom Mikroprozessor des Arduino Uno R3 in einen analogen Wert zwischen 0 und 1023 umgewandelt, dank der 10-Bit-Auflösung des Mikroprozessors.

Sobald sie umgewandelt wurde, können diese analogen Werte innerhalb deines Programms verwendet werden.

Um den analogen Wert des Potentiometers abzurufen, verwendest du den Befehl ``analogRead(pin)``. Dieser Befehl liest die Spannung, die in einen analogen Pin eingegeben wird, und ordnet sie einem Wert zwischen 0 und 1023 zu:

- Wenn keine Spannung anliegt, beträgt der analoge Wert 0.
- Wenn die Spannung volle 5 Volt beträgt, wird der analoge Wert 1023 sein.

Hier ist, wie du es verwendest:

    * ``analogRead(pin)``: Liest den Wert vom angegebenen analogen Pin.

    **Parameter**
        - ``pin``: der Name des analogen Eingabepins, von dem gelesen wird.

    **Rückgabe**
        Der analoge Wert am Pin. Obwohl er auf die Auflösung des Analog-Digital-Wandlers (0-1023 bei 10 Bit oder 0-4095 bei 12 Bit) beschränkt ist. Datentyp: int.

5. Platziere den folgenden Befehl in der ``void loop()`` Funktion, um den analogen Wert des Potentiometers in der oben deklarierten Variable ``potValue`` zu speichern:

.. code-block:: Arduino
    :emphasize-lines: 10

    int potValue = 0;

    void setup() {
        // Füge deinen Setup-Code hier ein, um ihn einmal auszuführen:
        pinMode(9, OUTPUT);  // Setze Pin 9 als Ausgang
    }

    void loop() {
        // Füge deinen Hauptcode hier ein, um ihn wiederholt auszuführen:
        potValue = analogRead(A0);        // Lese Wert vom Potentiometer
    }


Stelle sicher, dass du deinen Code speicherst und überprüfst, um mögliche Fehler zu korrigieren.


**Schreiben von Analogwerten**

Die digitalen Pins des Arduino Uno R3 können entweder EIN oder AUS Zustände annehmen, was bedeutet, dass sie keine echten analogen Werte ausgeben können. Um ein analoges Verhalten für Anwendungen wie die Steuerung der LED-Helligkeit zu simulieren, verwenden wir eine Technik namens Pulsweitenmodulation (PWM). PWM-Pins, die auf der Platine mit einer Tilde (~) gekennzeichnet sind, können die wahrgenommene Ausgangsleistung ändern, indem sie den Tastgrad des Signals anpassen.

.. image:: img/9_dimmer_pwm_pin.png
    :width: 500
    :align: center

Um die Helligkeit einer LED zu steuern, verwenden wir den Befehl ``analogWrite(pin, value)``. Dieser passt die Helligkeit der LED an, indem der Tastgrad des PWM-Signals, das an den Pin gesendet wird, geändert wird.

    * ``analogWrite(pin, value)``: Schreibt einen analogen Wert (PWM-Signal) an einen Pin. Kann verwendet werden, um eine LED mit variierender Helligkeit zu beleuchten oder einen Motor mit verschiedenen Geschwindigkeiten anzutreiben.

    **Parameter**
        - ``pin``: der Arduino-Pin, an den geschrieben wird. Erlaubte Datentypen: int.
        - ``value``: der Tastgrad: zwischen 0 (immer aus) und 255 (immer an). Erlaubte Datentypen: int.
    
    **Rückgabe**
        Keine

Betrachte den Tastgrad wie das Auf- und Zudrehen eines Wasserhahns, der den Wasserfluss in einen Eimer steuert, was die LED-Helligkeit darstellt. Hier ist eine einfache Aufschlüsselung:

* ``analogWrite(255)`` bedeutet, dass der Wasserhahn die ganze Zeit vollständig geöffnet ist, der Eimer voll ist und die LED am hellsten leuchtet.
* ``analogWrite(191)`` bedeutet, dass der Wasserhahn 75% der Zeit geöffnet ist, der Eimer weniger voll ist und die LED dunkler leuchtet.
* ``analogWrite(0)`` bedeutet, dass der Wasserhahn vollständig geschlossen ist, der Eimer leer ist und die LED aus ist.

.. image:: img/9_pwm_signal.png
    :width: 400
    :align: center

6. Füge in der Funktion ``void loop()`` einen ``analogWrite()``-Befehl hinzu und kommentiere jede Zeile zur Verdeutlichung:

.. note::

    * Da der Eingangsbereich des Potentiometers von 0 bis 1023 reicht, der Ausgangsbereich zu den LEDs jedoch von 0 bis 255 reicht, kannst du den Potentiometerwert durch 4 teilen, um diese Lücke zu überbrücken.

    * Obwohl das Ergebnis der Division möglicherweise keine ganze Zahl ist, wird nur der ganzzahlige Teil gespeichert, da die Variablen als Ganzzahlen (int) deklariert sind.


.. code-block:: Arduino
    :emphasize-lines: 11

    int potValue = 0;

    void setup() {
        // Füge deinen Setup-Code hier ein, um ihn einmal auszuführen:
        pinMode(9, OUTPUT);  // Setze Pin 9 als Ausgang
    }

    void loop() {
        // Füge deinen Hauptcode hier ein, um ihn wiederholt auszuführen:
        potValue = analogRead(A0);        // Lese Wert vom Potentiometer
        analogWrite(9, potValue / 4);     // Wende Helligkeit auf LED an Pin 9 an
    }

7. Sobald der Code auf den Arduino Uno R3 hochgeladen ist, ändert sich die Helligkeit der LEDs, wenn du das Potentiometer drehst. Entsprechend unserer Einrichtung sollte das Drehen des Potentiometers im Uhrzeigersinn die Helligkeit erhöhen, während das Drehen gegen den Uhrzeigersinn sie verringern sollte.

.. note::

    Beim Debuggen muss oft sowohl der Code als auch die Schaltung auf Fehler überprüft werden. Wenn der Code korrekt kompiliert wird oder korrekt erscheint, aber die LED sich nicht wie erwartet ändert, liegt das Problem möglicherweise in der Schaltung. Überprüfe alle Verbindungen und Komponenten auf dem Breadboard auf guten Kontakt.

8. Denke schließlich daran, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Frage**:

Wenn du die LED an einen anderen Pin anschließt, zum Beispiel Pin 8, und das Potentiometer drehst, wird sich die Helligkeit der LED immer noch ändern? Warum oder warum nicht?

**Zusammenfassung**

In dieser Lektion haben wir gelernt, wie man mit analogen Signalen in Arduino-Projekten arbeitet. Wir haben gelernt, wie man analoge Werte von einem Potentiometer liest, wie man diese Werte im Arduino-Sketch verarbeitet und wie man die Helligkeit einer LED mithilfe der Pulsweitenmodulation (PWM) steuert. Wir haben uns auch mit der Verwendung von Variablen zum Speichern und Verarbeiten von Daten innerhalb unserer Sketche befasst. Durch die Integration dieser Elemente haben wir die dynamische Steuerung elektronischer Komponenten demonstriert und die Brücke zwischen einfachen digitalen Ausgängen und einer nuancierteren Steuerung von Hardware durch analoge Eingaben geschlagen.

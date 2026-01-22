.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 zusammen mit anderen Enthusiasten ein.

    **Warum mitmachen?**

    - **Fachkundige Unterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitige Informationen über neue Produktankündigungen und Vorschauen.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und saisonalen Aktionen teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

.. _automatic_soap_dispenser:

20. Automatischer Seifenspender
====================================

Willkommen zu unserem Kurs über den Bau eines automatischen Seifenspenders mithilfe von Arduino-Technologie! In diesem Kurs erkunden wir die faszinierende Welt der automatisierten Systeme und wie einfache Elektronik Alltagsgegenstände erheblich verbessern kann. Unser Schwerpunkt liegt darauf, ein Gerät zu entwickeln, das die Nähe einer Hand erkennt und automatisch Seife ausgibt.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/20_automatic_soap_dispenser.mp4" type="video/mp4">
        Dein Browser unterstützt das Video-Tag nicht.
    </video>

Am Ende dieser Lektion wirst du in der Lage sein:


* Die Funktionsweise einer Wasserpumpe zu verstehen.
* Einen automatischen Seifenspender zu entwickeln, der auf die Nähe deiner Hand reagiert und mithilfe von Entfernungsmessungen eines Ultraschallsensors Seife ausgibt.



Bau der Schaltung
---------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Pumpe
     - 1 * Ultraschallmodul
     - 1 * L293D-Chip
   * - |list_uno_r3|
     - |list_pump| 
     - |list_ultrasonic|
     - |list_l293d|
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - Verbindungskabel
     - 1 * Steckbrett-Netzteilmodul
   * - |list_usb_cable|
     - |list_breadboard|
     - |list_wire|
     - |list_power_module|
   * - 1 * 9V Batterie
     - 1 * Batteriekabel
     - 
     -  
   * - |list_battery| 
     - |list_bat_cable| 
     -
     -

**Schritt-für-Schritt Aufbau**

Folge dem Verdrahtungsdiagramm oder den unten stehenden Schritten, um deine Schaltung aufzubauen.

.. image:: img/20_dispenser_connect_pump.png
    :width: 600
    :align: center

1. Bei der Verwendung von Motoren, Servos und anderen Aktoren wird empfohlen, eine externe Stromversorgung zu verwenden, um Schäden an der Hauptplatine zu vermeiden. Setze das Steckbrett-Netzteilmodul in das Steckbrett ein und verwende ein Verbindungskabel, um die negative Schiene des Steckbretts mit dem GND des Arduino Uno R3 zu verbinden, um eine gemeinsame Masse zu erreichen.

.. image:: img/14_dinosaur_power_module.png
    :width: 400
    :align: center

.. note::

    Die Anordnung der positiven und negativen Klemmen auf dem Steckbrett im Verdrahtungsdiagramm ist im Vergleich zum Steckbrett im Bausatz vertauscht.

    Beim tatsächlichen Verdrahten musst du das Steckbrett-Netzteilmodul von der höheren Zahlenseite (60~65) einfügen, sodass das "-" des Netzteilmoduls in die negative Schiene "-" des Steckbretts und das "+" in die positive Schiene "+" gelangt.

    .. raw:: html

        <video controls style = "max-width:100%">
            <source src="_static/video/about_power_module.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

2. Setze das Ultraschallmodul in das Steckbrett ein.

.. image:: img/20_dispenser_ultrasonic.png
    :width: 400
    :align: center

3. Verbinde den VCC-Pin des Ultraschallmoduls mit der positiven Seite des Steckbretts, den Trig-Pin mit Pin 8 auf dem Arduino-Board, den Echo-Pin mit Pin 7 und den GND mit der negativen Seite des Steckbretts.

.. image:: img/20_dispenser_ultrasonic_pins.png
    :width: 400
    :align: center

4. Finde die Wasserpumpe.

.. image:: img/20_despenser_pump.png
  :width: 200
  :align: center


Dies ist die DC 2.5-6V Mini-Tauchpumpe, ideal für kleine Projekte wie Tischbrunnen, Aquarien und Hydrokultursysteme.

Diese Pumpe verwendet zentrifugale Mechanik, wobei ein Elektromotor Rotationsenergie in Strömungsenergie umwandelt und so effizient Wasser durch das System bewegt. Einfach zu installieren und zu warten, ist sie eine zuverlässige Wahl für DIY-Enthusiasten.

.. image:: img/20_despenser_pump_intro.png
  :width: 400
  :align: center


5. Die Wasserpumpe benötigt auch einen Motortreiber-Chip. Jetzt setzen wir den L293D-Chip in die mittlere Kerbe des Steckbretts ein. Achte darauf, dass die Kerbe auf dem Chip nach links zeigt.

.. image:: img/20_dispenser_l293d.png
  :width: 600
  :align: center

6. Verbinde die Pins des L293D-Chips wie folgt:

* **1(1,2EN)**: Verbinde mit der positiven Schiene des Steckbretts, um den Chip zu aktivieren.
* **4(GND)**: Verbinde mit der negativen Schiene des Steckbretts, um den Chip zu erden.
* **8(VCC2)**: Verbinde mit der positiven Schiene des Steckbretts, um die Pumpe mit Strom zu versorgen.
* **16(VCC1)**: Verbinde mit der positiven Schiene des Steckbretts, um den Chip mit Strom zu versorgen.

.. image:: img/20_dispenser_l293d_power_pins.png
  :width: 600
  :align: center

7. Im Gegensatz zu Motoren haben Wasserpumpen keine Drehrichtung, die unterschieden werden muss. Sie benötigen lediglich eine Spannungsdifferenz an zwei Pins, um Wasser zu pumpen. Verbinde daher Pin 2 (1A) des L293D mit Pin 2 des Arduino Uno R3 und Pin 3 (1Y) mit der Wasserpumpe, wobei der andere Pin der Wasserpumpe mit GND verbunden wird.

* Indem Pin 2 einfach auf High gesetzt wird, beginnt die Wasserpumpe, Wasser zu pumpen.

.. image:: img/20_dispenser_connect_pump.png
  :width: 600
  :align: center

Codeerstellung - So funktioniert die Wasserpumpe
------------------------------------------------------

Lass uns zunächst sehen, wie die Wasserpumpe funktioniert. Du benötigst ein Glas Wasser, das groß genug ist, um die Pumpe vollständig zu untertauchen, und ein weiteres leeres Glas, um das abgepumpte Wasser aufzufangen.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „New Sketch“ aus dem „File“-Menü wählst.
2. Speichere dein Sketch unter dem Namen ``Lesson20_Pump`` mit ``Ctrl + S`` oder durch Klicken auf „Save“.

3. Das Betreiben der Wasserpumpe ist genauso einfach wie das Ansteuern einer LED. Initialisiere einfach den Pumpensteuerungspin, setze ihn als Ausgang und schalte ihn dann auf High.

.. code-block:: Arduino

  #define PUMP_PIN     2  // Pumpensteuerungspin

  void setup() {
    pinMode(PUMP_PIN, OUTPUT);    // Setze den Pumpensteuerungspin als Ausgang
  }

  void loop() {
    digitalWrite(PUMP_PIN, HIGH);       // Schalte die Pumpe mit voller Geschwindigkeit ein
  }

4. Der Code ist vollständig. Du kannst ihn jetzt auf das Arduino Uno R3 Board hochladen. Danach wirst du sehen, wie das Wasser durch den Schlauch der Pumpe vom vollen Glas in das leere Glas gepumpt wird.

**Frage**

In diesem Projekt hast du die Wasserpumpe mit einem speziellen Treiber und einer bestimmten Konfiguration angeschlossen. Was denkst du, würde passieren, wenn du die Anschlüsse der Pumpe umkehrst? Würde die Pumpe rückwärts arbeiten, aufhören zu funktionieren oder etwas anderes tun? Probiere es aus und reflektiere über das Ergebnis.

.. image:: img/20_despenser_pump_change.png
  :width: 600
  :align: center

Codeerstellung - Automatischer Seifenspender
-------------------------------------------------
Hier bauen wir einen automatischen Seifenspender, der durch eine Wasserpumpe Seifenflüssigkeit abgibt. Der Spender wird durch einen Ultraschallsensor ausgelöst, der die Nähe einer Hand erkennt. Wenn die gemessene Entfernung weniger als 10 cm beträgt, was darauf hindeutet, dass eine Hand in der Nähe ist, wird der Spender Seife abgeben.

Um den Seifenverbrauch zu optimieren, läuft die Pumpe 500 Millisekunden, um Seife abzugeben. Wird nach einer Pause von 2 Sekunden weiterhin eine Hand erkannt, aktiviert sich die Pumpe erneut für 500 Millisekunden, um eine ausreichende Menge Seife abzugeben. Dieses Setup verwaltet die Seifenabgabe effizient und berücksichtigt die Bedürfnisse des Benutzers.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „New Sketch“ aus dem „File“-Menü wählst.
2. Speichere dein Sketch unter dem Namen ``Lesson20_Soap_Dispenser`` mit ``Ctrl + S`` oder durch Klicken auf „Save“.

3. Initialisiere die beiden Pins für den Ultraschallsensor und den Pumpenpin.

.. code-block:: Arduino
  :emphasize-lines: 1-3

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7
  #define PUMP_PIN 2  // Pumpensteuerungspin

  void setup() {
    // füge hier den Setup-Code ein, der einmal ausgeführt wird:

  }

4. In der Funktion ``void setup()``, setze die Modi für die im Projekt verwendeten Pins und initialisiere die serielle Kommunikation bei 9600 bps zur Fehlerbehebung und Überwachung der Sensorausgabe.

.. code-block:: Arduino
  :emphasize-lines: 6-9

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7
  #define PUMP_PIN 2  // Pumpensteuerungspin

  void setup() {
    pinMode(PUMP_PIN, OUTPUT);     // Setze den Pumpensteuerungspin als Ausgang
    pinMode(TRIGGER_PIN, OUTPUT);  // Setze den Trig-Pin als Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setze den Echo-Pin als Eingang
    Serial.begin(9600);            // Starte die serielle Kommunikation zur Fehlerbehebung
  }

5. Du benötigst eine spezifische Funktion, um die vom Ultraschallmodul gemessene Entfernung abzurufen. Wie diese Funktion implementiert wird, kannst du unter :ref:`ar_read_distance` nachlesen.

.. code-block:: Arduino
  :emphasize-lines: 7-17
  
  void loop() {
    // füge hier den Hauptcode ein, der wiederholt ausgeführt wird:

  }

  // Funktion zum Auslesen der Sensordaten und Berechnung der Entfernung
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Stelle sicher, dass der Trig-Pin vor einem Puls auf LOW ist
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Sende einen hohen Puls
    delayMicroseconds(10);            // Pulsdauer von 10 Mikrosekunden
    digitalWrite(TRIGGER_PIN, LOW);   // Beende den hohen Puls

    long duration = pulseIn(ECHO_PIN, HIGH);  // Messe die Dauer des hohen Pegels am Echo-Pin
    long distance = duration * 0.034 / 2;     // Berechne die Entfernung (in cm)
    return distance;
  }

6. Nun wechsle zur Funktion ``void loop()``, rufe die Funktion ``measureDistance()`` auf, um die gemessene Distanz in der Variablen ``distance`` zu speichern, und gib sie im seriellen Monitor aus.

.. code-block:: Arduino
  :emphasize-lines: 2-4

  void loop() {
    long distance = measureDistance();  // Ruft die Funktion zur Distanzmessung auf
    Serial.println(distance);
    delay(100);  // Verzögerung zwischen den Messungen
  }

7. Anschließend wird basierend auf der gemessenen Distanz der Betriebszustand der Pumpe festgelegt. Wenn die Distanz zwischen 2 und 10 cm liegt, wird die Pumpe aktiviert, um für 500 Millisekunden Seife abzugeben, und schaltet sich dann ab. Danach wartet sie 2 Sekunden, bevor eine erneute Aktivierung erfolgen kann.

.. code-block:: Arduino
  :emphasize-lines: 5-12

  void loop() {
    long distance = measureDistance();  // Ruft die Funktion zur Distanzmessung auf
    Serial.println(distance);

    if (distance > 2 && distance < 10) {  // Wenn die Distanz zwischen 2 und 10 cm liegt
      digitalWrite(PUMP_PIN, HIGH);       // Schalte die Pumpe ein
      delay(500);
      digitalWrite(PUMP_PIN, LOW);  // Schalte die Pumpe aus
      delay(2000);
    } else {
      digitalWrite(PUMP_PIN, LOW);  // Schalte die Pumpe aus
    }
    delay(100);  // Verzögerung zwischen den Messungen
  }

8. Hier ist dein vollständiger Code, den du auf das Arduino Uno R3 Board hochladen kannst.

.. code-block:: Arduino

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7
  #define PUMP_PIN 2  // Pumpensteuerungspin

  void setup() {
    pinMode(PUMP_PIN, OUTPUT);     // Setze den Pumpensteuerungspin als Ausgang
    pinMode(TRIGGER_PIN, OUTPUT);  // Setze den Trig-Pin als Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setze den Echo-Pin als Eingang
    Serial.begin(9600);            // Starte die serielle Kommunikation zur Fehlerbehebung
  }

  void loop() {
    long distance = measureDistance();  // Ruft die Funktion zur Distanzmessung auf
    Serial.println(distance);

    if (distance > 2 && distance < 10) {  // Wenn die Distanz zwischen 2 und 10 cm liegt
      digitalWrite(PUMP_PIN, HIGH);       // Schalte die Pumpe ein
      delay(500);
      digitalWrite(PUMP_PIN, LOW);  // Schalte die Pumpe aus
      delay(2000);
    } else {
      digitalWrite(PUMP_PIN, LOW);  // Schalte die Pumpe aus
    }
    delay(100);  // Verzögerung zwischen den Messungen
  }

  // Funktion zum Auslesen der Sensordaten und Berechnung der Entfernung
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Stelle sicher, dass der Trig-Pin vor einem Puls auf LOW ist
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Sende einen hohen Puls
    delayMicroseconds(10);            // Pulsdauer von 10 Mikrosekunden
    digitalWrite(TRIGGER_PIN, LOW);   // Beende den hohen Puls

    long duration = pulseIn(ECHO_PIN, HIGH);  // Messe die Dauer des hohen Pegels am Echo-Pin
    long distance = duration * 0.034 / 2;     // Berechne die Entfernung (in cm)
    return distance;
  }

9. Denke schließlich daran, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.


**Zusammenfassung**

In der heutigen Lektion haben wir erfolgreich einen automatischen Seifenspender gebaut und programmiert. Wir haben den Einsatz von Ultraschallsensoren zur Erkennung von Annäherungen untersucht und gelernt, wie man eine Wasserpumpe über Arduino-Programmierung steuert. Die erworbenen Fähigkeiten erweitern nicht nur dein Verständnis von elektronischen Schaltungen, sondern eröffnen auch eine Vielzahl von Möglichkeiten für zukünftige Projekte.


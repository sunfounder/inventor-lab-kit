.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community auf Facebook! Tauche gemeinsam mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum mitmachen?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Einblicken.
    - **Spezielle Rabatte**: Profitiere von exklusiven Rabatten auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu erkunden und zu erschaffen? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

.. _ar_smart_trash_can:

19. Intelligenter Mülleimer
==============================

Willkommen zu unserem spannenden projektbasierten Kurs, in dem wir einen intelligenten Mülleimer bauen! Dieser Kurs bietet einen praxisnahen Ansatz zur Integration eines Ultraschallsensors mit einem Servomotor, um einen Mülleimer zu schaffen, der auf deine Anwesenheit reagiert. Am Ende dieses Kurses wirst du verstehen, wie alltägliche Gegenstände intelligenter und interaktiver gestaltet werden können.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/19_smart_trash_can.mp4" type="video/mp4">
        Dein Browser unterstützt das Video-Tag nicht.
    </video>

Am Ende dieser Lektion wirst du in der Lage sein:

* Ultraschallsensoren zur Abstandsmessung zu verstehen und zu nutzen.
* Einen Servo zu integrieren, um physische Aktionen zu automatisieren.
* Ein Arduino so zu programmieren, dass das Verhalten von Geräten basierend auf Sensoreingaben gesteuert wird.

Lerne das Ultraschallmodul kennen
-------------------------------------

Stell dir vor, du bist in einem dunklen Raum und kannst die Objekte um dich herum nicht sehen. In dieser Situation könntest du in die Hände klatschen, um ein Geräusch zu erzeugen, das sich ausbreitet. Wenn dieses Geräusch auf eine Wand oder ein anderes Objekt trifft, wird es als Echo zurückgeworfen. Wenn du genau hinhörst, kannst du dieses Echo hören. Indem du die Zeit berechnest, die das Geräusch benötigt, um zurückzukehren, kannst du grob abschätzen, wie weit die Wand oder das Objekt entfernt ist. Ultraschallsensoren funktionieren auf ähnliche Weise, um die Umgebung „zu sehen“.

.. image:: img/19_ultrasonic_pic.png
    :width: 400
    :align: center

* **TRIG**: Trigger-Puls-Eingang
* **ECHO**: Echo-Puls-Ausgang
* **GND**: Masse
* **VCC**: 5V Stromversorgung

Der HC-SR04 Ultraschall-Abstandssensor bietet eine berührungslose Messung von 2 cm bis 400 cm mit einer Reichweiten-Genauigkeit von bis zu 3 mm. Auf dem Modul sind ein Ultraschallsender, ein Empfänger und eine Steuerschaltung enthalten.

Du musst nur 4 Pins anschließen: VCC (Stromversorgung), Trig (Auslösung), Echo (Empfang) und GND (Masse), um ihn einfach für deine Messprojekte zu nutzen.

**Prinzip**

Die grundlegenden Prinzipien sind wie folgt:

* Verwendung von IO-Trigger für mindestens 10 µs High-Level-Signal.
* Das Modul sendet eine Ultraschall-Burst von 8 Zyklen bei 40 kHz und erkennt, ob ein Pulssignal empfangen wurde.
* Echo gibt ein High-Level aus, wenn ein Signal zurückkommt; die Dauer des High-Levels ist die Zeit vom Aussenden bis zum Empfang.
* Abstand = (High-Level-Zeit x Schallgeschwindigkeit (340M/S)) / 2

.. image:: img/19_ultrasonic_ms.png
    :width: 600
    :align: center

.. note::

  Dieses Modul sollte nicht unter Spannung angeschlossen werden. Falls notwendig, sollte zuerst die GND-Leitung des Moduls angeschlossen werden. Andernfalls kann dies die Funktion des Moduls beeinträchtigen.

  Die zu messende Objektfläche sollte mindestens 0,5 Quadratmeter groß und so flach wie möglich sein. Andernfalls kann dies die Ergebnisse beeinflussen.

Baue die Schaltung
------------------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Servo
     - 1 * Ultraschall-Modul
     - 1 * Steckbrett-Stromversorgungsmodul 
   * - |list_uno_r3|
     - |list_servo| 
     - |list_ultrasonic|
     - |list_power_module|
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - Jumper-Kabel
     -
   * - |list_usb_cable|
     - |list_breadboard|
     - |list_wire|
     -
   * - 1 * 9V Batterie
     - 1 * Batteriekabel
     - 
     -  
   * - |list_battery| 
     - |list_bat_cable| 
     -
     -

**Schritt-für-Schritt-Anleitung**

Folge dem Verdrahtungsdiagramm oder den folgenden Schritten, um deine Schaltung aufzubauen.

.. image:: img/19_trashcan_ultrasonic_pins.png
    :width: 600
    :align: center

1. Bei der Verwendung von Motoren, Servos und anderen Aktuatoren wird empfohlen, eine externe Stromversorgung zu verwenden, um Schäden an der Hauptplatine zu vermeiden. Stecke das Steckbrett-Stromversorgungsmodul in das Steckbrett und verbinde dann mit einem Jumperkabel die negative Schiene des Steckbretts mit dem GND des Arduino Uno R3, um eine gemeinsame Masse zu erreichen.

.. image:: img/14_dinosaur_power_module.png
    :width: 400
    :align: center

.. note::

    Die Anordnung der positiven und negativen Anschlüsse auf dem Steckbrett im Verdrahtungsdiagramm ist im Vergleich zu dem im Kit enthaltenen Steckbrett umgekehrt.

    In der tatsächlichen Verdrahtung musst du das Steckbrett-Stromversorgungsmodul von der höheren Nummerseite (60~65) einstecken, sodass das "-" des Stromversorgungsmoduls in die negative Schiene "-" des Steckbretts und das "+" in die positive Schiene "+" gesteckt wird.

    .. raw:: html

        <video controls style = "max-width:100%">
            <source src="_static/video/about_power_module.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

2. Verwende drei kurze Jumperkabel, um die drei Kabel deines Servos zu verlängern: Verbinde das gelbe Kabel mit Pin 9 des Arduino Uno R3, das rote Kabel mit der positiven Schiene des Steckbretts und das braune Kabel mit der negativen Schiene des Steckbretts.

.. image:: img/19_trashcan_servo.png
    :width: 600
    :align: center

4. Setze das Ultraschallmodul in das Steckbrett ein.

.. image:: img/19_trashcan_ultrasonic.png
    :width: 600
    :align: center


5. Verbinde den VCC-Pin des Ultraschallmoduls mit der positiven Seite des Steckbretts, den Trig-Pin mit Pin 8 auf dem Arduino-Board, den Echo-Pin mit Pin 7 und den GND mit der negativen Seite des Steckbretts.

.. image:: img/19_trashcan_ultrasonic_pins.png
    :width: 600
    :align: center

.. _ar_read_distance:

Code-Erstellung - Distanzmessung
-----------------------------------------
Nun schauen wir uns an, wie man die Entfernungsmessungen vom Ultraschallmodul erhält.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „Neue Skizze“ aus dem Menü „Datei“ wählst.
2. Speichere deine Skizze als ``Lesson19_Read_Distance`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Zuerst müssen wir die Pins am Arduino definieren, die mit dem Ultraschallmodul verbunden sind.

.. code-block:: Arduino
  :emphasize-lines: 1,2

  #define TRIGGER_PIN  8
  #define ECHO_PIN     7


4. Im ``setup()``-Funktionsblock legen wir den Modus für jeden Pin fest. Der Trig-Pin muss auf Ausgang gesetzt werden (da er das Signal sendet), der Echo-Pin wird auf Eingang gesetzt (da er das Signal empfängt).

.. code-block:: Arduino
  :emphasize-lines: 2,3
  
  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Setze den Trig-Pin auf Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setze den Echo-Pin auf Eingang
    Serial.begin(9600);            // Starte die serielle Kommunikation zum Debuggen
  }

5. Schreiben der ``measureDistance()``-Funktion:

Die ``measureDistance()``-Funktion fasst die Logik zusammen, die erforderlich ist, um den Ultraschallsensor auszulösen und die Entfernung basierend auf dem empfangenen Echo zu messen:

a. Auslösen des Ultraschallpulses

  * Setze den ``TRIGGER_PIN`` zunächst auf LOW, um einen sauberen Puls sicherzustellen.
  * Eine kurze Verzögerung von 2 Mikrosekunden sorgt dafür, dass die Leitung frei ist.
  * Sende einen 10-Mikrosekunden-High-Puls an den ``TRIGGER_PIN``. Dieser Impuls signalisiert dem Sensor, eine Ultraschallwelle auszusenden.
  * Setze den ``TRIGGER_PIN`` wieder auf LOW, um den Puls zu beenden.

  .. code-block:: Arduino

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Stelle sicher, dass der Trig-Pin vor einem Puls auf LOW ist
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Sende einen High-Puls
      delayMicroseconds(10);           // Pulsdauer von 10 Mikrosekunden
      digitalWrite(TRIGGER_PIN, LOW);  // Beende den High-Puls
    }


b. Echo lesen

  * Die Funktion ``pulseIn()`` wird am ``ECHO_PIN`` verwendet, um die Dauer des eingehenden Pulses zu messen. Diese Funktion wartet, bis der Pin auf ``HIGH`` geht, misst die Dauer des ``HIGH``-Zustands und gibt die Dauer in Mikrosekunden zurück.
  * Diese ``Dauer`` ist die Zeit, die das Ultraschall-Signal benötigt, um zum Objekt und zurück zu gelangen.

  .. code-block:: Arduino
    :emphasize-lines: 7

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Stelle sicher, dass der Trig-Pin vor einem Puls auf LOW ist
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Sende einen High-Puls
      delayMicroseconds(10);           // Pulsdauer von 10 Mikrosekunden
      digitalWrite(TRIGGER_PIN, LOW);  // Beende den High-Puls
      long duration = pulseIn(ECHO_PIN, HIGH);  // Miss die Dauer des HIGH-Levels am Echo-Pin
    }

c. Berechnung der Distanz

  * Die Schallgeschwindigkeit in der Luft (ca. 340 m/s) wird hier verwendet. Die Formel zur Berechnung der Entfernung lautet (Dauer * Schallgeschwindigkeit) / 2. Wir teilen durch 2, da die Schallwelle zum Objekt und zurück reist, also benötigen wir nur die Hälfte der Strecke für die Einwegmessung.
  * In unserem Code wird 0,034 cm/µs (Schallgeschwindigkeit in cm/Mikrosekunde) als Umrechnungsfaktor verwendet.

  .. code-block:: Arduino
    :emphasize-lines: 8,9

    long measureDistance() {
      digitalWrite(TRIGGER_PIN, LOW);  // Stelle sicher, dass der Trig-Pin vor einem Puls auf LOW ist
      delayMicroseconds(2);
      digitalWrite(TRIGGER_PIN, HIGH); // Sende einen High-Puls
      delayMicroseconds(10);           // Pulsdauer von 10 Mikrosekunden
      digitalWrite(TRIGGER_PIN, LOW);  // Beende den High-Puls
      long duration = pulseIn(ECHO_PIN, HIGH);  // Miss die Dauer des HIGH-Levels am Echo-Pin
      long distance = duration * 0.034 / 2;     // Berechne die Entfernung (in cm)
      return distance;
    }

6. In der Funktion ``loop()`` rufen wir die Funktion ``measureDistance()`` auf, um die Entfernung zu messen, und geben sie dann im seriellen Monitor aus.

.. code-block:: Arduino

  void loop() {
    long distance = measureDistance(); // Ruft die Funktion zur Entfernungsmessung auf
    Serial.print("Entfernung: ");
    Serial.print(distance);
    Serial.println(" cm");

    delay(100);  // Verzögerung zwischen den Messungen
  }

.. note::

  In den vorherigen Lektionen haben wir mit den Datentypen ``int`` und ``float`` für Variablen und Konstanten gearbeitet. Jetzt schauen wir uns an, was ``long`` und ``unsigned long`` sind:

  * ``long``: Ein ``long``-Integer ist eine erweiterte Version eines ``int``. Er wird verwendet, um größere Ganzzahlen zu speichern, die die Kapazität eines normalen ``int`` überschreiten. Ein ``long`` belegt normalerweise 32 oder 64 Bit Speicher, wodurch es viel größere Werte speichern kann, sowohl positiv als auch negativ.
  * ``unsigned long``: Ein ``unsigned long`` ist ähnlich wie ein ``long``, kann jedoch nur nicht-negative Werte darstellen. Es nutzt das Bit, das normalerweise für das Vorzeichen reserviert ist, um den Wertebereich zu erweitern, aber ausschließlich im positiven Bereich.

7. Hier ist dein vollständiger Code. Du kannst jetzt auf "Upload" klicken, um den Code auf das Arduino Uno R3 hochzuladen.

.. code-block:: Arduino

  #define TRIGGER_PIN  8
  #define ECHO_PIN     7

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Setzt den Trig-Pin auf Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setzt den Echo-Pin auf Eingang
    Serial.begin(9600);            // Startet die serielle Kommunikation zum Debuggen
  }

  void loop() {
    long distance = measureDistance(); // Ruft die Funktion zur Entfernungsmessung auf
    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    delay(100);  // Verzögerung zwischen den Messungen
  }

  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Stellt sicher, dass der Trig-Pin vor einem Puls auf LOW ist
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH); // Sendet einen High-Puls
    delayMicroseconds(10);           // Pulsdauer von 10 Mikrosekunden
    digitalWrite(TRIGGER_PIN, LOW);  // Beendet den High-Puls

    long duration = pulseIn(ECHO_PIN, HIGH);  // Misst die Dauer des HIGH-Levels am Echo-Pin
    long distance = duration * 0.034 / 2;     // Berechnet die Entfernung (in cm)
    return distance;
  }

8. Öffne den seriellen Monitor und du wirst die gemessenen Entfernungswerte sehen. Du kannst das Objekt vor dem Ultraschallsensor bewegen, um zu sehen, ob sich die angezeigte Entfernung ändert. Wenn dies der Fall ist, funktioniert das Ultraschallmodul korrekt.

.. code-block::

  Entfernung: 30 cm
  Entfernung: 29 cm
  Entfernung: 28 cm
  Entfernung: 27 cm
  Entfernung: 26 cm
  Entfernung: 25 cm
  Entfernung: 25 cm

9. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Frage**

Wenn du möchtest, dass die ermittelte Entfernung genauer ist und Dezimalstellen enthält, wie solltest du den Code ändern?

Code-Erstellung - Intelligenter Mülleimer
-----------------------------------------------
Wir wissen bereits, wie man die Entfernung zu Objekten mit einem Ultraschallmodul misst. Nun wollen wir den Code schreiben, um einen intelligenten Mülleimer zu erstellen. Dieser Mülleimer öffnet seinen Deckel automatisch, wenn der Ultraschallsensor ein Objekt in weniger als 20 cm Entfernung erkennt – was darauf hinweist, dass du beabsichtigst, Müll zu entsorgen. Nachdem der Müll eingeworfen wurde, schließt sich der Deckel automatisch.

Die Bewegung des Deckels wird von einem Servo gesteuert:

* Bei einem Servowinkel von 90 Grad ist die Servowelle parallel zum Servo, was bedeutet, dass der Mülleimerdeckel geschlossen ist.
* Bei 0 Grad ist die Servowelle senkrecht zum Servo, was den Deckel über eine an der Welle befestigte Stange öffnet.

Lass uns nun erkunden, wie wir dies mithilfe von Code umsetzen können.

1. Öffne die zuvor gespeicherte Skizze ``Lesson19_Read_Distance``. Wähle im Menü "Datei" die Option "Speichern unter..." und benenne die Skizze in ``Lesson19_Smart_Trashcan`` um. Klicke auf "Speichern".

2. Um den Servo zu steuern, müssen wir die ``Servo``-Bibliothek einbinden und eine Instanz der Klasse ``Servo`` erstellen, um den Servo zu steuern.

.. code-block:: Arduino
  :emphasize-lines: 1,3

  #include <Servo.h>

  Servo myServo;  // Erstelle ein Servo-Objekt

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7

3. Definiere als nächstes den Servopin und erstelle zwei Variablen, ``openAngle`` und ``closeAngle``, um die Winkel für das Öffnen und Schließen des Mülleimerdeckels zu speichern.

.. code-block:: Arduino
  :emphasize-lines: 9-11

  #include <Servo.h>

  Servo myServo;  // Erstelle ein Servo-Objekt

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7

  // Definiere die Parameter für den Servomotor
  const int servoPin = 9;
  const int openAngle = 0;
  const int closeAngle = 90;

4. In der Funktion ``void setup()`` wird das Servo-Objekt dem angegebenen Pin zugeordnet.

.. code-block:: Arduino
  :emphasize-lines: 6

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Setzt den Trig-Pin auf Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setzt den Echo-Pin auf Eingang
    Serial.begin(9600);            // Startet die serielle Kommunikation zum Debuggen

    myServo.attach(servoPin);
  }

5. Nun sind wir beim Hauptprogramm angekommen. Kommentiere zuerst den Code für die drei seriellen Ausgaben, um Störungen im Programmablauf zu vermeiden.

.. code-block:: Arduino
  :emphasize-lines: 6

  void loop() {
    long distance = measureDistance();  // Ruft die Funktion zur Entfernungsmessung auf
    // Serial.print("Entfernung: ");
    // Serial.print(distance);
    // Serial.println(" cm");
    delay(100);  // Verzögerung zwischen den Messungen
  }

6. Wie geplant, sollte der Servo auf 0 Grad drehen, um den Deckel des Mülleimers zu öffnen, wenn der Ultraschallsensor eine Entfernung von weniger als 20 cm erkennt. Andernfalls sollte der Servo auf 90 Grad bleiben, um den Deckel geschlossen zu halten.

  * ``delay(2000);`` wird hier verwendet, um genügend Zeit zu geben, den Müll zu entsorgen, ohne dass sich der Deckel zu schnell schließt. Diese Zeitspanne kann nach Bedarf angepasst werden.
  * In ``if (distance > 2 && distance < 20)`` wird die Bedingung ``distance > 2`` verwendet, um ungültige Werte herauszufiltern. Der effektive Messbereich des Ultraschallsensors liegt zwischen 2 cm und 400 cm. Zu nahe oder zu ferne Entfernungen liefern ungültige Werte von -1 oder 0.

.. code-block:: Arduino
  :emphasize-lines: 7-12

  void loop() {
    long distance = measureDistance();  // Ruft die Funktion zur Entfernungsmessung auf
    // Serial.print("Entfernung: ");
    // Serial.print(distance);
    // Serial.println(" cm");

    if (distance > 2 && distance < 20) {
      myServo.write(openAngle);
      delay(2000);
    } else {
      myServo.write(closeAngle);
    }

    delay(100);  // Verzögerung zwischen den Messungen
  }

7. Dein vollständiger Code sieht wie folgt aus. Du kannst ihn hochladen und testen, ob sich dein Mülleimer automatisch öffnet und dann schließt, nachdem du den Müll entsorgt hast.

.. code-block:: Arduino

  #include <Servo.h>

  Servo myServo;  // Erstelle ein Servo-Objekt

  #define TRIGGER_PIN 8
  #define ECHO_PIN 7

  // Parameter für den Servomotor festlegen
  const int servoPin = 9;
  const int openAngle = 0;
  const int closeAngle = 90;

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Setzt den Trig-Pin auf Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setzt den Echo-Pin auf Eingang
    Serial.begin(9600);            // Startet die serielle Kommunikation zum Debuggen

    myServo.attach(servoPin);
  }

  void loop() {
    long distance = measureDistance();  // Ruft die Funktion zur Entfernungsmessung auf
    // Serial.print("Entfernung: ");
    // Serial.print(distance);
    // Serial.println(" cm");

    if (distance > 2 && distance < 20) {
      myServo.write(openAngle);
      delay(2000);
    } else {
      myServo.write(closeAngle);
    }

    delay(100);  // Verzögerung zwischen den Messungen
  }

  // Funktion zur Sensorabfrage und Berechnung der Entfernung
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Stellt sicher, dass der Trig-Pin vor dem Puls auf LOW ist
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Sendet einen High-Puls
    delayMicroseconds(10);            // Pulsdauer von 10 Mikrosekunden
    digitalWrite(TRIGGER_PIN, LOW);   // Beendet den High-Puls

    long duration = pulseIn(ECHO_PIN, HIGH);  // Misst die Dauer des HIGH-Pegels am Echo-Pin
    long distance = duration * 0.034 / 2;     // Berechnet die Entfernung (in cm)
    return distance;
  }

8. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Zusammenfassung**

Heute haben wir erfolgreich einen intelligenten Mülleimer gebaut, der seinen Deckel automatisch öffnet, wenn ein Objekt in weniger als 20 cm Entfernung erkannt wird. Wir haben erforscht, wie Ultraschallsensoren funktionieren, ähnlich wie die Echoortung, und diese Technologie genutzt, um einen Servomotor zu steuern. Außerdem haben wir bewährte Methoden für die Verkabelung besprochen und Tipps für effizientes Arduino-Programmieren gegeben. Die interaktive Natur des Projekts hat praktische Erfahrungen mit realen Anwendungen von Sensoren und Servomotoren ermöglicht.


.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein und teile deine Begeisterung mit Gleichgesinnten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

30. Arduino-Radarsystem
===========================

In dieser spannenden Lektion wirst du ein dynamisches Arduino-Radarsystem konstruieren, das einen Servo und ein Ultraschallmodul kombiniert, um die Positionen nahegelegener Objekte auf einer animierten Benutzeroberfläche, die mit Processing PDE erstellt wurde, zu erkennen und anzuzeigen.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/30_servo_radar.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Am Ende dieser Lektion wirst du in der Lage sein:

* Ein scannendes Radar mit einem Servo und einem Ultraschallmodul zu bauen.
* Daten über die Arduino IDE per serieller Kommunikation an das Processing PDE zu übertragen.
* Die Grundlagen des Processing PDE zu erkunden, ein Werkzeug, das zur Erstellung einfacher Animationen und zur effektiven Visualisierung von Daten verwendet werden kann.
* Fähigkeiten in der Echtzeit-Datenvisualisierung mit dem Processing PDE zu entwickeln, um dein Verständnis von Datenflüssen und Sensordynamiken zu vertiefen.

1. Benötigte Komponenten
-----------------------------

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Servo
     - 1 * Ultraschallmodul
     - 
   * - |list_uno_r3|
     - |list_servo| 
     - |list_ultrasonic|
     - 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - Jumper-Wires
     - 1 * Steckbrett-Strommodul
   * - |list_usb_cable|
     - |list_breadboard|
     - |list_wire|
     - |list_power_module|
   * - 1 * 9V-Batterie
     - 1 * Batterieclip
     - 
     -  
   * - |list_battery| 
     - |list_bat_cable| 
     -
     -

2. Vorbereiten des Servos
-----------------------------

.. note::

  Wenn du mit dem Servo nicht vertraut bist, kannst du seine grundlegende Verwendung durch das folgende Projekt erlernen:

  * :ref:`ar_servo_usage`

**1. Aufbau der Schaltung**

Nun beginnen wir mit dem Aufbau der Schaltung. 

* Zuerst das Steckbrett-Strommodul in das Steckbrett einsetzen und dann ein Jumperkabel verwenden, um die negative Schiene des Steckbretts mit dem GND des Arduino Uno R3 zu verbinden, um eine gemeinsame Masse zu erreichen.

.. image:: img/14_dinosaur_power_module.png
    :width: 400
    :align: center

.. note::

    Die Anordnung der positiven und negativen Anschlüsse auf dem Steckbrett im Schaltplan ist im Vergleich zum im Kit bereitgestellten Steckbrett umgekehrt.

    In der tatsächlichen Verdrahtung musst du das Steckbrett-Strommodul von der höheren Nummernseite (60~65) einstecken, damit das "-" des Strommoduls in die negative Schiene "-" des Steckbretts geht und das "+" in die positive Schiene "+".

    .. raw:: html

        <video controls style = "max-width:100%">
            <source src="_static/video/about_power_module.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

* Verwende drei kurze Jumper-Wires, um die drei Kabel deines Servos zu verlängern: Verbinde das gelbe Kabel mit Pin 12 des Arduino Uno R3, das rote Kabel mit der positiven Schiene des Steckbretts und das braune Kabel mit der negativen Schiene des Steckbretts.

.. image:: img/30_radar_servo.png
    :width: 600
    :align: center

**2. Schreiben des Codes**

In unserem Arduino-Radarsystem schwenkt der Servo von 0 bis 180 Grad hin und her. Jetzt müssen wir seinen Anfangswinkel auf 90 Grad einstellen.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „Neue Skizze“ im Menü „Datei“ auswählst.
2. Speichere deine Skizze unter dem Namen ``Lesson30_Servo_Angle`` mit ``Ctrl + S`` oder indem du auf „Speichern“ klickst.

3. Den Servo zum Laufen zu bringen, ist ganz einfach. Binde einfach die ``Servo``-Bibliothek in deinen Code ein, erstelle dann ein ``Servo``-Objekt und verbinde das Servo-Objekt mit dem angegebenen Pin. Danach kannst du die ``write()``-Funktion verwenden, um den Servo auf einen bestimmten Winkel einzustellen, wie unten gezeigt:

.. code-block:: Arduino

  #include <Servo.h>

  Servo myServo;  // Erstelle ein Servo-Objekt

  const int servoPin = 12;  // Servo an digitalen Pin 12 angeschlossen

  void setup() {
    myServo.attach(servoPin);  // Verbinde das Servo-Objekt mit dem angegebenen Pin
    myServo.write(90);         // Anfangsposition auf 90 Grad setzen
  }

  void loop() {
    // Hier kommt der Hauptcode, der wiederholt ausgeführt wird:
  }

4. Lade dann den Code auf dein Arduino-Board hoch. Du wirst ein Geräusch vom Servo hören, das darauf hinweist, dass er sich in die 90-Grad-Position bewegt hat.

5. Befestige nun den einseitigen Servoarm am Servo im angegebenen Winkel. Versuche, den Servoarm parallel zum Servogehäuse zu halten; eine leichte Neigung beeinträchtigt seine Leistung nicht.

.. image:: img/30_radar_servo_arm.png
  :width: 600
  :align: center

3. Vorbereitung des Ultraschallmoduls
-----------------------------------------

.. note::

  Wenn du mit dem Ultraschallmodul nicht vertraut bist, kannst du dessen grundlegende Verwendung durch das folgende Projekt erlernen:

  * :ref:`ar_smart_trash_can`

**1. Aufbau der Schaltung**

1. Finde oder baue eine Halterung für das Ultraschallmodul, damit es am Servo befestigt werden kann.

.. note::
  Das Kit enthält diese Halterung nicht, daher musst du eine kaufen oder selbst erstellen.

.. image:: img/30_radar_ultrasonic_support.png
    :width: 600
    :align: center

2. Befestige nun das Ultraschallmodul an der Halterung, in der Regel mit M2x4-Schrauben und M2-Muttern.

.. image:: img/30_radar_ultrasonic_secure.png
    :width: 300
    :align: center

3. Befestige die Ultraschallhalterung am Servoarm. Stelle sicher, dass das Ultraschallmodul nach dem Einschalten des Arduino-Boards nach vorne zeigt.

.. image:: img/30_radar_ultrasonic_servo.png
  :width: 600
  :align: center

4. Verwende nun Jumper-Wires, um das Ultraschallmodul zu verbinden: VCC mit der positiven Schiene auf dem Steckbrett, Trig-Pin mit Pin 10 auf dem Arduino-Board, Echo-Pin mit Pin 11 und GND mit der negativen Schiene auf dem Steckbrett.

.. image:: img/30_radar_ultrasonic_pins.png
  :width: 600
  :align: center

**2. Schreiben des Codes**

1. Öffne die zuvor gespeicherte Skizze ``Lesson30_Sero_Angle``. Wähle "Speichern unter..." im "Datei"-Menü und benenne sie in ``Lesson30_Arduino_Radar`` um. Klicke auf "Speichern".

2. Definiere nun die Pins für das Ultraschallmodul und setze ihre Modi entsprechend auf ``OUTPUT`` und ``INPUT``. In diesem Code müssen wir den seriellen Monitor zur Kommunikation mit dem Processing PDE verwenden, daher starte die serielle Kommunikation mit 9600 bps.

.. code-block:: Arduino
  :emphasize-lines: 7,8,11-13

  #include <Servo.h>

  Servo myServo;  // Erstelle ein Servo-Objekt

  const int servoPin = 12;  // Servo an digitalen Pin 12 angeschlossen

  #define TRIGGER_PIN 10  // Pin für das Auslösen des Ultraschallimpulses
  #define ECHO_PIN 11     // Pin zum Empfangen des Echos

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Setze den Trig-Pin als Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setze den Echo-Pin als Eingang
    Serial.begin(9600);            // Starte die serielle Kommunikation zur Fehlersuche
    myServo.attach(servoPin);      // Definiert, an welchem Pin der Servo angeschlossen ist
    myServo.write(90);             // Anfangsposition auf 90 Grad setzen
  }

3. Du benötigst eine spezielle Funktion, um die vom Ultraschallmodul gemessene Distanz abzurufen. Du kannst sehen, wie diese Funktion implementiert wird, indem du auf :ref:`ar_read_distance` verweist.

.. code-block:: Arduino
  :emphasize-lines: 7-17
  
  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:

  }

  // Funktion zum Lesen der Sensordaten und Berechnen der Distanz
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Sicherstellen, dass der Trig-Pin vor einem Impuls niedrig ist
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Sende einen hohen Impuls
    delayMicroseconds(10);            // Impulsdauer von 10 Mikrosekunden
    digitalWrite(TRIGGER_PIN, LOW);   // Beende den hohen Impuls

    long duration = pulseIn(ECHO_PIN, HIGH);  // Messe die Dauer des hohen Pegels am Echo-Pin
    long distance = duration * 0.034 / 2;     // Berechne die Distanz (in cm)
    return distance;
  }

4. Verwende eine ``for``-Schleife, um den Drehwinkel des Servos auf einen Bereich zwischen 15 und 165 Grad zu begrenzen. Dieser Bereich kann je nach Aufbau angepasst werden; der Servo kann sich von 0 bis 180 Grad drehen.

.. code-block:: Arduino
  :emphasize-lines: 3-6

  void loop() {
    // Der Servo dreht sich von 15 bis 165 Grad
    for (int i = 15; i <= 165; i++) {
      myServo.write(i);
      delay(30);
    }
  }

5. Während sich der Servo dreht, soll der Ultraschallsensor die Entfernung zu den umliegenden Objekten erfassen und die Messwerte an den seriellen Monitor senden. Diese Daten werden dann über den seriellen Port an das Processing PDE übertragen.

.. note::

  * Ändere die folgenden 4 Zeilen der ``Serial.print()``-Funktion nicht. Die Daten, die an den seriellen Monitor gesendet werden, müssen im angegebenen Format an das Processing PDE übertragen werden.
  * Im Processing-Code wird das Zeichen ``,`` verwendet, um den Servo-Winkel zu bestimmen und in einer vorgesehenen Variablen zu speichern.
  * Im Processing-Code wird das Zeichen ``.`` verwendet, um die gemessene Entfernung zu bestimmen und in einer vorgesehenen Variablen zu speichern.

.. code-block:: Arduino
  :emphasize-lines: 6-10

  void loop() {
    // Der Servo dreht sich von 15 bis 165 Grad
    for (int i = 15; i <= 165; i++) {
      myServo.write(i);
      delay(30);
      long distance = measureDistance();  // Ruf die Funktion zur Messung der Entfernung auf
      Serial.print(i);                    // Sendet den aktuellen Winkel an den seriellen Port
      Serial.print(",");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
      Serial.print(distance);             // Sendet den Entfernungswert an den seriellen Port
      Serial.print(".");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
    }
  }

6. Lasse den Servo von 165 Grad auf 15 Grad zurückdrehen und drucke die Winkel- und Entfernungswerte wie zuvor an den seriellen Port. Diese Daten werden über den seriellen Port an das Processing PDE übertragen.

.. code-block:: Arduino
  :emphasize-lines: 13-21

  void loop() {
    // Der Servo dreht sich von 15 bis 165 Grad
    for (int i = 15; i <= 165; i++) {
      myServo.write(i);
      delay(30);
      long distance = measureDistance();  // Ruf die Funktion zur Messung der Entfernung auf
      Serial.print(i);                    // Sendet den aktuellen Winkel an den seriellen Port
      Serial.print(",");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
      Serial.print(distance);             // Sendet den Entfernungswert an den seriellen Port
      Serial.print(".");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
    }
    // Der Servo dreht sich von 165 auf 15 Grad zurück
    for (int i = 165; i > 15; i--) {
      myServo.write(i);
      delay(30);
      long distance = measureDistance();  // Ruf die Funktion zur Messung der Entfernung auf
      Serial.print(i);                    // Sendet den aktuellen Winkel an den seriellen Port
      Serial.print(",");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
      Serial.print(distance);             // Sendet den Entfernungswert an den seriellen Port
      Serial.print(".");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
    }
  }

7. Der vollständige Code ist unten dargestellt. Jetzt kannst du ihn auf dein Arduino-Board hochladen. Du wirst sehen, wie sich der Servo mit dem Ultraschallmodul kontinuierlich von links nach rechts und wieder zurück bewegt. Die Daten werden im seriellen Monitor in einem Ein-Zeilen-Format ausgegeben.

.. code-block:: Arduino

  #include <Servo.h>

  Servo myServo;  // Erstelle ein Servo-Objekt

  const int servoPin = 12;  // Servo verbunden mit digitalem Pin 12

  #define TRIGGER_PIN 10  // Pin zum Auslösen des Ultraschallimpulses
  #define ECHO_PIN 11     // Pin zum Empfangen des Echos

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Setze den Trig-Pin als Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setze den Echo-Pin als Eingang
    Serial.begin(9600);            // Starte die serielle Kommunikation zur Fehlersuche
    myServo.attach(servoPin);      // Definiert, an welchem Pin der Servo angeschlossen ist
    myServo.write(90);             // Anfangsposition auf 90 Grad setzen
  }

  void loop() {
    // Der Servo dreht sich von 15 bis 165 Grad
    for (int i = 15; i <= 165; i++) {
      myServo.write(i);
      delay(30);
      long distance = measureDistance();  // Ruf die Funktion zur Messung der Entfernung auf
      Serial.print(i);                    // Sendet den aktuellen Winkel an den seriellen Port
      Serial.print(",");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
      Serial.print(distance);             // Sendet den Entfernungswert an den seriellen Port
      Serial.print(".");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
    }
    // Wiederhole die vorherigen Zeilen von 165 bis 15 Grad
    for (int i = 165; i > 15; i--) {
      myServo.write(i);
      delay(30);
      long distance = measureDistance();  // Ruf die Funktion zur Messung der Entfernung auf
      Serial.print(i);                    // Sendet den aktuellen Winkel an den seriellen Port
      Serial.print(",");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
      Serial.print(distance);             // Sendet den Entfernungswert an den seriellen Port
      Serial.print(".");                  // Sendet ein zusätzliches Zeichen direkt neben dem vorherigen Wert, das später im Processing PDE zum Indexieren verwendet wird
    }
  }

  // Funktion zum Lesen der Sensordaten und Berechnen der Entfernung
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Sicherstellen, dass der Trig-Pin vor einem Impuls niedrig ist
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Sende einen hohen Impuls
    delayMicroseconds(10);            // Impulsdauer von 10 Mikrosekunden
    digitalWrite(TRIGGER_PIN, LOW);   // Beende den hohen Impuls

    long duration = pulseIn(ECHO_PIN, HIGH);  // Messe die Dauer des hohen Pegels am Echo-Pin
    long distance = duration * 0.034 / 2;     // Berechne die Entfernung (in cm)
    return distance;
  }

8. Vergiss abschließend nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Frage**

Im obigen Code misst das Ultraschallmodul bei jedem Grad eine Entfernung. Wenn du denkst, dass die Messungen zu häufig sind und du alle 5 Grad eine Messung durchführen möchtest, wie sollte der Code geändert werden?

4. Vorbereitung des Processing PDE
-------------------------------------------

Mit dem fertigen Servo und Ultraschallmodul müssen wir nun das Processing PDE verwenden, um Code zu schreiben und auszuführen, der eine Radaroberfläche generiert, um den Drehwinkel des Radars und die erkannten Ziele anzuzeigen.

**1. Download und Installation des Processing PDE**

1. Besuche die offizielle Download-Seite von Processing: |link_processing_download|.

2. Wähle den Download entsprechend deinem Betriebssystem aus.

.. image:: img/30_radar_processing_page.png
  :width: 600
  :align: center

3. Die Installation auf jedem Rechner ist einfach.

* Unter Windows hast du eine ``.zip``-Datei. Doppelklicke darauf und ziehe den Ordner auf einen Ort deiner Festplatte. Es könnte der Programmordner oder einfach der Desktop sein, aber das Wichtigste ist, dass der Processing-Ordner aus der ``.zip``-Datei herausgezogen wird. Doppelklicke dann auf ``processing.exe``, um es zu starten.

* Die Mac OS X-Version ist ebenfalls eine ``.zip``-Datei. Doppelklicke darauf und ziehe das **Processing**-Symbol in den **Programme**-Ordner. Wenn du den Rechner einer anderen Person benutzt und den **Programme**-Ordner nicht ändern kannst, ziehe die Anwendung einfach auf den Desktop. Doppelklicke dann auf das **Processing**-Symbol, um es zu starten.

* Die Linux-Version ist eine ``.tar.gz``-Datei, die den meisten Linux-Nutzern vertraut sein sollte. Lade die Datei in dein Home-Verzeichnis herunter, öffne dann ein Terminalfenster und gib ein:

.. code-block:: Shell

  tar xvfz processing-xxxx.tgz

(Ersetze xxxx durch den Rest des Dateinamens, der die Versionsnummer ist.) Dies erstellt einen Ordner namens processing-2.0 oder etwas Ähnliches. Wechsle dann in dieses Verzeichnis:

.. code-block:: Shell

  cd processing-xxxx

und führe es aus:

.. code-block:: Shell

  ./processing

4. Mit etwas Glück wird nun das Hauptfenster von Processing sichtbar sein. 

.. image:: img/30_radar_processing_ide.png
  :align: center

**2. Code anpassen und ausführen**

1. Lade den Code herunter, der im Processing PDE ausgeführt werden soll, und extrahiere ihn dann.

* :download:`ArduinoRadarGUI </_static/zip/ArduinoRadarGUI.zip>`

2. Klicke auf **Datei** -> **Öffnen**.

.. image:: img/30_radar_open_example.png
  :align: center

3. Navigiere zu dem Ordner, in dem du gerade den Code extrahiert hast, wähle **ArduinoRadarGUI.pde** aus und klicke dann auf **Öffnen**.

.. image:: img/30_radar_example_path.png
  :align: center

4. Als Nächstes musst du den seriellen Port im Code anpassen, um denjenigen zu verwenden, den du im Arduino IDE eingestellt hast.

.. code-block:: Arduino
  :emphasize-lines: 6

  void setup() {
    //fullScreen(); // Kommentiere diese Zeile aus, wenn du keinen Vollbildmodus möchtest.
    size (1680, 945); // ***ÄNDERE DAS AUF DEINE BILDSCHIRMAUFLÖSUNG***

    smooth();
    myPort = new Serial(this, "COM39", 9600); // Startet die serielle Kommunikation
    myPort.bufferUntil('.'); // Liest die Daten vom seriellen Port bis zum Zeichen '.'. Tatsächlich liest es dies: Winkel,Entfernung.
    orcFont = loadFont("OCRAExtended-30.vlw");
  }
  
5. Nachdem du den seriellen Port geändert hast, führe den Code aus. Bevor du den Code startest, stelle sicher, dass dein Arduino Uno R3 mit dem Computer verbunden ist und der eingestellte Port korrekt ist.

.. image:: img/30_radar_run.png
  :width: 800
  :align: center

6. Du wirst sehen, wie der Servo mit dem Ultraschallmodul nach links und rechts scannt und die Winkel der erkannten Objekte innerhalb von 40 cm auf der Processing-Oberfläche anzeigt.

.. image:: img/30_radar_scan.png
  :width: 800
  :align: center

7. Wenn die Anzeige nicht vollständig sichtbar ist, kannst du die Auflösung entsprechend deinem Bildschirm anpassen, wobei ein Seitenverhältnis von 16:9 empfohlen wird. Zusätzlich kannst du ``fullScreen();`` auskommentieren, um die Processing-Anzeige im Vollbildmodus darzustellen; drücke ``ESC``, um den Vollbildmodus zu verlassen.

.. note::

  Du kannst auch die gesamte Benutzeroberfläche nach deinen Wünschen anpassen. Für detaillierte Informationen zu den Funktionen im Code, besuche bitte: |link_processing_reference|.

.. code-block:: Arduino
  :emphasize-lines: 3,4

  void setup() {

    //fullScreen(); // Kommentiere diese Zeile aus, wenn du keinen Vollbildmodus möchtest.
    size (1680, 945); // ***ÄNDERE DAS AUF DEINE BILDSCHIRMAUFLÖSUNG***

    smooth();
    myPort = new Serial(this, "COM39", 9600); // Startet die serielle Kommunikation
    myPort.bufferUntil('.'); // Liest die Daten vom seriellen Port bis zum Zeichen '.'. Tatsächlich liest es dies: Winkel, Entfernung.
    orcFont = loadFont("OCRAExtended-30.vlw");
  }

8. Vergiss abschließend nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Zusammenfassung**

In dieser Lektion haben wir ein Arduino-Radarsystem mit einem Servo und einem Ultraschallmodul gebaut, das sich von 0 bis 180 Grad hin- und herbewegt. Anschließend haben wir die erkannten Objekte und ihre entsprechenden Winkel auf einer animierten Oberfläche, die mit Processing PDE erstellt wurde, angezeigt und so ein echtes Radarsystem simuliert.

Wir haben gelernt, wie man Daten von der Arduino-IDE an das Processing PDE über serielle Kommunikation überträgt, wodurch der Datenaustausch zwischen den beiden Programmierplattformen ermöglicht wird. Darüber hinaus haben wir die Grundlagen der Processing-Programmierumgebung erkundet, ein Werkzeug, das verwendet werden kann, um einfache Animationen zu erstellen und Daten effektiv zu visualisieren.

Processing basiert zwar auf Java, bietet aber eine sehr einfache und unkomplizierte Programmiersprache, die auch für Anfänger zugänglich ist. Du wirst ermutigt, Processing weiter zu erforschen, um dessen Fähigkeiten für kreative und visuelle Projekte voll auszuschöpfen. Für weitere Einblicke und Tutorials kannst du dieses Getting Started with Processing-Tutorial besuchen.

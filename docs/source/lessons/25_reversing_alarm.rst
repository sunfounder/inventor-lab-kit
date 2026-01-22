.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche gemeinsam mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Probleme nach dem Verkauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu erkunden und zu kreieren? Klicke auf [|link_sf_facebook|] und trete noch heute bei!

25. Rückfahr-Radarsystem
=====================================

Beim Rückwärtsfahren eines Autos ist es entscheidend, sich der Hindernisse hinter dem Fahrzeug bewusst zu sein, insbesondere in Situationen mit eingeschränkter Sicht.
Um die Sicherheit zu erhöhen, sind viele moderne Fahrzeuge mit Rückfahr-Radarsystemen ausgestattet.

Heute lernen wir, wie man ein Ultraschall-Radarsystem mit Arduino baut und programmiert. Dieses System verwendet einen Ultraschallsensor, um Entfernungen zu messen, und gibt Rückmeldungen über ein LCD-Display und einen Summer. Wir gehen jeden Abschnitt des Codes durch und erklären, was er bewirkt und warum er wichtig ist.

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/25_reverse_alarm.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Entwicklung des Rückfahr-Radarsystems
----------------------------------------

Die Entwicklung von Rückfahr-Radarsystemen, auch bekannt als Einparksensoren, begann im späten 20. Jahrhundert, um den Bedarf an sichererem Fahrzeugparken zu decken. Ursprünglich in den 1970er Jahren unter Verwendung von Ultraschalltechnologie, ähnlich der von Marinesonaren, entwickelt, nutzten diese Systeme Schallwellen, um Objekte zu erkennen und Entfernungen zu berechnen.

Erhebliche Fortschritte gab es in den 1990er Jahren mit der Einführung von mikrocontrollerbasierten Systemen und elektromagnetischen Sensoren, die präzisere Messungen und eine bessere Integration in Fahrzeuge ermöglichten. In dieser Zeit fanden diese Sensoren ihren Weg in Luxusfahrzeuge, was sowohl die Sicherheit als auch den luxuriösen Charme steigerte.

Bis Anfang der 2000er Jahre hatten sich Rückfahr-Radarsysteme so weit entwickelt, dass sie visuelles, akustisches und haptisches Feedback sowie digitale Anzeigen und die Integration in Navigationssysteme boten, um Fahrern Echtzeitinformationen über ihre Umgebung zu liefern.

Heute entwickelt sich die Technologie weiter mit der Integration von KI und IoT, indem eine Mischung aus Kameras, Radar- und Ultraschallsensoren verwendet wird, um einen detaillierten Überblick über die Umgebung des Fahrzeugs zu bieten, das Unfallrisiko zu verringern und das Parken zu erleichtern. Diese Technologie ist mittlerweile ein wesentlicher Bestandteil der autonomen Fahrsysteme, die die Automobilindustrie revolutionieren sollen.

.. image:: img/25_reverse_radar.png
  :width: 600
  :align: center

Aufbau der Schaltung
--------------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Ultraschall-Modul
     - 1 * Aktiver Summer
     - 1 * I2C LCD1602
   * - |list_uno_r3| 
     - |list_ultrasonic| 
     - |list_active_buzzer| 
     - |list_i2c_lcd1602|
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - Verbindungskabel
     - 
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - 

**Schritt-für-Schritt-Anleitung**

Folge dem Schaltplan oder den unten aufgeführten Schritten, um die Schaltung aufzubauen.

.. image:: img/25_reverse_circuit.png
    :width: 700
    :align: center

1. Setze das Ultraschall-Modul in das Steckbrett ein.

.. image:: img/25_reverse_ultrasonic.png
    :width: 400
    :align: center

2. Verbinde den VCC-Pin des Ultraschall-Moduls mit der positiven Seite des Steckbretts, den Trig-Pin mit Pin 8 auf dem Arduino-Board, den Echo-Pin mit Pin 7 und GND mit der negativen Seite des Steckbretts.

.. image:: img/25_reverse_ultrasonic_pins.png
    :width: 400
    :align: center

3. Setze den aktiven Summer (mit weißem Aufkleber) in das Steckbrett ein. Verbinde den "+"-Pin mit Pin 9 und den "-" Pin mit GND.

.. image:: img/25_reverse_pa_buzzer.png
    :width: 400
    :align: center

4. Schließe das I2C LCD1602-Modul an: GND an die negative Schiene des Steckbretts, VCC an die positive Schiene des Steckbretts, SDA an Pin A4 und SCL an Pin A5.

.. image:: img/25_reverse_i2c_lcd1602.png
    :width: 700
    :align: center

5. Schließe abschließend die GND- und 5V-Pins des Arduino Uno R3 an die negative bzw. positive Schiene des Steckbretts an.

.. image:: img/25_reverse_circuit.png
    :width: 700
    :align: center

Code-Erstellung
--------------------
In einem Rückfahr-Radarsystem spielt jede Komponente eine entscheidende Rolle, um eine genaue Entfernungsmessung und effektives Feedback zu gewährleisten:

* Der Ultraschallsensor wird verwendet, um die Entfernung zu Objekten vor ihm zu erkennen.
* Das I2C LCD1602 wird verwendet, um die vom Ultraschallsensor erkannte Entfernung anzuzeigen.
* Der aktive Summer wird verwendet, um das Piepsintervall basierend auf der gemessenen Entfernung durch den Ultraschallsensor zu ändern.

So reagiert das System basierend auf verschiedenen Entfernungsbereichen:

* **Weniger als 10 cm**: Der Summer piept in einem schnellen Intervall von 100 Millisekunden.
* **Zwischen 10 cm und 20 cm**: Das Piepsintervall erhöht sich auf 500 Millisekunden.
* **Zwischen 20 cm und 50 cm**: Das Intervall verlängert sich weiter auf 1000 Millisekunden (1 Sekunde).
* **Größer als 50 cm**: Der Summer piept in einem entspannten Intervall von 2000 Millisekunden (2 Sekunden).

Nun lasst uns mit der Codierung beginnen, um zu sehen, wie wir die oben beschriebene Funktionalität implementieren können.

.. note::

  Wenn du mit dem Ultraschallsensor, dem I2C LCD1602 oder dem aktiven Summer nicht vertraut bist, kannst du deren grundlegende Verwendung in den folgenden Projekten erlernen:

  * :ref:`ar_i2c_lcd1602`
  * :ref:`ar_smart_trash_can`
  * :ref:`ar_morse_code`

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „New Sketch“ aus dem Menü „File“ auswählst.
2. Speichere deinen Sketch unter dem Namen ``Lesson25_Reverse_Radar_System`` mit ``Ctrl + S`` oder durch Klicken auf „Save“.

3. Zunächst binden wir die erforderlichen Bibliotheken zur Verwendung des LCDs ein und initialisieren es mit der richtigen I2C-Adresse und Größe.

.. note::

  Hier wird die ``LiquidCrystal I2C``-Bibliothek verwendet, die du über den **Library Manager** installieren kannst.

.. code-block:: Arduino

  #include <Wire.h>
  #include <LiquidCrystal_I2C.h>

  // Initialisiere das LCD mit der I2C-Adresse 0x27 und der Größe 16x2
  LiquidCrystal_I2C lcd(0x27, 16, 2);

4. Definiere als Nächstes die Pins am Arduino, die mit dem Trigger, Echo des Ultraschallsensors und dem Summer verbunden sind.

.. code-block:: Arduino

  #define TRIGGER_PIN 8  // Pin zum Auslösen des Ultraschallpulses
  #define ECHO_PIN 7     // Pin zum Empfangen des Echos
  #define BUZZER_PIN 9   // Pin für den Summer

5. Lege Variablen fest, um zu steuern, wie häufig der Summer basierend auf der gemessenen Entfernung piept.

.. code-block:: Arduino

  // Zeitsteuerungsvariablen zur Kontrolle der Piepsfrequenz basierend auf der Entfernung
  unsigned long intervals = 1000;    // Standardintervall für das Piepsen
  unsigned long previousMillis = 0;  // Speichert die letzte Zeit, zu der der Summer piepte

  // Variable zur Entfernungsmesung
  long distance = 0;

6. In der Funktion ``void setup()``, konfiguriere die Pin-Modi und initialisiere das LCD sowie die serielle Kommunikation.

.. code-block:: Arduino

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Setze den Trigger-Pin als Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setze den Echo-Pin als Eingang
    pinMode(BUZZER_PIN, OUTPUT);   // Setze den Summer-Pin als Ausgang
    lcd.init();                    // Initialisiere das LCD
    lcd.backlight();               // Schalte die LCD-Hintergrundbeleuchtung ein
    Serial.begin(9600);            // Starte die serielle Kommunikation mit 9600 Baud
  }

7. Die Hauptschleife misst kontinuierlich die Entfernung, passt das Piepsintervall an und aktualisiert das LCD-Display.

.. code-block:: Arduino

  void loop() {
    distance = measureDistance();  // Messe die Entfernung

    // Passe die Intervalle basierend auf der Entfernung an
    adjustBeepingInterval();

    unsigned long currentMillis = millis();  // Hole die aktuelle Zeit
    // Überprüfe, ob es Zeit ist zu piepen
    if (currentMillis - previousMillis >= intervals) {
      Serial.println("Beeping!");
      beep();
      previousMillis = currentMillis;  // Aktualisiere previousMillis direkt hier
    }

    updateLCD();  // Aktualisiere das LCD-Display
    delay(100);   // Kurze Verzögerung zur Stabilisierung der Messwerte
  }

* Zuerst verwenden wir die Funktion ``measureDistance()``, um die Entfernung mit dem Ultraschallsensor zu bestimmen.

.. code-block:: Arduino

  distance = measureDistance();  // Messe die Entfernung

* Als Nächstes passen wir die Piepsfrequenz basierend auf der neu gemessenen Entfernung mit der Funktion ``adjustBeepingInterval()`` an. Dies ändert dynamisch, wie oft der Summer ertönt, je nachdem, wie nah das erkannte Objekt ist.

.. code-block:: Arduino

  // Passe die Intervalle basierend auf der Entfernung an
  adjustBeepingInterval();

* Die Funktion ``millis()`` wird dann aufgerufen, um die aktuelle Zeit in Millisekunden zu erfassen, seitdem das Arduino-Board das Programm gestartet hat.

.. code-block:: Arduino

  unsigned long currentMillis = millis();

* Überprüfe, ob die seit dem letzten Piepsen vergangene Zeit größer oder gleich dem eingestellten Intervall ist. Falls ja, wird eine Nachricht an den seriellen Monitor ausgegeben, der Summer aktiviert und ``previousMillis`` zurückgesetzt. Dies stellt sicher, dass der Summer in Abständen piept, die der gemessenen Entfernung entsprechen, und die Warnintervalle konsistent bleiben.

.. code-block:: Arduino
  
  if (currentMillis - previousMillis >= intervals) {
    Serial.println("Beeping!");
    beep();
    previousMillis = currentMillis;  // Aktualisiere previousMillis direkt hier
  }

* Schließlich wird die Funktion ``updateLCD()`` aufgerufen, um das LCD-Display mit der aktuellen Entfernungsanzeige zu aktualisieren.

.. code-block:: Arduino

  updateLCD();  // Aktualisiere das LCD-Display

8. Zur Funktion ``adjustBeepingInterval()``: Diese passt das Piepsintervall basierend auf der gemessenen Entfernung an. Die Funktion setzt die Variable ``intervals``. Je näher das Objekt ist, desto kürzer wird das Intervall, wodurch der Summer häufiger piept, je näher sich Objekte befinden.

.. code-block:: Arduino

  // Funktion zur Anpassung der Intervalle basierend auf der Entfernung
  void adjustBeepingInterval() {
    if (distance <= 10) {
      intervals = 100;
    } else if (distance <= 20) {
      intervals = 500;
    } else if (distance <= 50) {
      intervals = 1000;
    } else {
      intervals = 2000;
    }
  }
  
9. Über die ``beep()``-Funktion: Schaltet den Summer ein und nach einer kurzen Pause wieder aus.

.. code-block:: Arduino

  // Funktion, um den Summer piepen zu lassen
  void beep() {
    digitalWrite(BUZZER_PIN, HIGH);  // Schaltet den Summer EIN
    delay(100);                      // Piepdauer: 100 Millisekunden
    digitalWrite(BUZZER_PIN, LOW);   // Schaltet den Summer AUS
  }

10. Über die Funktion ``measureDistance()``: Misst die Entfernung mithilfe des Ultraschallsensors. Diese Funktion sendet Ultraschallwellen aus und misst, wie lange es dauert, bis das Echo zurückkehrt. Die ``distance`` wird basierend auf der Laufzeit dieser Wellen berechnet.

.. code-block:: Arduino

  // Funktion zur Messung der Entfernung mithilfe des Ultraschallsensors
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Sicherstellen, dass der Trigger-Pin niedrig ist
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Sende einen hohen Impuls
    delayMicroseconds(10);            // Impulsdauer
    digitalWrite(TRIGGER_PIN, LOW);   // Beende den Impuls

    long duration = pulseIn(ECHO_PIN, HIGH);  // Messe die Dauer des hohen Pegels am Echo-Pin
    long distance = duration * 0.034 / 2;     // Berechne die Entfernung in cm
    return distance;
  }

11. Über die Funktion ``updateLCD()``: Aktualisiert das LCD nur, wenn sich die gemessene Entfernung ändert, um unnötige Updates zu vermeiden. Es zeigt die aktuelle Entfernung auf dem LCD an.

.. code-block:: Arduino

  // Funktion zum Aktualisieren des LCD-Displays mit der Entfernung
  void updateLCD() {
    static float lastDistance = -1;  // Speichert die zuletzt angezeigte Entfernung
    if (distance != lastDistance) {
      lcd.clear();          // Lösche das LCD-Display
      lcd.setCursor(0, 0);  // Setze den Cursor an den Anfang
      lcd.print("Dis: ");
      lcd.print(distance);
      lcd.print(" cm");
      lastDistance = distance;  // Aktualisiere die zuletzt angezeigte Entfernung
    }
  }

12. Jetzt, da du alle Teile des Codes geschrieben hast, lade ihn auf dein Arduino-Board hoch, um zu sehen, ob alles wie erwartet funktioniert.

.. code-block:: Arduino

  #include <Wire.h>
  #include <LiquidCrystal_I2C.h>

  // Initialisiere das LCD mit der I2C-Adresse 0x27 und der Größe 16x2
  LiquidCrystal_I2C lcd(0x27, 16, 2);

  #define TRIGGER_PIN 8  // Pin zum Auslösen des Ultraschallpulses
  #define ECHO_PIN 7     // Pin zum Empfangen des Echos
  #define BUZZER_PIN 9   // Pin für den Summer

  // Zeitsteuerungsvariablen zur Kontrolle der Piepsfrequenz basierend auf der Entfernung
  unsigned long intervals = 1000;    // Standardintervall für das Piepsen
  unsigned long previousMillis = 0;  // Speichert die letzte Zeit, zu der der Summer piepte

  // Variable zur Entfernungsmesung
  long distance = 0;

  void setup() {
    pinMode(TRIGGER_PIN, OUTPUT);  // Setze den Trigger-Pin als Ausgang
    pinMode(ECHO_PIN, INPUT);      // Setze den Echo-Pin als Eingang
    pinMode(BUZZER_PIN, OUTPUT);   // Setze den Summer-Pin als Ausgang
    lcd.init();                    // Initialisiere das LCD
    lcd.backlight();               // Schalte die LCD-Hintergrundbeleuchtung ein
    Serial.begin(9600);            // Starte die serielle Kommunikation mit 9600 Baud
  }

  void loop() {
    distance = measureDistance();  // Messe die Entfernung

    // Passe die Intervalle basierend auf der Entfernung an
    adjustBeepingInterval();

    unsigned long currentMillis = millis();  // Hole die aktuelle Zeit
    // Überprüfe, ob es Zeit ist zu piepen
    if (currentMillis - previousMillis >= intervals) {
      Serial.println("Beeping!");
      beep();
      previousMillis = currentMillis;  // Aktualisiere previousMillis direkt hier
    }

    updateLCD();  // Aktualisiere das LCD-Display
    delay(100);   // Kurze Verzögerung zur Stabilisierung der Messwerte
  }

  // Funktion zur Anpassung der Intervalle basierend auf der Entfernung
  void adjustBeepingInterval() {
    if (distance <= 10) {
      intervals = 100;
    } else if (distance <= 20) {
      intervals = 500;
    } else if (distance <= 50) {
      intervals = 1000;
    } else {
      intervals = 2000;
    }
  }

  // Funktion, um den Summer piepen zu lassen
  void beep() {
    digitalWrite(BUZZER_PIN, HIGH);  // Schaltet den Summer EIN
    delay(100);                      // Piepdauer: 100 Millisekunden
    digitalWrite(BUZZER_PIN, LOW);   // Schaltet den Summer AUS
  }

  // Funktion zur Messung der Entfernung mithilfe des Ultraschallsensors
  long measureDistance() {
    digitalWrite(TRIGGER_PIN, LOW);  // Sicherstellen, dass der Trigger-Pin niedrig ist
    delayMicroseconds(2);
    digitalWrite(TRIGGER_PIN, HIGH);  // Sende einen hohen Impuls
    delayMicroseconds(10);            // Impulsdauer
    digitalWrite(TRIGGER_PIN, LOW);   // Beende den Impuls

    long duration = pulseIn(ECHO_PIN, HIGH);  // Messe die Dauer des hohen Pegels am Echo-Pin
    long distance = duration * 0.034 / 2;     // Berechne die Entfernung in cm
    return distance;
  }

  // Funktion zum Aktualisieren des LCD-Displays mit der Entfernung
  void updateLCD() {
    static float lastDistance = -1;  // Speichert die zuletzt angezeigte Entfernung
    if (distance != lastDistance) {
      lcd.clear();          // Lösche das LCD-Display
      lcd.setCursor(0, 0);  // Setze den Cursor an den Anfang
      lcd.print("Dis: ");
      lcd.print(distance);
      lcd.print(" cm");
      lastDistance = distance;  // Aktualisiere die zuletzt angezeigte Entfernung
    }
  }


13. Speichere abschließend deinen Code und räume deinen Arbeitsplatz auf.

**Frage**

In diesem Projekt haben wir einen aktiven Summer als Alarmsystem verwendet, aber auch ein passiver Summer könnte ähnliche Funktionen erfüllen. Wie müsste der Code angepasst werden, wenn du den aktiven durch einen passiven Summer ersetzt?

**Zusammenfassung**

Im Laufe dieses Kurses haben wir den Weg von der konzeptionellen Erfassung bis zur praktischen Implementierung eines Rückfahr-Radarsystems durchlaufen. Beginnend mit dem Aufbau der Schaltung auf einem Breadboard, haben wir einen Ultraschallsensor, einen aktiven Summer und ein LCD-Display mit einem Arduino-Board verbunden. Nach der Hardware-Einrichtung haben wir uns dem Codieren gewidmet, wobei du gelernt hast, Sensordaten zu verarbeiten, um akustische und visuelle Rückmeldungen basierend auf der Entfernung von Hindernissen hinter einem Fahrzeug auszulösen.

Du hast nun erfolgreich dein Arduino so programmiert, dass es Entfernungen misst und Alarme durch einen Summer und visuelle Rückmeldungen über ein LCD ausgibt, ähnlich wie bei fortschrittlichen Rückfahrradarsystemen moderner Autos. Dies zeigt nicht nur deine Fähigkeit, verschiedene elektronische Komponenten zu integrieren, sondern auch deine Kompetenz, ein System zu erstellen, das die Fahrzeugsicherheit verbessern könnte.

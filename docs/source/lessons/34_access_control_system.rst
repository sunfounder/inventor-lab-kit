.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein und tausche dich mit anderen Begeisterten aus.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und festlichen Aktionen teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

34. Zugangskontrollsystem
===============================
Willkommen zu unserem interaktiven Workshop zum Aufbau eines Zugangskontrollsystems mit Arduino! Dieser Kurs richtet sich an Enthusiasten, die tiefer in die Welt der Elektronik, Robotik und Programmierung eintauchen möchten. Du erhältst praktische Erfahrungen mit Schrittmotoren, RFID-Technologie und LCD-Displays, indem du ein praxisnahes Projekt erstellst, das du in realen Szenarien einsetzen kannst. Egal, ob du deine Haussicherheit verbessern möchtest oder einfach neugierig auf elektronische Systeme bist, dieser Kurs bietet eine umfassende Anleitung zum Verständnis und zur Implementierung grundlegender Automatisierungs- und Steuerungssysteme.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/34_access_control_system.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Am Ende dieses Kurses wirst du in der Lage sein:

* Die Funktionsweise von Schrittmotoren zu verstehen und wie sie mechanische Bewegungen erzeugen können.
* Die Funktionalität der RFID-Technologie zu erkunden und zu erfahren, wie sie in Projekte zur sicheren Zugangskontrolle integriert werden kann.
* Ein I2C-LCD-Display an Arduino zu programmieren und anzuschließen, um Benutzerfeedback und Systemstatusmeldungen bereitzustellen.
* Ein einfaches Zugangskontrollsystem zu entwerfen und zu implementieren, das RFID-Technologie verwendet, um basierend auf programmierten Kriterien den Zugang zu gewähren oder zu verweigern.

Über den Schrittmotor und das ULN2003-Modul
------------------------------------------------

**Schrittmotor**

Der 28BYJ-48 ist ein 5-adriger unipolarer Schrittmotor, der mit 5V betrieben wird. Schrittmotoren sind Präzisionsmotoren, die sehr genau gesteuert werden können, ohne Rückmeldung von Sensoren zu benötigen. Dies liegt daran, dass die Motorwelle mit Magneten ausgestattet ist und durch elektromagnetische Spulen gesteuert wird, die in einer bestimmten Reihenfolge ein- und ausgeschaltet werden, wodurch sich die Welle in präzisen kleinen Schritten bewegt.

.. image:: img/34_step_stepper.png
  :align: center

Der Stator des von uns verwendeten Schrittmotors hat 32 magnetische Pole, sodass ein Kreis 32 Schritte benötigt. Die Ausgangswelle des Schrittmotors ist mit einem Untersetzungsgetriebe verbunden, und das Untersetzungsverhältnis beträgt 1/64. Daher benötigt die endgültige Ausgangswelle für eine volle Umdrehung 32 * 64 = 2048 Schritte.

**Wie ein Unipolar-Schrittmotor funktioniert**

Ein unipolarer Schrittmotor hat typischerweise vier Phasen und arbeitet mit Gleichstrom. Durch korrektes Timing des elektrischen Stroms zu den Phasen des Motors kann der Motor Schritt für Schritt gedreht werden. Stell dir vor, dass das Zentrum des Motors ein zahnradförmiger Magnet (der Rotor) ist, der von mehreren Zähnen mit den Nummern 0 bis 5 umgeben ist. Um diese Zähne herum befinden sich acht magnetische Pole, die in Paaren (A bis D) angeordnet sind und durch Spulen verbunden sind.

.. image:: img/34_step_interal.png
  :align: center

Wenn du verschiedene Schalter einschaltest, die mit diesen Spulen verbunden sind (beschriftet mit SA, SB, SC und SD), steuerst du, welche magnetischen Pole aktiviert werden. Zum Beispiel, wenn Schalter SB eingeschaltet ist (und die anderen ausgeschaltet sind), richten sich die magnetischen Pole B an bestimmten Zähnen des Rotors aus, wodurch dieser sich bewegt. Wenn du den Schalter SC als nächstes einschaltest, dreht sich der Rotor, um sich mit den magnetischen Polen C auszurichten, und so weiter. Durch das Durchschalten der Schalter A, B, C und D dreht sich der Rotor kontinuierlich.

**ULN2003-Modul**

.. image:: img/34_step_uln2003.png
    :align: center

Das ULN2003-Schrittmotor-Treibermodul ist entscheidend für die Integration des Schrittmotors in Schaltungen. Es funktioniert als 7-Kanal-Inverter, was bedeutet, dass es Eingangssignale in die benötigten Ausgangsaktionen für den Motor umwandelt. Zum Beispiel, wenn ein hohes Signal an IN1 gesendet wird und niedrige Signale an IN2, IN3 und IN4, dann wird OUT1 niedrig und die anderen Ausgänge bleiben hoch, wodurch sich der Motor um einen Schritt dreht. Durch das Bereitstellen spezifischer Sequenzen wie dieser kann der Motor sanft Schritt für Schritt rotieren. Der ULN2003 vereinfacht die Steuerung der Zeitsequenzen, die für den Betrieb des Motors erforderlich sind.

Baue die Schaltung
------------------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RFID-Modul und Tag
     - 1 * I2C LCD1602
     - 1 * Schrittmotor
   * - |list_uno_r3|
     - |list_rc522_module| 
     - |list_i2c_lcd1602|
     - |list_stepper|
   * - 1 * ULN2003-Modul
     - Steckbrücken
     - 1 * Steckbrett
     - 1 * USB-Kabel
   * - |list_uln2003_module|
     - |list_wire|
     - |list_breadboard|
     - |list_usb_cable|
   * - 1 * Steckbrett-Stromversorgung
     - 1 * 9V-Batterie
     - 1 * Batterieanschlusskabel
     - 
   * - |list_power_module| 
     - |list_battery| 
     - |list_bat_cable| 
     -

**Aufbauschritte**

Folge dem Schaltplan oder den unten aufgeführten Schritten, um deine Schaltung aufzubauen.

.. image:: img/34_step_connect_lcd.png
    :width: 700
    :align: center

1. Stecke den Schrittmotor in das ULN2003-Treiberboard.

.. image:: img/34_step_connect_uln2003_stepper.png
  :width: 500
  :align: center


2. Beim Einsatz von Motoren, Servos und anderen Aktuatoren wird empfohlen, eine externe Stromversorgung zu verwenden, um eine Beschädigung der Hauptplatine zu vermeiden. Stecke das Steckbrett-Stromversorgungsmodul in das Steckbrett und verbinde dann mit einem Steckbrücken-Kabel die negative Schiene des Steckbretts mit dem GND des Arduino Uno R3, um eine gemeinsame Masse zu erreichen.

.. image:: img/14_dinosaur_power_module.png
    :width: 400
    :align: center

.. note::

    Die Reihenfolge der positiven und negativen Anschlüsse auf dem Steckbrett im Schaltplan ist im Vergleich zu dem im Kit enthaltenen Steckbrett umgekehrt.

    Beim tatsächlichen Verdrahten musst du das Steckbrett-Stromversorgungsmodul von der Seite mit der höheren Nummer (60~65) einstecken, damit das "-" des Stromversorgungsmoduls in die negative Schiene "-" des Steckbretts geht und das "+" in die positive Schiene "+".

  .. raw:: html

      <video controls style = "max-width:100%">
          <source src="_static/video/about_power_module.mp4" type="video/mp4">
          Your browser does not support the video tag.
      </video>

3. Verbinde IN1 des ULN2003 mit Arduino Uno R3 Pin 2, IN2 mit Pin 4, IN3 mit Pin 3 und IN4 mit Pin 5.

.. image:: img/34_step_connect_uln2003.png
  :width: 700
  :align: center

4. Verbinde nun das "-" des ULN2003-Moduls mit dem negativen Anschluss des Steckbretts und "+" mit dem positiven Anschluss.

.. image:: img/34_step_connect_power.png
  :width: 700
  :align: center

5. Verbinde das RC522-RFID-Modul mit dem Arduino Uno R3.

.. list-table::
    :widths: 20 20
    :header-rows: 1

    *   - RC522-RFID
        - Arduino UNO R3
    *   - 3.3V
        - 3.3V
    *   - RST
        - 9
    *   - GND
        - Negative Schiene auf dem Steckbrett
    *   - IRQ
        -
    *   - MISO
        - 12
    *   - MOSI
        - 11
    *   - SCK
        - 13
    *   - SDA
        - 10

.. image:: img/34_step_connect_rfid.png
  :width: 700
  :align: center

6. Verbinde abschließend das I2C LCD1602-Modul: GND mit GND auf dem Arduino Uno R3, VCC mit dem 5V-Pin, SDA mit Pin A4 und SCL mit Pin A5.

.. image:: img/34_step_connect_lcd.png
    :width: 700
    :align: center


Code-Erstellung - Den Schrittmotor drehen lassen
------------------------------------------------------------
Jetzt werden wir den Code verwenden, um den Schrittmotor zu drehen.

1. Öffne die Arduino-IDE und starte ein neues Projekt, indem du im Menü „Datei“ die Option „Neuer Sketch“ auswählst.
2. Speichere deinen Sketch unter dem Namen ``Lesson34_Stepper_Motor`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Füge die notwendige Bibliothek für den Schrittmotor hinzu.

.. code-block:: Arduino
  :emphasize-lines: 1

  #include <Stepper.h>  // Füge die Stepper-Bibliothek hinzu

  void setup() {
    // Hier kommt der Setup-Code hin, der einmal ausgeführt wird:

  }

4. Definiere die Anzahl der Schritte pro Umdrehung des Motors, initialisiere das Stepper-Objekt und setze die Pin-Verbindungen (IN1, IN3, IN2, IN4).

.. code-block:: Arduino
  :emphasize-lines: 4,7

  #include <Stepper.h>  // Füge die Stepper-Bibliothek hinzu

  // Definiere die Anzahl der Schritte pro Umdrehung des Motors
  #define STEPS 2048

  // Initialisiere das Stepper-Objekt und setze die Pin-Verbindungen (IN1, IN3, IN2, IN4)
  Stepper stepper(STEPS, 2, 3, 4, 5);

  void setup() {
    // Hier kommt der Setup-Code hin, der einmal ausgeführt wird:

  }

5. Im ``setup()``-Abschnitt muss nichts initialisiert werden, also lass ihn leer. Im ``loop()``-Abschnitt wird die Drehgeschwindigkeit des Schrittmotors auf 5 U/min eingestellt, er dreht sich 512 Schritte, pausiert für eine Sekunde und setzt dann die Drehung mit 5 U/min für weitere 512 Schritte fort.

.. note::

  Aus der vorherigen Diskussion wissen wir, dass der Schrittmotor 2048 Schritte benötigt, um eine vollständige Umdrehung zu machen. Wenn du die Schrittanzahl auf 512 setzt, entspricht das einer 1/4 Umdrehung. Somit benötigt er vier Sekunden, um eine vollständige Umdrehung abzuschließen.


.. code-block:: Arduino
  :emphasize-lines: 7-9

  void setup() {
    // Hier kommt der Setup-Code hin, der einmal ausgeführt wird:
  }

  void loop() {
    // Im Uhrzeigersinn mit 5 U/min drehen
    stepper.setSpeed(5);
    stepper.step(512);  // Drehe 1/4 Umdrehung
    delay(1000);        // Warte 1 Sekunde
  }

* ``setSpeed(rpms)``: Legt die Drehgeschwindigkeit des Motors in Umdrehungen pro Minute (RPM) fest. Diese Funktion sorgt nicht dafür, dass der Motor sich dreht, sondern legt lediglich die Geschwindigkeit fest, mit der er sich dreht, wenn du ``step()`` aufrufst.

  * ``rpms``: Die Geschwindigkeit, mit der sich der Motor in Umdrehungen pro Minute drehen soll – eine positive Zahl (long).

* ``step(steps)``: Diese Funktion dreht den Motor um die angegebene Anzahl von Schritten unter Verwendung der in ``setSpeed()`` zuletzt festgelegten Geschwindigkeit. Wichtig ist, dass diese Funktion blockierend arbeitet, das heißt, sie wartet, bis der Motor seine Bewegung abgeschlossen hat, bevor sie zur nächsten Zeile im Sketch übergeht. Wenn du zum Beispiel die Geschwindigkeit auf 1 U/min einstellst und ``step(2048)`` aufrufst, würde der Motor eine volle Minute benötigen, um diese Funktion auszuführen. Um eine präzisere Steuerung zu erreichen, empfiehlt es sich, eine höhere Geschwindigkeit beizubehalten und nur wenige Schritte mit jedem Aufruf von ``step()`` zu machen.

  * ``steps``: Die Anzahl der Schritte, um die der Motor gedreht werden soll – positiv für eine Richtung, negativ für die andere (int).

6. Hier ist dein vollständiger Code, den du auf das Arduino-Board hochladen kannst. Danach wirst du sehen, wie sich der Schrittmotor jede Sekunde um 1/4 Umdrehung dreht und in vier Sekunden eine vollständige Umdrehung abschließt.

.. code-block:: Arduino

  #include <Stepper.h>  // Füge die Stepper-Bibliothek hinzu

  // Definiere die Anzahl der Schritte pro Umdrehung des Motors
  #define STEPS 2048

  // Initialisiere das Stepper-Objekt und setze die Pin-Verbindungen (IN1, IN3, IN2, IN4)
  Stepper stepper(STEPS, 2, 3, 4, 5);

  void setup() {
    // Hier kommt der Setup-Code hin, der einmal ausgeführt wird:
  }

  void loop() {
    // Im Uhrzeigersinn mit 5 U/min drehen
    stepper.setSpeed(5);
    stepper.step(512);  // Drehe 1/4 Umdrehung
    delay(1000);        // Warte 1 Sekunde
  }
  
**Frage**

Wenn Sie eine vollständige Umdrehung in eine Richtung und dann eine vollständige Umdrehung in die entgegengesetzte Richtung erreichen möchten, wie sollte der Code entsprechend angepasst werden?


Code-Erstellung - Zugangskontrollsystem
------------------------------------------
Im vorherigen Projekt haben wir gelernt, wie man einen Schrittmotor mit Code steuert. Nun wollen wir einen Schrittmotor, ein I2C LCD1602 und ein RC522-RFID-Modul verwenden, um ein Zugangskontrollsystem zu erstellen.

* Der Schrittmotor wird verwendet, um das Öffnen und Schließen einer Tür zu simulieren.
* Das RC522-RFID-Modul dient dazu, die Karten oder Tags von Besuchern zu scannen. Wenn die ID mit der vordefinierten übereinstimmt, wird der Schrittmotor aktiviert.
* Das I2C LCD1602-Modul zeigt die Ergebnisse des Kartenscans an.

Lassen Sie uns nun den Code schreiben, um zu sehen, wie dieses Zugangskontrollsystem implementiert wird.

.. note::

  Wenn Sie mit dem MCRF522-Modul und dem I2C LCD1602 nicht vertraut sind, können Sie deren grundlegende Verwendung zunächst durch die folgenden Projekte erlernen:

  * :ref:`ar_rfid_module`
  * :ref:`ar_i2c_lcd1602`

  Hier werden die Bibliotheken ``LiquidCrystal I2C`` und ``MFRC522`` verwendet, die Sie über den **Library Manager** installieren können.

1. Öffnen Sie die Arduino-IDE und starten Sie ein neues Projekt, indem Sie im Menü „Datei“ die Option „Neuer Sketch“ auswählen.
2. Speichern Sie Ihren Sketch unter dem Namen ``Lesson34_Stepper_Motor`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Fügen Sie die notwendigen Bibliotheken für die I2C- und SPI-Kommunikation hinzu, dann fügen Sie die Bibliotheken für das RFID-Modul, das I2C LCD und den Schrittmotor hinzu.

.. code-block:: Arduino

  #include <SPI.h>                // Fügen Sie die SPI-Bibliothek für die SPI-Kommunikation hinzu
  #include <MFRC522.h>            // Fügen Sie die Bibliothek für das RFID-Modul hinzu
  #include <Wire.h>               // Fügen Sie die Wire-Bibliothek für die I2C-Kommunikation hinzu
  #include <LiquidCrystal_I2C.h>  // Fügen Sie die Bibliothek für das I2C LCD hinzu
  #include <Stepper.h>            // Fügen Sie die Bibliothek für den Schrittmotor hinzu

4. Initialisieren Sie den RFID-Leser und das LCD-Display mit den angegebenen Pin-Verbindungen und LCD-Dimensionen/-Konfiguration (Adresse 0x27, 16 Spalten, 2 Reihen). Definieren Sie die Anzahl der Schritte pro Umdrehung für den Motor, initialisieren Sie das Stepper-Objekt und setzen Sie die Pin-Verbindungen (IN1, IN3, IN2, IN4).

.. code-block:: Arduino
  :emphasize-lines: 7-17

  #include <SPI.h>                // Fügen Sie die SPI-Bibliothek für die SPI-Kommunikation hinzu
  #include <MFRC522.h>            // Fügen Sie die Bibliothek für das RFID-Modul hinzu
  #include <Wire.h>               // Fügen Sie die Wire-Bibliothek für die I2C-Kommunikation hinzu
  #include <LiquidCrystal_I2C.h>  // Fügen Sie die Bibliothek für das I2C LCD hinzu
  #include <Stepper.h>            // Fügen Sie die Bibliothek für den Schrittmotor hinzu

  #define RST_PIN 9  // Reset-Pin für das RFID-Modul
  #define SS_PIN 10  // Slave-Select-Pin für das RFID-Modul

  // Erstellen Sie eine Instanz der MFRC522-Klasse, um mit dem RFID-Modul zu interagieren
  MFRC522 mfrc522(SS_PIN, RST_PIN);
  // Erstellen Sie eine Instanz der LiquidCrystal_I2C-Klasse für das LCD
  LiquidCrystal_I2C lcd(0x27, 16, 2);

  // Definieren Sie die Konfiguration des Schrittmotors
  const int stepsPerRevolution = 2048;              // Gesamtanzahl der Schritte pro Umdrehung
  Stepper stepper(stepsPerRevolution, 2, 3, 4, 5);  // Pins für den Schrittmotor (IN1, IN2, IN3, IN4)

5. Setzen Sie die Anzahl der Schritte für den Schrittmotor und die UID für den autorisierten Zugang.

.. code-block:: Arduino
  :emphasize-lines: 1,4

  int doorStep = 512;  // Schritte, um die Tür um 90 Grad zu öffnen

  // UID für autorisierten Zugang
  const byte authorizedUID[4] = { 0x9B, 0x2F, 0x0A, 0x11 };

  void setup() {
    // Hier kommt der Setup-Code hin, der einmal ausgeführt wird:

  }

6. Die Funktion ``setup()`` initialisiert die serielle Kommunikation, den SPI-Bus, den RFID-Leser, den Schrittmotor und das LCD. Es wird die Hintergrundbeleuchtung des LCD eingerichtet und eine Bereitschaftsnachricht an den seriellen Monitor gesendet.
 
.. code-block:: Arduino

  void setup() {
    Serial.begin(9600);
    SPI.begin();
    mfrc522.PCD_Init();    // Initialisieren Sie den RFID-Leser
    stepper.setSpeed(15);  // Stellen Sie die Geschwindigkeit des Schrittmotors auf 15 U/min ein

    // Initialisieren Sie das LCD-Display
    lcd.init();
    lcd.backlight();
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Scan your card");
    Serial.println("Ready to read a card");
  }

7. In der Funktion ``loop()``:

* Überprüft kontinuierlich, ob neue RFID-Karten vorhanden sind, liest deren UID und validiert sie gegen eine autorisierte Liste.
* Wenn die ID der Karte mit der festgelegten übereinstimmt, wird ``grantAccess()`` aufgerufen, um relevante Informationen auf dem LCD anzuzeigen und die Tür mit dem Schrittmotor zu öffnen. Die Tür schließt sich nach 5 Sekunden.
* Wenn die ID der Karte nicht mit der festgelegten übereinstimmt, wird ``denyAccess()`` aufgerufen, um eine Zugriffsverweigerungsnachricht anzuzeigen.
* Schließlich wird die Kartenkommunikation gestoppt und die Verschlüsselung beendet. Eine Verzögerung ermöglicht es, die angezeigten Informationen zu lesen, bevor das LCD gelöscht wird, um es für die nächste Karte vorzubereiten.

.. code-block:: Arduino

  void loop() {
    // Überprüfen Sie, ob eine neue Karte vorhanden ist
    if (!mfrc522.PICC_IsNewCardPresent() || !mfrc522.PICC_ReadCardSerial()) {
      return;  // Schleife beenden, wenn keine neue Karte vorhanden ist
    }

    // Erstellen und zeigen Sie die UID der Karte an
    String uidStr = buildUIDString();
    Serial.print("Card ID: ");
    Serial.println(uidStr);

    // Überprüfen Sie die Kartenautorisierung und reagieren Sie entsprechend
    if (isAuthorized(mfrc522.uid.uidByte)) {
      grantAccess();
    } else {
      denyAccess();
    }

    delay(3000);  // Verzögerung vor dem nächsten Kartenlesevorgang
    lcd.clear();
    lcd.print("Scan your card");

    // Beenden Sie die Kartenkommunikation und stoppen Sie die Verschlüsselung
    mfrc522.PICC_HaltA();
    mfrc522.PCD_StopCrypto1();
  }

8. ``buildUIDString()`` Funktion:

* Erstellt eine formatierte Zeichenkette der UID der RFID-Karte zur einfachen Anzeige.
* Jedes Byte der UID wird in Hexadezimal umgewandelt und durch Doppelpunkte getrennt.

.. code-block:: Arduino

  String buildUIDString() {
    String uidStr = "";  // Speichern Sie die UID als Zeichenkette zur Anzeige
    for (byte i = 0; i < mfrc522.uid.size; i++) {
      char buff[3];
      sprintf(buff, "%02X", mfrc522.uid.uidByte[i]);
      uidStr += buff;
      if (i < mfrc522.uid.size - 1) uidStr += ":";
    }
    return uidStr;
  }
  
9. ``grantAccess()`` Funktion: 

* Steuert den Schrittmotor, um die Tür zu öffnen und später wieder zu schließen.
* Zeigt Begrüßungsnachrichten auf dem LCD an.
* Verwaltet den Stromverbrauch effizient, indem der Motor deaktiviert wird, wenn er nicht in Gebrauch ist.

.. code-block:: Arduino

  void grantAccess() {
    lcd.clear();
    lcd.print("Welcome!");
    lcd.setCursor(0, 1);
    lcd.print("Door Opening...");
    stepper.step(doorStep);   // Tür öffnen
    savePower();              // Energiesparfunktion nach Motoraktivität
    delay(5000);              // Simuliert, dass die Tür eine Weile offen bleibt
    stepper.step(-doorStep);  // Tür schließen
    savePower();              // Energiesparfunktion nach Motoraktivität
  }

10. ``denyAccess()`` Funktion: Informiert den Benutzer über das LCD, dass der Zugang aufgrund einer unzulässigen oder nicht autorisierten RFID-Karte verweigert wurde.

.. code-block:: Arduino

  void denyAccess() {
    lcd.clear();
    lcd.print("Access Denied");
    lcd.setCursor(0, 1);
    lcd.print("Invalid Card");
  }

11. ``savePower()`` Funktion: Schaltet alle Pins, die mit dem Schrittmotor verbunden sind, ab, um den Stromverbrauch zu reduzieren, wenn der Motor nicht aktiv ist.

.. code-block:: Arduino

  void savePower() {
    // Deaktiviert alle Schrittmotor-Pins, um Strom zu sparen
    digitalWrite(2, LOW);
    digitalWrite(3, LOW);
    digitalWrite(4, LOW);
    digitalWrite(5, LOW);
  }

12. ``isAuthorized(byte *uid)`` Funktion:

* Vergleicht die gescannte UID mit einer vordefinierten Liste autorisierter UIDs.
* Bestimmt, ob der Zugang gewährt oder verweigert wird, basierend auf diesem Vergleich.

.. code-block:: Arduino

  bool isAuthorized(byte *uid) {
    // Überprüft, ob die gescannte UID mit der autorisierten UID übereinstimmt
    for (byte i = 0; i < 4; i++) {
      if (uid[i] != authorizedUID[i]) {
        return false;  // Gibt false zurück, wenn ein Byte nicht übereinstimmt
      }
    }
    return true;  // Gibt true zurück, wenn alle Bytes übereinstimmen
  }

13. Hier ist Ihr vollständiger Code, den Sie auf das Arduino-Board hochladen können.

.. code-block:: Arduino

  #include <SPI.h>                // Fügen Sie die SPI-Bibliothek für die SPI-Kommunikation hinzu
  #include <MFRC522.h>            // Fügen Sie die Bibliothek für das RFID-Modul hinzu
  #include <Wire.h>               // Fügen Sie die Wire-Bibliothek für die I2C-Kommunikation hinzu
  #include <LiquidCrystal_I2C.h>  // Fügen Sie die Bibliothek für das I2C LCD hinzu
  #include <Stepper.h>            // Fügen Sie die Bibliothek für den Schrittmotor hinzu

  #define RST_PIN 9  // Reset-Pin für das RFID-Modul
  #define SS_PIN 10  // Slave-Select-Pin für das RFID-Modul

  // Erstellen Sie eine Instanz der MFRC522-Klasse, um mit dem RFID-Modul zu interagieren
  MFRC522 mfrc522(SS_PIN, RST_PIN);
  // Erstellen Sie eine Instanz der LiquidCrystal_I2C-Klasse für das LCD
  LiquidCrystal_I2C lcd(0x27, 16, 2);

  // Definieren Sie die Konfiguration des Schrittmotors
  const int stepsPerRevolution = 2048;              // Gesamtanzahl der Schritte pro Umdrehung
  Stepper stepper(stepsPerRevolution, 2, 3, 4, 5);  // Pins für den Schrittmotor (IN1, IN2, IN3, IN4)

  int doorStep = 512;  // Schritte, um die Tür um 90 Grad zu öffnen

  // UID für autorisierten Zugang
  const byte authorizedUID[4] = { 0x9B, 0x2F, 0x0A, 0x11 };

  void setup() {
    Serial.begin(9600);
    SPI.begin();
    mfrc522.PCD_Init();    // Initialisieren Sie den RFID-Leser
    stepper.setSpeed(15);  // Stellen Sie die Geschwindigkeit des Schrittmotors auf 15 U/min ein

    // Initialisieren Sie das LCD-Display
    lcd.init();
    lcd.backlight();
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Scan your card");
    Serial.println("Ready to read a card");
  }

  void loop() {
    // Überprüfen Sie, ob eine neue Karte vorhanden ist
    if (!mfrc522.PICC_IsNewCardPresent() || !mfrc522.PICC_ReadCardSerial()) {
      return;  // Schleife beenden, wenn keine neue Karte vorhanden ist
    }

    // Erstellen und zeigen Sie die UID der Karte an
    String uidStr = buildUIDString();
    Serial.print("Card ID: ");
    Serial.println(uidStr);

    // Überprüfen Sie die Kartenautorisierung und reagieren Sie entsprechend
    if (isAuthorized(mfrc522.uid.uidByte)) {
      grantAccess();
    } else {
      denyAccess();
    }

    delay(3000);  // Verzögerung vor dem nächsten Kartenlesevorgang
    lcd.clear();
    lcd.print("Scan your card");

    // Beenden Sie die Kartenkommunikation und stoppen Sie die Verschlüsselung
    mfrc522.PICC_HaltA();
    mfrc522.PCD_StopCrypto1();
  }

  String buildUIDString() {
    String uidStr = "";  // Speichern Sie die UID als Zeichenkette zur Anzeige
    for (byte i = 0; i < mfrc522.uid.size; i++) {
      char buff[3];
      sprintf(buff, "%02X", mfrc522.uid.uidByte[i]);
      uidStr += buff;
      if (i < mfrc522.uid.size - 1) uidStr += ":";
    }
    return uidStr;
  }

  void grantAccess() {
    lcd.clear();
    lcd.print("Welcome!");
    lcd.setCursor(0, 1);
    lcd.print("Door Opening...");
    stepper.step(doorStep);   // Tür öffnen
    savePower();              // Energiesparfunktion nach Motoraktivität
    delay(5000);              // Simuliert, dass die Tür eine Weile offen bleibt
    stepper.step(-doorStep);  // Tür schließen
    savePower();              // Energiesparfunktion nach Motoraktivität
  }


  void denyAccess() {
    lcd.clear();
    lcd.print("Access Denied");
    lcd.setCursor(0, 1);
    lcd.print("Invalid Card");
  }

  void savePower() {
    // Deaktiviert alle Schrittmotor-Pins, um Strom zu sparen
    digitalWrite(2, LOW);
    digitalWrite(3, LOW);
    digitalWrite(4, LOW);
    digitalWrite(5, LOW);
  }

  bool isAuthorized(byte *uid) {
    // Überprüft, ob die gescannte UID mit der autorisierten UID übereinstimmt
    for (byte i = 0; i < 4; i++) {
      if (uid[i] != authorizedUID[i]) {
        return false;  // Gibt false zurück, wenn ein Byte nicht übereinstimmt
      }
    }
    return true;  // Gibt true zurück, wenn alle Bytes übereinstimmen
  }

14. Jede Karten- oder Tag-ID ist einzigartig, und Sie könnten beim ersten Scannen Ihrer Karte auf Zugang verweigert-Nachrichten stoßen. In diesem Fall können Sie den seriellen Monitor öffnen, um die ID Ihrer Karte zu überprüfen. Ersetzen Sie dann Ihre ID im Array ``authorizedUID[]``.

Zum Beispiel, wenn ich ``Card ID: 23:E7:03:33`` lese, ersetze ich sie mit ``const byte authorizedUID[4] = { 0x23, 0xE7, 0x03, 0x33 };``

.. image:: img/34_step_print_id.png
  :width: 600
  :align: center

15. Laden Sie den Code erneut hoch, und wenn Sie Ihre Karte in die Nähe des Antennenbereichs des RFID-Moduls bringen, sehen Sie eine Begrüßungsnachricht, und der Schrittmotor dreht sich 512 Schritte (90 Grad), um das Öffnen der Tür zu simulieren. Nach 5 Sekunden kehrt er in seine ursprüngliche Position zurück, um die Tür zu schließen.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/31_access_control_system.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

16. Speichern Sie abschließend Ihren Code und räumen Sie Ihren Arbeitsplatz auf.

**Frage**

Nachdem nun ein grundlegendes Zugangskontrollsystem eingerichtet wurde, welche zusätzlichen Komponenten könnten hinzugefügt werden, um dessen Funktionalität und Flexibilität zu verbessern?


**Zusammenfassung**

In diesem Kurs haben wir uns intensiv mit den Funktionen von Schrittmotoren, RFID-Modulen und I2C-LCD-Displays auseinandergesetzt, was schließlich zur Entwicklung eines voll funktionsfähigen Zugangskontrollsystems führte. Sie haben gelernt, verschiedene Komponenten zu integrieren, um ein System zu entwickeln, das RFID-Tags liest, Türmechanismen über Schrittmotoren steuert und Systemstatus und Nachrichten auf einem LCD anzeigt.


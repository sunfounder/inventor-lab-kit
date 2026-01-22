.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein und tausche dich mit anderen Enthusiasten aus.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Sneak Peeks.
    - **Spezielle Rabatte**: Profitiere von exklusiven Rabatten auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und festlichen Aktionen teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

.. _ar_rfid_module:

33. Erkundung des RF522-RFID-Moduls
================================================
Die Zeiten des Wartens in langen Kassenschlangen im Supermarkt sind dank der RFID-Technologie vorbei! Stell dir ein RFID-basiertes automatisches Kassensystem vor, bei dem du einfach deinen Wagen füllst und zur Tür hinausgehst. Jedes Produkt, das mit einem RFID-Label versehen ist, wird sofort erkannt und erfasst. Kein lästiges Scannen jedes einzelnen Artikels mehr!

In dieser spannenden Lektion tauchen wir in die Welt der RFID-Technologie ein, indem wir das RC522 RFID-Lese-/Schreibmodul verwenden. Dieses Modul ist bei Hobbyisten sehr beliebt, da es einen geringen Stromverbrauch, Erschwinglichkeit, Langlebigkeit, einfache Schnittstellen und eine weit verbreitete Popularität bietet.

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/33_rfid_lcd.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

In dieser Lektion wirst du:

* Die Grundlagen der RFID-Technologie und ihre Anwendungen verstehen.
* Lernen, wie man das RC522 RFID-Lesemodul mit einem Arduino verbindet.
* Persönliche Daten mit dem RC522-Modul auf ein RFID-Tag schreiben.
* Die geschriebenen Daten vom RFID-Tag lesen und verifizieren.
* Die RFID-Tag-Informationen auf einem I2C LCD anzeigen.

Was ist das RC522-Modul und die RFID-Technologie?
------------------------------------------------------
**RC522-Modul**

Das RC522 RFID-Lesemodul, das bei einer Frequenz von 13,56 MHz arbeitet, ist für die Kommunikation mit RFID-Tags ausgelegt, die dem ISO 14443A-Standard entsprechen. Dieses kompakte und vielseitige Gerät eignet sich hervorragend für Anwendungen in der Zugangskontrolle, Bestandsverfolgung und kontaktlosen Bezahlsystemen, da es über eine 4-polige SPI-Verbindung mit Mikrocontrollern kommuniziert, Datenraten von bis zu 10 Mbit/s unterstützt und zusätzliche I2C- und UART-Kommunikationsprotokolle bietet.

Es arbeitet mit einer Spannung zwischen 2,5 und 3,3 V, und seine 5V-toleranten Logikpins erleichtern die Integration mit Arduino und anderen 5V-Logik-Mikrocontrollern, wodurch die Notwendigkeit eines Pegelwandlers entfällt.

.. image:: img/33_rfid_module.png
  :width: 400
  :align: center

* **VCC**: Versorgt das Modul mit Strom (2,5 bis 3,3 V). Verbinde es mit dem 3,3V-Ausgang des Arduino. Verbinde es nicht mit 5V, da dies das Modul beschädigen kann.
* **RST**: Setzt das Modul zurück und schaltet es aus. Es geht in den Energiesparmodus, wenn es auf LOW gesetzt wird, und wird beim ansteigenden Signal wieder aktiviert.
* **GND**: Erdungspin, verbinde ihn mit GND des Arduino.
* **IRQ**: Interrupt-Pin, benachrichtigt den Mikrocontroller, wenn ein RFID-Tag in der Nähe ist.
* **MISO / SCL / Tx**: Dient als Master-In-Slave-Out für SPI, als serieller Taktgeber für I2C und als serielle Datenausgabe für UART.
* **MOSI**: SPI-Eingang zum Modul.
* **SCK**: Serieller Takteingang vom SPI-Bus-Master (Arduino).
* **SS / SDA / Rx**: Signal-Eingang für SPI, serielle Daten für I2C und serielle Dateneingabe für UART. Oft mit einem Quadrat markiert.


**RFID-Technologie**

Ein RFID-System, oder auch Radiofrequenz-Identifikationssystem, besteht aus zwei Hauptkomponenten: einem Tag, das an dem zu identifizierenden Objekt befestigt ist, und einem Leser, der dieses Tag ausliest.

Der Leser enthält ein HF-Modul und eine Antenne, die ein hochfrequentes elektromagnetisches Feld erzeugt. Tags sind typischerweise passiv, was bedeutet, dass sie keine Batterie haben. Sie bestehen aus einem Mikrochip zur Speicherung und Verarbeitung von Informationen sowie einer Antenne zum Empfangen und Senden von Signalen.

.. image:: img/33_rfid_com.png
  :width: 800
  :align: center

Wenn sich das Tag in der Nähe des Lesers befindet, versorgt das elektromagnetische Feld des Lesers den Chip des Tags, indem es einen Elektronenfluss durch seine Antenne induziert.

Der Chip sendet dann seine gespeicherten Daten über ein Funksignal zurück an den Leser, ein Prozess, der als Rückstreuung bekannt ist. Der Leser erfasst und dekodiert dieses Signal und sendet die Informationen zur weiteren Verarbeitung an einen Computer oder Mikrocontroller.

Baue die Schaltung auf
------------------------------------
Jetzt, da wir alles über das Modul wissen, lass uns damit beginnen, es mit unserem Arduino zu verbinden!

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RFID-Modul und Tag
     - 1 * I2C LCD1602
   * - |list_uno_r3|
     - |list_rc522_module| 
     - |list_i2c_lcd1602|
   * - Jumper-Kabel
     - 1 * Steckbrett
     - 1 * USB-Kabel
   * - |list_wire|
     - |list_breadboard|
     - |list_usb_cable|

**Bauanleitung**

Folge dem Schaltplan oder den folgenden Schritten, um deine Schaltung aufzubauen.

.. image:: img/33_rfid_connect_lcd.png
    :width: 700
    :align: center


1. Stecke zunächst das RC522-RFID-Modul in das Steckbrett.

.. image:: img/33_rfid_plug_rc522.png
    :width: 400
    :align: center


2. Verbinde dann das RC522-RFID-Modul mit dem Arduino Uno R3.

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
        - GND
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
  
.. image:: img/33_rfid_connect_rc522.png
    :width: 500
    :align: center

3. Abschließend verbinde das I2C LCD1602-Modul: GND mit GND am Arduino Uno R3, VCC mit dem 5V-Pin, SDA mit Pin A4 und SCL mit Pin A5.

.. image:: img/33_rfid_connect_lcd.png
    :width: 700
    :align: center
  

Code-Erstellung - Schreiben und Lesen
------------------------------------------
In diesem Abschnitt installieren wir die für die Verwendung des MFRC522 RFID-Moduls erforderlichen Bibliotheken und öffnen dann Beispielcode, um Informationen auf ein Tag zu schreiben und diese wieder auszulesen.

**Informationen schreiben**

1. Um das MFRC522 RFID-Modul zu verwenden, musst du die entsprechende Bibliothek einbinden. Suche nun im **Library Manager** nach ``MFRC522`` und klicke dann auf **INSTALL**.

.. image:: img/33_rfid_install_lib.png
  :align: center

2. Klicke nun auf **Datei** -> **Beispiele** -> **MFRC522**. Dort findest du mehrere Beispielcodes, die verschiedene Funktionen demonstrieren. Öffne den Beispielcode ``rfid_write_personal_data``.

.. image:: img/33_rfid_open_write.png
  :align: center

3. Klicke auf **Hochladen**, um den Code auf dein Arduino-Board hochzuladen. Öffne dann den seriellen Monitor, und du wirst eine Eingabeaufforderung sehen.

.. image:: img/33_rfid_write_open.png
  :align: center

4. Lege nun die mitgelieferte weiße Karte oder das Tag in die Nähe des MFRC522-Moduls. Du wirst die UID des Tags, den PICC-Typ und eine Aufforderung sehen, den Nachnamen einzugeben, gefolgt von einem #.

.. code-block::

  Persönliche Daten auf eine MIFARE PICC schreiben
  Karten-UID: 9B 2F 0A 11 PICC type: MIFARE 1KB
  Gib den Nachnamen ein, gefolgt von #

5. Gib nun deinen Nachnamen ein, zum Beispiel ``XIE#``. Drücke ``Enter``, um deine Eingabe an das Arduino-Board zu senden, das die Daten dann an das RFID-Modul überträgt.

.. note::

  Achte beim Eingeben der Daten darauf, dass deine Karte oder dein Tag weiterhin in der Nähe der Antenne des RFID-Moduls bleibt, da sonst ein Fehler auftritt.

.. image:: img/33_rfid_write_first_name.png
  :align: center

6. Du wirst eine Erfolgsmeldung für das Schreiben der Daten sehen, gefolgt von einer Aufforderung, den Vornamen einzugeben.

.. code-block::

  Write personal data on a MIFARE PICC 
  Card UID: 9B 2F 0A 11 PICC type: MIFARE 1KB
  Type Family name, ending with #
  PCD_Authenticate() success: 
  MIFARE_Write() success: 
  MIFARE_Write() success: 
  Type First name, ending with #

7. Gib als nächstes den Vornamen ein, zum Beispiel ``Daisy#``. Du wirst eine weitere Erfolgsmeldung für das Schreiben der Daten sehen.

.. code-block::

  Write personal data on a MIFARE PICC 
  Card UID: 9B 2F 0A 11 PICC type: MIFARE 1KB
  Type Family name, ending with #
  PCD_Authenticate() success: 
  MIFARE_Write() success: 
  MIFARE_Write() success: 
  Type First name, ending with #
  MIFARE_Write() success: 
  MIFARE_Write() success: 

**Informationen auslesen**

Wir haben gerade unseren Namen auf die Karte oder das Tag geschrieben. Nun öffnen wir einen weiteren Beispielcode, um die Informationen von dieser Karte auszulesen und zu überprüfen, ob die Daten korrekt geschrieben wurden.

1. Klicke erneut auf **Datei** -> **Beispiele** -> **MFRC522** und öffne den Beispielcode ``rfid_read_personal_data``.

.. image:: img/33_rfid_read_open.png
  :align: center

2. Lade den Code nach dem Öffnen auf dein Arduino-Board hoch. Lege dann deine Karte in die Nähe der Antenne des RFID-Moduls. Du wirst deine UID und die zuvor geschriebenen Namensinformationen sehen.

.. code-block::

  **Karte erkannt:**
  Karten-UID: 9B 2F 0A 11
  Karten-SAK: 08
  PICC-Typ: MIFARE 1KB
  Name: 
  Daisy XIE             
  **Ende des Lesens**

Code-Erstellung - Anzeige auf LCD
---------------------------------------

Hier lernen wir, wie man den Namen und die UID der Karte auf einem I2C LCD anzeigt.

.. note::

  Falls du mit dem I2C LCD1602 nicht vertraut bist, kannst du zunächst dessen Grundfunktionen durch die folgenden Projekte erlernen:

  * :ref:`ar_i2c_lcd1602`

  Die Bibliothek ``LiquidCrystal I2C`` wird hier verwendet und kann über den **Library Manager** installiert werden.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „Neue Skizze“ im Menü „Datei“ auswählst.
2. Speichere deine Skizze als ``Lesson33_RFID_LCD`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Bibliotheken für die SPI- und I2C-Kommunikation werden eingebunden, um mit den RFID- und LCD-Modulen zu interagieren. Die Reset-Pins (``RST_PIN``) und der Slave-Select-Pin (``SS_PIN``) für den RFID-Leser werden definiert.

.. code-block:: Arduino

  #include <SPI.h>                // Einbindung der SPI-Bibliothek für die SPI-Kommunikation
  #include <MFRC522.h>            // Einbindung der Bibliothek für das RFID-Modul
  #include <Wire.h>               // Einbindung der Wire-Bibliothek für die I2C-Kommunikation
  #include <LiquidCrystal_I2C.h>  // Einbindung der Bibliothek für das I2C-LCD

  #define RST_PIN 9  // Reset-Pin für das RFID-Modul
  #define SS_PIN 10  // Slave-Select-Pin für das RFID-Modul

4. Die Initialisierung des RFID-Lesers und des LCD-Displays erfolgt mit den angegebenen Pin-Verbindungen und den LCD-Abmessungen/Konfigurationen (Adresse 0x27, 16 Spalten, 2 Zeilen).

.. code-block:: Arduino

  // Erstellen einer Instanz der MFRC522-Klasse zur Schnittstelle mit dem RFID-Modul
  MFRC522 mfrc522(SS_PIN, RST_PIN);
  // Erstellen einer Instanz der LiquidCrystal_I2C-Klasse für das LCD
  LiquidCrystal_I2C lcd(0x27, 16, 2);

5. Die ``setup()``-Funktion initialisiert die serielle Kommunikation, den SPI-Bus, den RFID-Leser und das LCD. Sie schaltet die LCD-Hintergrundbeleuchtung ein und sendet eine Bereitschaftsmeldung an den seriellen Monitor.

.. code-block:: Arduino

  void setup() {
    Serial.begin(9600);                         // Starte die serielle Kommunikation mit 9600bps
    SPI.begin();                                // Initialisiere den SPI-Bus
    mfrc522.PCD_Init();                         // Initialisiere den RFID-Leser
    lcd.init();                                 // Initialisiere das LCD-Display
    lcd.backlight();                            // Schalte die Hintergrundbeleuchtung des LCD ein
    Serial.println(F("Ready to read a card"));  // Drucke eine Nachricht zum Start des Lesens
  }

6. Die ``loop()``-Funktion prüft kontinuierlich, ob neue RFID-Karten vorhanden sind. Wenn eine Karte erkannt wird, liest und zeigt sie die UID an, liest Daten aus Block 4 und pausiert dann einen Moment, bevor das LCD gelöscht wird.

.. code-block:: Arduino

  void loop() {
    // Prüfe, ob eine neue RFID-Karte vorhanden ist und gelesen werden kann
    if (!mfrc522.PICC_IsNewCardPresent() || !mfrc522.PICC_ReadCardSerial()) {
      return;  // Wenn keine neue Karte vorhanden ist, verlasse die Schleife
    }

    displayCardUID();           // Funktion zur Anzeige der UID der Karte
    readAndDisplayBlock(4);     // Funktion zum Lesen und Anzeigen von Block 4 der RFID-Karte
    mfrc522.PICC_HaltA();       // Halte die RFID-Karte an, um das Lesen zu stoppen
    mfrc522.PCD_StopCrypto1();  // Stoppe die Verschlüsselung der Kommunikation
    delay(5000);                // Warte 5 Sekunden
    lcd.clear();                // Lösche das LCD-Display
  }


7. Die Funktion ``displayCardUID()``: Handhabt die Anzeige der UID der Karte sowohl auf dem seriellen Monitor als auch auf dem LCD. Sie formatiert die UID als hexadezimale Werte.

.. code-block:: Arduino

  // Function to display the UID of the RFID card
  void displayCardUID() {
    Serial.print(F("Card UID:"));                  // Print the text "Card UID:"
    lcd.clear();                                   // Clear the LCD display
    lcd.setCursor(0, 0);                           // Set the LCD cursor to the top-left
    lcd.print("UID:");                             // Print "UID:" on the LCD
    for (byte i = 0; i < mfrc522.uid.size; i++) {  // Loop through each byte of the UID
      Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
      Serial.print(mfrc522.uid.uidByte[i], HEX);  // Print UID byte in hexadecimal
      lcd.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
      lcd.print(mfrc522.uid.uidByte[i], HEX);  // Print UID byte on the LCD in hexadecimal
    }
    Serial.println();  // Print a newline on the serial monitor
  }

8. Die Funktion ``authenticateBlock``: Handhabt das Lesen eines spezifischen Blocks von der RFID-Karte, authentifiziert den Zugriff auf den Block und zeigt die abgerufenen Daten auf dem LCD an.

.. code-block:: Arduino

  // Function to authenticate and read a block from the RFID card
  bool authenticateBlock(byte block, byte *buffer, byte &size) {
    MFRC522::StatusCode status;  // Variable to hold the status of RFID operations
    MFRC522::MIFARE_Key key;     // Variable to hold the authentication key
    // Set the key to the default key known as FFFFFFFFFFFFh
    for (byte i = 0; i < 6; i++) key.keyByte[i] = 0xFF;  // Default key A for authentication

    // Authenticate the desired block with the key
    status = mfrc522.PCD_Authenticate(MFRC522::PICC_CMD_MF_AUTH_KEY_A, block, &key, &(mfrc522.uid));
    if (status != MFRC522::STATUS_OK) {
      Serial.print(F("Authentication failed: "));
      Serial.println(mfrc522.GetStatusCodeName(status));
      return false;  // If authentication failed, return false
    }

    // Read the block after successful authentication
    status = mfrc522.MIFARE_Read(block, buffer, &size);
    if (status != MFRC522::STATUS_OK) {
      Serial.print(F("Reading failed: "));
      Serial.println(mfrc522.GetStatusCodeName(status));
      return false;  // If reading failed, return false
    }
    buffer[size - 1] = '\0';  // Ensure the string is null-terminated
    return true;              // Return true if reading is successful
  }

9. Funktion ``readAndDisplayBlock``: Diese Funktion versucht, einen bestimmten Block auf der RFID-Karte mit einem vordefinierten Schlüssel zu authentifizieren. Bei erfolgreicher Authentifizierung werden die Daten ausgelesen.

.. code-block:: Arduino

  // Function to read a block and display its contents
  void readAndDisplayBlock(byte block) {
    byte buffer[18];                               // Buffer to store the data read from the RFID card
    byte size = sizeof(buffer);                    // Variable to store the size of the data read
    if (authenticateBlock(block, buffer, size)) {  // If authentication and reading are successful
      lcd.setCursor(0, 1);                         // Set the cursor to the second line of the LCD
      lcd.print("Name: ");                         // Print "Name:"
      // Print the name starting from the second character to skip the size byte
      lcd.print((char *)buffer + 1);
      Serial.print("Name: ");
      Serial.println((char *)buffer + 1);  // Print the name on the serial monitor
    }
  }

10. Der Code sieht folgendermaßen aus. Du kannst ihn auf das Arduino Uno R3 hochladen. Anschließend bringst du deine Karte oder dein Tag in die Nähe der Antenne des RFID-Moduls, und du wirst den Namen und die ID sowohl auf dem LCD als auch auf dem seriellen Monitor sehen.

.. code-block:: Arduino

  #include <SPI.h>                // Include the SPI library for SPI communication
  #include <MFRC522.h>            // Include the library for the RFID module
  #include <Wire.h>               // Include the Wire library for I2C communication
  #include <LiquidCrystal_I2C.h>  // Include the library for the I2C LCD

  #define RST_PIN 9  // Reset pin for the RFID module
  #define SS_PIN 10  // Slave select pin for the RFID module

  // Create an instance of the MFRC522 class to interface with the RFID module
  MFRC522 mfrc522(SS_PIN, RST_PIN);
  // Create an instance of the LiquidCrystal_I2C class for the LCD
  LiquidCrystal_I2C lcd(0x27, 16, 2);

  void setup() {
    Serial.begin(9600);                         // Start serial communication at 9600bps
    SPI.begin();                                // Initialize the SPI bus
    mfrc522.PCD_Init();                         // Initialize the RFID reader
    lcd.init();                                 // Initialize the LCD display
    lcd.backlight();                            // Turn on the backlight of the LCD
    Serial.println(F("Ready to read a card"));  // Print a message to start read
  }

  void loop() {
    // Check if a new RFID card is present and can be read
    if (!mfrc522.PICC_IsNewCardPresent() || !mfrc522.PICC_ReadCardSerial()) {
      return;  // If no new card is present, exit the loop
    }

    displayCardUID();           // Function to display the UID of the card
    readAndDisplayBlock(4);     // Function to read and display block4 of the RFID card
    mfrc522.PICC_HaltA();       // Halt the RFID card to stop reading
    mfrc522.PCD_StopCrypto1();  // Stop encryption on the communication
    delay(5000);                // Delay for 5 seconds
    lcd.clear();                // Clear the LCD display
  }

  // Function to display the UID of the RFID card
  void displayCardUID() {
    Serial.print(F("Card UID:"));                  // Print the text "Card UID:"
    lcd.clear();                                   // Clear the LCD display
    lcd.setCursor(0, 0);                           // Set the LCD cursor to the top-left
    lcd.print("UID:");                             // Print "UID:" on the LCD
    for (byte i = 0; i < mfrc522.uid.size; i++) {  // Loop through each byte of the UID
      Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
      Serial.print(mfrc522.uid.uidByte[i], HEX);  // Print UID byte in hexadecimal
      lcd.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
      lcd.print(mfrc522.uid.uidByte[i], HEX);  // Print UID byte on the LCD in hexadecimal
    }
    Serial.println();  // Print a newline on the serial monitor
  }

  // Function to authenticate and read a block from the RFID card
  bool authenticateBlock(byte block, byte *buffer, byte &size) {
    MFRC522::StatusCode status;  // Variable to hold the status of RFID operations
    MFRC522::MIFARE_Key key;     // Variable to hold the authentication key
    // Set the key to the default key known as FFFFFFFFFFFFh
    for (byte i = 0; i < 6; i++) key.keyByte[i] = 0xFF;  // Default key A for authentication

    // Authenticate the desired block with the key
    status = mfrc522.PCD_Authenticate(MFRC522::PICC_CMD_MF_AUTH_KEY_A, block, &key, &(mfrc522.uid));
    if (status != MFRC522::STATUS_OK) {
      Serial.print(F("Authentication failed: "));
      Serial.println(mfrc522.GetStatusCodeName(status));
      return false;  // If authentication failed, return false
    }

    // Read the block after successful authentication
    status = mfrc522.MIFARE_Read(block, buffer, &size);
    if (status != MFRC522::STATUS_OK) {
      Serial.print(F("Reading failed: "));
      Serial.println(mfrc522.GetStatusCodeName(status));
      return false;  // If reading failed, return false
    }
    buffer[size - 1] = '\0';  // Ensure the string is null-terminated
    return true;              // Return true if reading is successful
  }

  // Function to read a block and display its contents
  void readAndDisplayBlock(byte block) {
    byte buffer[18];                               // Buffer to store the data read from the RFID card
    byte size = sizeof(buffer);                    // Variable to store the size of the data read
    if (authenticateBlock(block, buffer, size)) {  // If authentication and reading are successful
      lcd.setCursor(0, 1);                         // Set the cursor to the second line of the LCD
      lcd.print("Name: ");                         // Print "Name:"
      // Print the name starting from the second character to skip the size byte
      lcd.print((char *)buffer + 1);
      Serial.print("Name: ");
      Serial.println((char *)buffer + 1);  // Drucke den Namen auf dem seriellen Monitor
    }
  }

**Frage**

Nachdem du nun verstanden hast, wie man das RC522-RFID-Modul zum Lesen oder Schreiben von Karten- oder Tag-Informationen und zur Anzeige auf einem LCD verwendet, wie würdest du ein gängiges Zugangskontrollsystem für den täglichen Gebrauch entwerfen? Beschreibe deinen Designansatz.


**Zusammenfassung**

In dieser Lektion haben wir gelernt, wie man die RFID-Technologie mithilfe des RC522-Moduls nutzt. Wir haben die grundlegenden Konzepte erkundet, die erforderlichen Schaltungen aufgebaut, persönliche Daten auf RFID-Tags geschrieben und gelesen und die Informationen auf einem LCD angezeigt. Am Ende dieser Lektion solltest du gut gerüstet sein, um RFID-Technologie in deine eigenen Projekte zu integrieren und deine Systeme effizienter und benutzerfreundlicher zu gestalten.

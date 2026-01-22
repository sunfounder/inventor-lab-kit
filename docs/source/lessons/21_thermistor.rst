.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche gemeinsam mit anderen Begeisterten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum mitmachen?**

    - **Expertenunterstützung**: Löse nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitig Zugang zu neuen Produktankündigungen und Sneak Peeks.
    - **Exklusive Rabatte**: Profitiere von exklusiven Rabatten auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und Sonderaktionen während der Feiertage teil.

    👉 Bereit, mit uns zu erkunden und zu gestalten? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

.. _ar_temperature:

21. Temperaturalarm
========================

In dieser Lektion erkunden wir die entscheidende Rolle des Temperaturmanagements für die Lebensmittelsicherheit. Nicht alle Lebensmittel müssen gekühlt oder gefroren werden; auch haltbare Produkte wie Chips, Brot und bestimmte Früchte benötigen die richtige Lagerungstemperatur, um Qualität und Sicherheit zu gewährleisten. Indem wir ein Temperaturüberwachungssystem bauen, lernen wir, wie man Lebensmittel innerhalb sicherer Temperaturbereiche hält und einen Alarm auslöst, wenn diese Grenzen überschritten werden. Dieses praxisorientierte Projekt schützt nicht nur Lebensmittel, sondern dient auch als hervorragende Einführung in die Umweltüberwachung mit realen Anwendungen.

.. .. image:: img/16_temperature.jpg
..     :width: 400
..     :align: center

.. raw:: html

    <video muted controls style = "max-width:90%">
        <source src="_static/video/21_temp_alarm.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Am Ende dieser Lektion wirst du in der Lage sein:

* Die Bedeutung der Temperaturkontrolle für die Lebensmittelsicherheit zu verstehen.
* Einen Schaltkreis mit einem Thermistor zu bauen, um Temperaturänderungen zu überwachen.
* Ein Arduino-Programm zu schreiben, das Temperaturdaten von einem Thermistor liest.
* Logik in der Programmierung anzuwenden, um Aktionen (wie das Einschalten einer LED oder das Auslösen eines Alarms) basierend auf Temperaturdaten auszulösen.
* Konzepte des elektrischen Widerstands und der Temperaturumrechnung in praktischen Szenarien anzuwenden.


Den Schaltkreis aufbauen
---------------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * RGB-LED
     - 3 * 220Ω Widerstand
     - 1 * 10KΩ Widerstand
   * - |list_uno_r3| 
     - |list_rgb_led| 
     - |list_220ohm| 
     - |list_10kohm| 
   * - 1 * Thermistor
     - 1 * Steckbrett
     - Verbindungskabel
     - 1 * USB-Kabel
   * - |list_thermistor| 
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

**Schritt-für-Schritt-Anleitung**

Dieser Schaltkreis baut auf dem aus Lektion 12 auf und fügt einen Thermistor hinzu.

.. image:: img/16_temperature_alarm.png
    :width: 500
    :align: center

1. Entferne das Verbindungskabel, das den GND-Pin des Arduino Uno R3 mit dem GND-Pin der RGB-LED verbindet, und stecke es in den Minuspol des Steckbretts. Verbinde dann ein weiteres Kabel vom Minuspol des Steckbretts mit dem GND-Pin der RGB-LED.

.. image:: img/16_temperature_alarm_gnd.png
    :width: 500
    :align: center

2. Stecke den Thermistor in die Löcher 6E und 8E. Die Pins sind richtungslos und können beliebig eingesetzt werden.

.. image:: img/16_temperature_alarm_thermistor.png
    :width: 500
    :align: center

Ein Thermistor ist ein spezieller Widerstand, dessen Widerstand sich mit der Temperatur ändert. Dieses Bauteil ist sehr nützlich, da es uns hilft, die Temperatur zu erfassen und zu messen, und damit die Kontrolle in verschiedenen elektronischen Projekten und Geräten ermöglicht.

Hier ist das elektronische Symbol des Thermistors.

.. image:: img/16_thermistor_symbol.png
    :width: 300
    :align: center

Thermistoren gibt es in zwei grundlegenden Typen:

* **NTC-Thermistoren**: Der Widerstand sinkt mit steigender Temperatur. Sie werden häufig als Temperatursensoren oder Einschaltstrombegrenzer in Schaltkreisen verwendet.
* **PTC-Thermistoren**: Der Widerstand steigt mit steigender Temperatur. Sie werden oft als selbstrückstellende Sicherungen in Schaltkreisen eingesetzt, um vor Überstrom zu schützen.

In diesem Kit verwenden wir einen **NTC**-Thermistor.

Nun benutze ein Multimeter, um den Widerstand dieses Thermistors zu messen und zu überprüfen, ob er bei steigender Temperatur tatsächlich abnimmt.

3. Da der Nennwiderstand des Thermistors 10K beträgt, stelle das Multimeter auf den Bereich 20 Kilo-Ohm (20K) ein, um den Widerstand zu messen.

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

4. Berühre nun die beiden Pins des Fotowiderstands mit den roten und schwarzen Prüfspitzen des Multimeters.

.. image:: img/16_temperature_alarm_test.png
    :width: 500
    :align: center

5. Lies den Widerstandswert bei der aktuellen Temperatur ab und trage ihn in die folgende Tabelle ein.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Umgebung
     - Widerstand (Kilo-Ohm)
   * - Aktuelle Temperatur
     - *9,37*
   * - Höhere Temperatur
     -
   * - Niedrigere Temperatur
     -

6. Jetzt kannst du einen Freund bitten, den Thermistor zu halten, oder etwas anderes verwenden, um die Temperatur um den Thermistor herum zu erhöhen (kein Wasser, kein Feuer, Sicherheit geht vor). Notiere den Widerstandswert des Thermistors zu diesem Zeitpunkt in der Tabelle.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Umgebung
     - Widerstand (Kilo-Ohm)
   * - Aktuelle Temperatur
     - *9,37*
   * - Höhere Temperatur
     - *6,10*
   * - Niedrigere Temperatur
     -

7. Du kannst den Thermistor ins Freie legen oder ihn mit einem Ventilator kühlen, um die Temperatur um ihn herum zu senken. Notiere den gemessenen Widerstand zu diesem Zeitpunkt in der Tabelle.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Umgebung
     - Widerstand (Kilo-Ohm)
   * - Aktuelle Temperatur
     - *9,37*
   * - Höhere Temperatur
     - *6,10*
   * - Niedrigere Temperatur
     - *12,49*

Durch diese Messungen können wir erkennen, dass bei höherer Umgebungstemperatur der Widerstand sinkt.

8. Jetzt kannst du den Schaltkreis weiter aufbauen. Verbinde ein Ende des Thermistors mit einem 10K-Widerstand und das andere Ende des 10K-Widerstands mit der negativen Schiene des Steckbretts.

.. image:: img/16_temperature_alarm_resistor.png
    :width: 500
    :align: center

9. Verbinde das andere Ende des Steckbretts mit dem 5V-Pin des Arduino Uno R3.

.. image:: img/16_temperature_alarm_5v.png
    :width: 500
    :align: center

10. Abschließend verbinde den gemeinsamen Pin des Fotowiderstands und des 10K-Widerstands mit dem A0-Pin des Arduino Uno R3.

.. image:: img/16_temperature_alarm.png
    :width: 500
    :align: center

Verständnis der Temperaturberechnung
----------------------------------------
**Über die Temperaturformel**

Der Widerstand eines NTC-Thermistors ändert sich mit der Temperatur. Diese Beziehung wird oft genau durch die Steinhart-Hart-Gleichung beschrieben, wie folgt:

.. image:: img/16_format_steinhart.png
    :width: 400
    :align: center

Hierbei werden a, b und c als Steinhart-Hart-Parameter bezeichnet, die für jedes Bauteil spezifisch sind. T ist die absolute Temperatur, und R ist der Widerstand.

Zusätzlich zur Steinhart-Hart-Gleichung wird in vielen praktischen Anwendungen auch eine vereinfachte Formel auf Basis des Beta-Parameters (Beta-Parameter-Modell) verwendet, um die Temperatur schnell zu berechnen. Dieses Modell geht davon aus, dass die Beziehung zwischen Widerstand und Temperatur durch eine einfachere exponentielle Beziehung angenähert werden kann, was den Berechnungsprozess vereinfacht und es für eine schnelle Temperaturüberwachung in technischen Anwendungen geeignet macht.

.. image:: img/16_format_3.png
    :width: 400
    :align: center

* **T** ist die Temperatur des Thermistors in Kelvin.
* **T0** ist eine Referenztemperatur, normalerweise bei 25°C (was in Kelvin 273,15 + 25 ergibt).
* **B** ist der Beta-Parameter des Materials, der Beta-Koeffizient des in diesem Kit verwendeten NTC-Thermistors beträgt 3950.
* **R** ist der gemessene Widerstand.
* **R0** ist der Widerstand bei der Referenztemperatur T0, der Widerstand des in diesem Kit verwendeten NTC-Thermistors beträgt bei 25°C 10 Kilo-Ohm.

Nach Umformung der obigen Formeln wird die Kelvin-Temperatur wie folgt berechnet: ``T=1/(ln(R/R0)/B+1/T0)``, ziehe 273,15 ab, um die Temperatur in Celsius umzurechnen.

**Wie misst man den Widerstand?**

Wir verbinden den Thermistor und einen 10K-Widerstand in Reihe in unserem Schaltkreis.

.. image:: img/16_thermistor_sch.png
    :width: 200
    :align: center

Die Spannung am Pin A0, die wir messen, geteilt durch den Reihenwiderstand (den 10K-Widerstand), gibt uns den Stromfluss durch den Schaltkreis an. Dieser Strom kann auch durch die Teilung der Gesamtspannung durch den Gesamtwiderstand des Schaltkreises (Reihenwiderstand + Thermistor) ermittelt werden:

.. image:: img/16_format_1.png
    :width: 400
    :align: center

* **Vsupply**: Die an den Schaltkreis angelegte Spannung.
* **Rseries**: Der Widerstandswert des Reihenwiderstands.
* **Vmeasured**: Die Spannung über dem 10K-Widerstand, ebenfalls die Spannung am Pin A0.

Daraus können wir die Formel umstellen, um den Widerstand des Thermistors zu berechnen:

.. image:: img/16_format_2.png
    :width: 400
    :align: center

In unserem Code verwenden wir die Funktion ``analogRead()``, um die Spannung am Pin A0 zu messen. Die Beziehung zwischen der Spannung **Vmeasured** und dem gelesenen Analogwert ist:

.. code-block::

    (Analog value at A0) / 1023.0 = Vmeasured / Vsupply

Unter Verwendung der obigen Formel berechnen wir den Widerstand des Thermistors:

.. code-block::

    R_thermistor =R_series x (1023.0 / (Analog value at A0) - 1)

.. note::

    Wenn die Formeln kompliziert erscheinen, merke dir einfach die Endformeln hier, und du bist auf der sicheren Seite!

    Der Widerstand des Thermistors kann mit der folgenden Formel ermittelt werden:

    .. code-block::

        R_thermistor =R_series x (1023.0 / (Analogwert an A0) - 1)

    Anschließend wird die Kelvin-Temperatur mit der folgenden Formel berechnet:

    .. code-block::

        T=1/(ln(R/R0)/B+1/T0)

    * **T0**: 273,15 + 25.
    * **B**: 3950.
    * **R** ist der gemessene Widerstand.
    * **R0**: 10 Kilo-Ohm.

    Schließlich erfolgt die Umrechnung in Celsius mit der folgenden Formel:

    .. code-block::

        Tc = T - 273,15

Code-Erstellung
--------------------

**Temperatur messen**

1. Öffne die Arduino-IDE und starte ein neues Projekt, indem du im Menü „Datei“ „Neuer Sketch“ auswählst.
2. Speichere deinen Sketch als ``Lesson21_Temperature_Alarm`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. In den vorherigen Lektionen haben wir die Pins der RGB-LED direkt im Code verwendet; hier definieren wir sie als Konstanten.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    // Pin-Konfigurationen
    const int tempSensorPin = A0;  // Analogeingang für den NTC-Thermistor
    const int redPin = 11;         // Digitaler Pin für die rote LED
    const int greenPin = 10;       // Digitaler Pin für die grüne LED
    const int bluePin = 9;         // Digitaler Pin für die blaue LED

    void setup() {
        // Setup-Code hier einfügen, der einmal ausgeführt wird:
    }

Die Verwendung von Konstanten anstelle von Variablen, die im gesamten Programm unverändert bleiben, sorgt für Klarheit und erleichtert die Wartung. Dies ermöglicht aussagekräftige Namen anstelle von Zahlen und erfordert Änderungen nur in der Deklaration, nicht überall im Code. Konstanten folgen den gleichen Namensregeln wie Variablen und vermeiden reservierte Schlüsselwörter oder Befehle der Arduino-IDE.

4. Bevor wir den Thermistor verwenden, müssen wir weitere Konstanten definieren, um die Schaltungsparameter zu speichern.

.. note::

    Du wirst sehen, dass es sowohl Konstanten des Typs ``int`` als auch ``float`` gibt. Was ist der Unterschied zwischen diesen beiden Typen?

  * ``const int``: Eine Ganzzahl-Konstante speichert ganze Zahlen. Dieser Typ unterstützt keine Bruchteile oder Dezimalstellen und belegt typischerweise 16 oder 32 Bit Speicher.
  * ``const float``: Eine Gleitkomma-Konstante speichert Zahlen, die Bruchteile haben können. Dieser Typ wird verwendet, wenn mehr Präzision erforderlich ist, z.B. bei Messungen oder Berechnungen, die Dezimalwerte erfordern. Eine Gleitkomma-Konstante belegt typischerweise 32 Bit Speicher und kann eine größere Bandbreite von Zahlen darstellen als ``int``.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    // Pin-Konfigurationen
    const int tempSensorPin = A0;  // Analogeingang für den NTC-Thermistor
    const int redPin = 10;         // Digitaler Pin für die rote LED
    const int greenPin = 11;       // Digitaler Pin für die grüne LED
    const int bluePin = 12;        // Digitaler Pin für die blaue LED

    // Konstanten für die Temperaturberechnung
    const float beta = 3950.0;               // Beta-Wert des NTC-Thermistors
    const float seriesResistor = 10000;      // Wert des Reihenwiderstands (Ohm)
    const float roomTempResistance = 10000;  // Widerstand des NTC bei 25°C
    const float roomTemp = 25 + 273.15;      // Raumtemperatur in Kelvin

5. Im ``void setup()``-Block setzen wir die RGB-LED-Pins als Ausgänge und konfigurieren die serielle Kommunikation mit einer Baudrate von 9600.

.. code-block:: Arduino
    :emphasize-lines: 2-5

    void setup() {
        // Initialisiere die LED-Pins als Ausgänge
        pinMode(redPin, OUTPUT);
        pinMode(greenPin, OUTPUT);
        pinMode(bluePin, OUTPUT);
        
        // Starte die serielle Kommunikation mit 9600 Baud
        Serial.begin(9600);
    }

6. Zuerst musst du im ``void loop()``-Block den analogen Wert des Pins A0 auslesen.

.. code-block:: Arduino
    :emphasize-lines: 2

    void loop() {
        int adcValue = analogRead(tempSensorPin);  // Lese den Thermistorwert
    }

7. Berechne als Nächstes den Widerstand des Thermistors mithilfe der zuvor hergeleiteten Formel zur Umrechnung von Analogwerten in Spannung.

.. code-block:: Arduino
    :emphasize-lines: 3

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Lese den Thermistorwert
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Berechne den Widerstand des Thermistors
    }

8. Dann berechne die Temperatur in Kelvin mithilfe der unten gezeigten Formel:

.. code-block:: Arduino
    :emphasize-lines: 6

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Lese den Thermistorwert
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Berechne den Widerstand des Thermistors

        // Berechne die Temperatur in Kelvin unter Verwendung der Beta-Gleichung
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    }

9. Ziehe 273,15 von der Kelvin-Temperatur ab, um sie in Celsius umzurechnen, und drucke das Ergebnis dann mit der ``Serial.println()``-Funktion auf den seriellen Monitor.

.. code-block:: Arduino
    :emphasize-lines: 8,9

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Lese den Thermistorwert
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Berechne den Widerstand des Thermistors

        // Berechne die Temperatur in Kelvin unter Verwendung der Beta-Gleichung
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    
        float tempC = tempK - 273.15;  // In Celsius umrechnen
        Serial.println(tempC);         // Zeige die Temperatur in Celsius auf dem seriellen Monitor an
    }

10. An diesem Punkt kannst du den Code auf dein Arduino Uno R3 hochladen und die aktuellen Celsius-Temperaturwerte abrufen.

.. code-block::

    26.28
    26.19
    26.19
    26.28
    26.28

**RGB-LED-Farbe ändern**

Nun ändern wir die Farbe der RGB-LED basierend auf der vom Thermistor gemessenen Temperatur.

Zum Beispiel legen wir drei Temperaturbereiche fest:

* Unter 10 Grad zeigt die RGB-LED grün und signalisiert, dass die Temperatur angenehm ist.
* Zwischen 10 und 20 Grad zeigt die RGB-LED gelb und warnt vor einer kritischen Temperatur.
* Über 21 Grad zeigt die RGB-LED rot und signalisiert, dass die Temperatur zu hoch ist und Maßnahmen ergriffen werden müssen.

11. Zur Steuerung der RGB-LED verwenden wir die Funktion ``setColor()``, die in den vorherigen Lektionen erstellt wurde.

.. code-block:: Arduino

    // Funktion zum Setzen der RGB-LED-Farbe
    void setColor(int red, int green, int blue) {
        // Schreibe PWM-Werte für Rot, Grün und Blau an die RGB-LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

12. Nun verwenden wir eine ``if-else if``-Anweisung, um die Farbe der RGB-LED basierend auf verschiedenen Temperaturen zu steuern.

.. code-block:: Arduino
    :emphasize-lines: 12-18

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Lese den Thermistorwert
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Berechne den Widerstand des Thermistors

        // Berechne die Temperatur in Kelvin unter Verwendung der Beta-Gleichung
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);
    
        float tempC = tempK - 273.15;  // In Celsius umrechnen
        Serial.println(tempC);         // Zeige die Temperatur in Celsius auf dem seriellen Monitor an

        // Passe die LED-Farbe basierend auf der Temperatur an
        if (tempC < 10) {
            setColor(0, 0, 255);  // Kalt: blau
        } else if (tempC >= 10 && tempC <= 21) {
            setColor(0, 255, 0);  // Angenehm: grün
        } else if (tempC > 21) {
            setColor(255, 0, 0);  // Heiß: rot
        }
        delay(1000);  // 1 Sekunde Verzögerung vor der nächsten Messung
    }

13. Dein vollständiger Code ist jetzt bereit. Du kannst ihn auf dein Arduino Uno R3 hochladen, um die Effekte zu sehen.

.. code-block:: Arduino

    // Pin-Konfigurationen
    const int tempSensorPin = A0;  // Analogeingang des NTC-Thermistors
    const int redPin = 10;         // Digitaler Pin der roten LED
    const int greenPin = 11;       // Digitaler Pin der grünen LED
    const int bluePin = 12;        // Digitaler Pin der blauen LED

    // Konstanten für die Temperaturberechnung
    const float beta = 3950.0;               // Beta-Wert des NTC-Thermistors
    const float seriesResistor = 10000;      // Widerstandswert des Reihenwiderstands (Ohm)
    const float roomTempResistance = 10000;  // Widerstand des NTC bei 25°C
    const float roomTemp = 25 + 273.15;      // Raumtemperatur in Kelvin

    void setup() {
        // Initialisiere die LED-Pins als Ausgänge
        pinMode(redPin, OUTPUT);
        pinMode(greenPin, OUTPUT);
        pinMode(bluePin, OUTPUT);

        // Starte die serielle Kommunikation mit 9600 Baud
        Serial.begin(9600);
    }

    void loop() {
        int adcValue = analogRead(tempSensorPin);                     // Lese den Thermistorwert
        float resistance = (1023.0 / adcValue - 1) * seriesResistor;  // Berechne den Widerstand des Thermistors

        // Berechne die Temperatur in Kelvin unter Verwendung der Beta-Gleichung
        float tempK = 1 / (log(resistance / roomTempResistance) / beta + 1 / roomTemp);

        float tempC = tempK - 273.15;  // In Celsius umrechnen
        Serial.println(tempC);         // Zeige die Temperatur in Celsius auf dem seriellen Monitor an

        // Passe die LED-Farbe basierend auf der Temperatur an
        if (tempC < 10) {
            setColor(0, 0, 255);  // Kalt: blau
        } else if (tempC >= 10 und tempC <= 21) {
            setColor(0, 255, 0);  // Angenehm: grün
        } else if (tempC > 21) {
            setColor(255, 0, 0);  // Heiß: rot
        }
        delay(1000);  // 1 Sekunde Verzögerung vor der nächsten Messung
    }

    // Funktion zum Setzen der RGB-LED-Farbe
    void setColor(int red, int green, int blue) {
        // Schreibe PWM-Werte für Rot, Grün und Blau an die RGB-LED
        analogWrite(11, red);
        analogWrite(10, green);
        analogWrite(9, blue);
    }

14. Speichere abschließend deinen Code und räume deinen Arbeitsplatz auf.

**Fragen**

1. Im Code werden die Temperaturen in Kelvin und Celsius berechnet. Wenn du auch die Fahrenheit-Temperatur wissen möchtest, was solltest du tun?

2. Fallen dir andere Situationen oder Orte ein, in denen ein Temperaturüberwachungssystem wie das, das wir heute gebaut haben, nützlich sein könnte?

**Zusammenfassung**

In der heutigen Lektion haben wir ein Temperaturalarm-System gebaut, das einen Thermistor verwendet, um die Temperatur eines Lagerbereichs für lagerstabile Lebensmittel zu überwachen. Wir haben gelernt, wie man Widerstandswerte vom Thermistor abliest und in Celsius-Temperaturen umwandelt. Durch unsere Programmierung haben wir außerdem Bedingungen festgelegt, um die Farbe einer RGB-LED basierend auf der Temperatur zu ändern, was eine visuelle Warnung für zu niedrige, angenehme oder zu hohe Temperaturen bietet.


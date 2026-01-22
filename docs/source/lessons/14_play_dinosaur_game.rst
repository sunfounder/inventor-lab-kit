.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community auf Facebook! Tauche gemeinsam mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum beitreten?**

    - **Experten-Support**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezielle Rabatte**: Profitiere von exklusiven Rabatten auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und festlichen Aktionen teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

14. Dinosaurier-Spiel spielen
==================================

Hast du schon einmal das süchtig machende Dinosaurier-Spiel auf Chrome gespielt, wenn du offline warst? Viele haben unzählige Minuten damit verbracht, ihre eigenen Highscores zu überbieten, indem sie sich allein auf schnelle Reflexe verlassen. Aber was wäre, wenn du einen Weg entwickeln könntest, um diese Highscores mühelos zu knacken?

Diese Lektion wird deine Art, das Spiel zu spielen, revolutionieren, indem du einfache Elektronik wie einen Fotowiderstand und ein Servo integrierst, um das Spiel zu automatisieren. Es geht nicht nur darum, das Spiel zu spielen – es geht darum, die Regeln neu zu schreiben!

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/14_dinosaur_game.mp4" type="video/mp4">
        Dein Browser unterstützt das Video-Tag nicht.
    </video>

Am Ende dieser Lektion wirst du in der Lage sein:

* Die Funktionen von Servo und Fotowiderstand zu identifizieren und zu beschreiben.
* Einen einfachen Schaltkreis mit Arduino zu bauen, der Servos und Fotowiderstände effektiv integriert.
* Arduino-Code zu schreiben und hochzuladen, der die Bewegungen des Servos basierend auf den Messwerten des Fotowiderstands steuert.
* Den aufgebauten Schaltkreis und das programmierte Arduino verwenden, um das Chrome-Dinosaurier-Spiel automatisch zu spielen.

1. Benötigte Komponenten
---------------------------

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Fotowiderstand
     - 1 * 10KΩ Widerstand
     - 1 * Servo
   * - |list_uno_r3| 
     - |list_photoresistor| 
     - |list_10kohm| 
     - |list_servo| 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - Verbindungskabel
     - 1 * Multimeter
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_wire| 
     - |list_meter|
   * - 1 * Steckbrett-Strommodul
     - 1 * 9V-Batterie
     - 1 * Batteriekabel
     - 
   * - |list_power_module| 
     - |list_battery| 
     - |list_bat_cable| 
     -

.. _ar_servo_usage:

2. Servo vorbereiten
-----------------------

**1. Servo vorstellen**

.. image:: img/14_servo_pic.jpg
    :width: 300
    :align: center

Ein Servo besteht in der Regel aus folgenden Teilen: Gehäuse, Welle, Getriebesystem, Potentiometer, Gleichstrommotor und eingebauter Platine.

So funktioniert es:

* Der Mikrocontroller sendet PWM-Signale an das Servo, und die eingebaute Platine im Servo empfängt die Signale über den Signaleingang und steuert den Motor im Inneren zum Drehen.
* Dadurch treibt der Motor das Getriebesystem an, welches nach der Verzögerung die Welle bewegt.
* Die Welle und das Potentiometer des Servos sind miteinander verbunden. Wenn sich die Welle dreht, bewegt sie das Potentiometer, das ein Spannungssignal an die eingebaute Platine ausgibt.
* Die Platine bestimmt dann die Drehrichtung und -geschwindigkeit basierend auf der aktuellen Position, sodass das Servo genau an der vorgegebenen Position stoppt und dort verharrt.

.. image:: img/14_servo_internal.png
    :width: 500
    :align: center

Die Positionierung des Servos wird durch Pulsweitenmodulation (PWM) gesteuert:

* Das Servo empfängt alle 20 ms einen Puls, wobei die Pulsdauer die Drehung des Motors bestimmt.
* Ein 1,5 ms langer Puls richtet den Motor auf die 90-Grad-Nullstellung aus.
* Kürzere Pulse als 1,5 ms drehen das Servo gegen den Uhrzeigersinn aus der Nullstellung, während längere Pulse es im Uhrzeigersinn drehen.
* Die Pulslängen reichen typischerweise von 0,5 ms (Minimum) bis 2,5 ms (Maximum), um gültige Servopositionen zu steuern.

.. image:: img/14_servo_duty.png
    :width: 600
    :align: center

**2. Schaltkreis aufbauen**

Beginnen wir nun mit dem Aufbau des Schaltkreises.

* Zuerst steckst du das Steckbrett-Strommodul in das Steckbrett und verbindest dann mit einem Verbindungskabel die negative Schiene des Steckbretts mit der GND des Arduino Uno R3, um eine gemeinsame Masse zu erreichen.

.. image:: img/14_dinosaur_power_module.png
    :width: 400
    :align: center

.. note::

    Die Reihenfolge der positiven und negativen Anschlüsse auf dem Steckbrett in der Verdrahtungsskizze ist im Vergleich zum im Bausatz enthaltenen Steckbrett vertauscht.

    In der tatsächlichen Verdrahtung musst du das Steckbrett-Strommodul von der höheren Nummer (60~65) einstecken, sodass das "-" des Strommoduls in die negative Schiene "-" des Steckbretts geht und das "+" in die positive Schiene "+".

    .. raw:: html

        <video controls style = "max-width:100%">
            <source src="_static/video/about_power_module.mp4" type="video/mp4">
            Dein Browser unterstützt das Video-Tag nicht.
        </video>

* Verwende drei kurze Verbindungskabel, um die drei Drähte deines Servos zu verlängern: Verbinde das gelbe Kabel mit Pin 9 des Arduino Uno R3, das rote Kabel mit der positiven Schiene des Steckbretts und das braune Kabel mit der negativen Schiene des Steckbretts.

.. image:: img/14_dinosaur_servo.png
    :width: 600
    :align: center
    
**3. Den Code schreiben**

Nun lass uns den Code schreiben, um zu sehen, wie man das Servo steuert.

1. Öffne die Arduino-IDE und starte ein neues Projekt, indem du im Menü „Datei“ „Neues Sketch“ auswählst.
2. Speichere deinen Sketch unter dem Namen ``Lesson14_Servo`` mit ``Ctrl + S`` oder durch Klicken auf „Speichern“.

3. Die Servo-Bibliothek einbinden.

Im Arduino-Programm gibt es einige Funktionen, die im Kern der Arduino-Umgebung integriert sind und direkt verwendet werden können, wie z. B. ``pinMode()``, ``digitalWrite()``, ``analogWrite()``, die wir in früheren Lektionen verwendet haben.

Einige spezialisierte Funktionen sind jedoch Teil von Bibliotheken, die eingebunden werden müssen, bevor man sie verwenden kann. Zum Beispiel ``Servo``, ``LiquidCrystal``, ``Stepper`` usw., die man auf der Arduino-Website auf der Seite |link_arduino_lib_page| finden kann.

Um das Servo zu steuern, müssen wir die ``Servo``-Bibliothek einbinden, die Funktionen zur Steuerung des Motors bietet.

.. code-block:: Arduino
    :emphasize-lines: 1

    #include <Servo.h>

    void setup() {
        // Der Setup-Code wird einmal ausgeführt:

    }

4. Eine Instanz der ``Servo``-Klasse erstellen, um das Servo zu steuern, und den Pin für das Servo definieren.

.. code-block:: Arduino
    :emphasize-lines: 3,5

    #include <Servo.h>

    Servo myServo;  // Erstelle ein Servo-Objekt

    const int servoPin = 9;         // Servo mit digitalem Pin 9 verbunden

5. Verwende in der ``void setup()``-Funktion die ``attach()``-Funktion aus der ``Servo``-Bibliothek, um das Servo-Objekt dem angegebenen Pin zuzuordnen.

* ``servo.attach(pin)``: Weist die Servo-Variable einem Pin zu.

    **Parameter**

    * ``servo``: Eine Variable vom Typ Servo.
    * ``pin``: Die Nummer des Pins, an den das Servo angeschlossen ist.

.. code-block:: Arduino
    :emphasize-lines: 2,3

    void setup() {
        myServo.attach(servoPin);  // Weist das Servo-Objekt dem angegebenen Pin zu
    }

6. Setze die Anfangsposition des Servos auf 0 Grad mit ``write()`` in der Servo-Bibliothek.

* ``servo.write(angle)``: Schreibt einen Wert an das Servo und steuert damit die Welle.

    **Parameter**

    * ``servo``: Eine Variable vom Typ Servo.
    * ``angle``: Der Wert, der an das Servo geschrieben wird, von 0 bis 180.

.. code-block:: Arduino
    :emphasize-lines: 9

    #include <Servo.h>

    Servo myServo;  // Erstelle ein Servo-Objekt

    const int servoPin = 9;         // Servo mit digitalem Pin 9 verbunden

    void setup() {
        myServo.attach(servoPin);  // Weist das Servo-Objekt dem angegebenen Pin zu
        myServo.write(0);          // Anfangsposition auf 0 Grad setzen
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:

    }

7. Jetzt, wo der Code fertig ist, klicke auf die Schaltfläche Hochladen, um den Code auf deine Arduino Uno R3-Platine zu übertragen. Suche in deinem Servo-Paket nach einem zweiseitigen Servo-Arm und befestige ihn so, dass er parallel zum Servo ist.

.. image:: img/14_servo_arm.png
    :width: 600
    :align: center

**Frage**

Wenn das Servo an Pin 8 oder einem anderen Nicht-PWM-Pin auf einem Arduino angeschlossen ist, wird es dennoch korrekt funktionieren? Warum oder warum nicht?

Du kannst dies zuerst testen, bevor du antwortest.

**3. Den Servo-Winkel anpassen**

Da der Servoarm die Leertaste auf der Tastatur drücken muss, musst du das Servo in einer bestimmten Position befestigen und dann mit dem Code den Servoarm steuern, um die Leertaste zu drücken.

1. Klebe das Servo neben deine Tastatur, wobei sich die Servoachse über der Leertaste befindet. Verwende starkes Klebeband, um sicherzustellen, dass das Servo sich nicht löst, wenn sich die Achse bewegt.

.. image:: img/14_attach_servo.png
    :width: 500
    :align: center

2. Fahre mit dem obigen Code fort. Verwende in der ``void loop()``-Funktion die ``write()``-Funktion, um das Servo auf 30 Grad zu stellen.

.. code-block:: Arduino
    :emphasize-lines: 14

    #include <Servo.h>

    Servo myServo;  // Erstelle ein Servo-Objekt

    const int servoPin = 9;         // Servo mit digitalem Pin 9 verbunden

    void setup() {
        myServo.attach(servoPin);  // Weist das Servo-Objekt dem angegebenen Pin zu
        myServo.write(0);          // Anfangsposition auf 0 Grad setzen
    }

    void loop() {
        // Hauptcode, der wiederholt ausgeführt wird:
        myServo.write(30);          // Auf 30 Grad einstellen
    }

3. Jetzt lade den Code auf die Arduino-Platine. Beobachte den Winkel der Servoachse, um zu sehen, ob sie die Leertaste drückt und ob sich das Servo nicht anhebt.

.. note::

    Da die Höhe der Tastatur bei jedem unterschiedlich ist, musst du entsprechend anpassen. Nach jeder Anpassung lade den Code hoch, um ihn zu aktivieren.
    
    * Wenn die Leertaste nicht gedrückt wird, erhöhe den Servo-Winkel.
    * Wenn die Leertaste gedrückt wird, aber sich das Servo anhebt, verringere den Winkel.

.. image:: img/14_servo_30.png
    :width: 500
    :align: center

4. Schreibe nun den Code, um das Servo wiederholt zwischen 0 und 30 Grad hin und her zu bewegen.

.. code-block:: Arduino
    :emphasize-lines: 13-16

    #include <Servo.h>

    Servo myServo;  // Erstelle ein Servo-Objekt

    const int servoPin = 9;         // Servo mit digitalem Pin 9 verbunden

    void setup() {
        myServo.attach(servoPin);  // Weist das Servo-Objekt dem angegebenen Pin zu
        myServo.write(0);          // Anfangsposition auf 0 Grad setzen
    }

    void loop() {
        myServo.write(30);  // Servo auf 30 Grad einstellen
        delay(100);         // Verzögerung von 100ms
        myServo.write(0);   // Servo auf 0 Grad einstellen
        delay(100);         // Verzögerung von 100ms
    }

5. Nach dem Hochladen des Codes überprüfe, ob das Servo jedes Mal die Leertaste drückt. Wenn es funktioniert, ist das Servo einsatzbereit.

.. .. raw:: html

..     <video width="600" loop autoplay>
..         <source src="_static/video/14_servo_range.mp4" type="video/mp4">
..         Dein Browser unterstützt das Video-Tag nicht.
..     </video>

.. _ar_photoresistor:

**3. Vorbereitung des Fotowiderstands**
----------------------------------------------

**1. Einführung und Messung des Fotowiderstands**

1. Beginnen Sie mit einem Fotowiderstand.

.. image:: img/17_photoresistor.png
    :width: 100
    :align: center

Ein Fotowiderstand oder Fotoleiter ist ein lichtgesteuerter variabler Widerstand. Der Widerstand eines Fotowiderstands nimmt mit zunehmender Lichtintensität ab; mit anderen Worten, er zeigt Photoleitfähigkeit.

Fotowiderstände können als widerstandsbasierte Halbleiter in lichtempfindlichen Detektorschaltungen sowie in licht- und dunkelgesteuerten Schaltungen verwendet werden. Im Dunkeln kann der Widerstand eines Fotowiderstands mehrere Megaohm (MΩ) betragen, während er unter Beleuchtung auf einige hundert Ohm sinken kann.

Das Kit enthält einen Widerstand, der bei 25 °C auf 10 KΩ ausgelegt ist. Jetzt verwenden Sie ein Multimeter, um den Widerstand des Fotowiderstands bei normalem Licht, beleuchtetem Zustand und Dunkelheit zu messen.

2. Sie müssen zwei DuPont-Kabel verwenden, um den Fotowiderstand zu verlängern.

.. image:: img/14_pho_wire.png
    :width: 500
    :align: center

Wenn Sie sich nicht sicher sind, wie Sie ihn anschließen sollen, können Sie das folgende Video ansehen.

.. raw:: html

    <video width="600" loop muted>
        <source src="_static/video/14_pho_wire.mp4" type="video/mp4">
        Ihr Browser unterstützt das Video-Tag nicht.
    </video>

3. Da der Fotowiderstand einen Nennwiderstand von 10 KΩ hat, stellen Sie das Multimeter auf den Bereich von 20 Kiloohm (20K) ein, um den Widerstand zu messen.

.. image:: img/multimeter_20k.png
    :width: 300
    :align: center

4. Setzen Sie den Fotowiderstand in das Steckbrett ein. Die Pins sind nicht richtungsgebunden und können beliebig eingesetzt werden.

.. image:: img/14_dinosaur_pho.png
    :width: 600
    :align: center

5. Berühren Sie nun die beiden Pins des Fotowiderstands mit den roten und schwarzen Prüfspitzen des Multimeters.

.. image:: img/14_dinosaur_pho_multimeter.png
    :width: 600
    :align: center

6. Lesen Sie den Widerstandswert unter dem aktuellen Umgebungslicht ab und notieren Sie ihn in der folgenden Tabelle.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Umgebung
     - Widerstand (Kiloohm)
   * - Normales Licht
     - *5,48*
   * - Helles Licht
     -
   * - Dunkelheit
     -

7. Lassen Sie nun einen Freund eine Taschenlampe oder eine andere Lichtquelle direkt auf den Fotowiderstand richten und notieren Sie den Widerstandswert, der nur einige hundert Ohm betragen könnte. Daher müssen Sie das Multimeter möglicherweise auf 2 KΩ oder sogar auf 200 Ohm einstellen, um eine genauere Messung zu erhalten.

.. note::

    Wir haben die Widerstandseinheit in der Tabelle auf Kiloohm festgelegt. 1 Kiloohm (kΩ) = 1000 Ohm.

    Wenn Sie den Bereich von 200 Ohm gewählt und einen Messwert von 164,5 Ohm erhalten haben, konvertieren Sie ihn in 0,16 Kiloohm (Runden auf zwei Dezimalstellen empfohlen) und tragen Sie den umgerechneten Wert in die Tabelle ein.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Umgebung
     - Widerstand (Kiloohm)
   * - Normales Licht
     - *≈5,48*
   * - Helles Licht
     - *≈0,16*
   * - Dunkelheit
     - 

8. Bei Dunkelheit kann der Widerstand des Fotowiderstands mehrere Megaohm erreichen, daher müssen wir das Multimeter auf den 2-Megaohm-Bereich einstellen.

.. image:: img/multimeter_2mΩ.png
    :width: 300
    :align: center

9. Decken Sie den Fotowiderstand vollständig mit einem schwarzen Objekt ab und notieren Sie den gemessenen Widerstand in der Tabelle.

.. note::
    Wir haben die Widerstandseinheit in der Tabelle auf Kiloohm festgelegt. 1 Megaohm (MΩ) = 1000 Kiloohm.

    Wenn Sie den 2-Megaohm-Bereich gewählt und einen Messwert von 1,954 Megaohm erhalten haben, konvertieren Sie ihn in 1954 Kiloohm, was der Wert ist, den Sie eintragen sollten.

    Wenn der Messwert direkt höher als 2 MΩ ist, wird "1." angezeigt. In diesem Fall können Sie direkt 2 Megaohm eintragen oder ein genaueres Multimeter verwenden, um den exakten Wert zu messen.

.. list-table::
   :widths: 20 20
   :header-rows: 1

   * - Umgebung
     - Widerstand (Kiloohm)
   * - Normales Licht
     - *≈5,48*
   * - Helles Licht
     - *≈0,16*
   * - Dunkelheit
     - *≈1954*

Aus den Messungen haben wir die photoleitenden Eigenschaften des Fotowiderstands bestätigt: Je stärker das Licht, desto geringer der Widerstand; je schwächer das Licht, desto höher der Widerstand, der mehrere Megaohm erreichen kann.


**2. Aufbau der Schaltung**

1. Fahren Sie mit dem Aufbau der Schaltung fort. Verbinden Sie einen Pin des Fotowiderstands mit dem negativen Anschluss des Steckbretts und den anderen Pin mit dem A0-Pin auf dem Arduino Uno R3.

.. image:: img/14_dinosaur_pho_gnd_5v.png
    :width: 600
    :align: center

2. Setzen Sie einen 10K-Widerstand in dieselbe Reihe wie den Anschluss des Fotowiderstands an A0 ein.

.. image:: img/14_dinosaur_resistor.png
    :width: 600
    :align: center

In dieser Schaltung sind der 10K-Widerstand und der Fotowiderstand in Reihe geschaltet, und der durch sie fließende Strom ist derselbe. Der 10K-Widerstand dient als Schutz, und der A0-Pin liest den Wert nach der Spannungsumwandlung des Fotowiderstands.

Wenn das Licht stärker wird, nimmt der Widerstand des Fotowiderstands ab, dann sinkt seine Spannung, sodass der Wert des A0-Pins sinkt. Wenn das Licht stark genug ist, wird der Widerstand des Fotowiderstands fast 0 sein, und der Wert des A0-Pins wird nahezu 0 sein. Zu diesem Zeitpunkt spielt der 10K-Widerstand eine Schutzfunktion und verhindert einen Kurzschluss, indem er verhindert, dass 5V und GND direkt miteinander verbunden werden.

Wenn Sie den Fotowiderstand in eine dunkle Umgebung bringen, wird der Wert des A0-Pins steigen. In einer ausreichend dunklen Umgebung wird der Widerstand des Fotowiderstands unendlich und seine Spannung wird fast 5V betragen (der 10K-Widerstand wird vernachlässigbar), und der Wert des A0-Pins wird nahe 1023 sein.

3. Verbinden Sie den anderen Pin des 10K-Widerstands mit dem positiven Anschluss des Steckbretts.

.. image:: img/14_dinosaur_resistor_vcc.png
    :width: 600
    :align: center

**3. Schreiben des Codes**

Nun müssen Sie die Werte des Fotowiderstands auslesen.

1. Öffnen Sie den zuvor gespeicherten Sketch „Lesson14_Servo“. Wählen Sie im Menü „Datei“ die Option „Speichern unter...“ und benennen Sie ihn in „Lesson14_Photoresistor“ um. Klicken Sie auf „Speichern“.

2. Zuerst initialisieren Sie den Pin für den Fotowiderstand.

.. code-block:: Arduino
    :emphasize-lines: 6

    #include <Servo.h>

    Servo myServo;  // Erstellen eines Servo-Objekts

    const int servoPin = 9;         // Servomotor angeschlossen an digitalen Pin 9
    const int lightSensorPin = A0;  // Lichtsensor angeschlossen an analogen Pin A0

3. Wir müssen den seriellen Monitor verwenden, um die Werte des Fotowiderstands anzuzeigen. Initialisieren Sie daher die serielle Kommunikation mit einer Baudrate von 9600 in der Funktion ``void setup()``.

.. code-block:: Arduino
    :emphasize-lines: 9

    #include <Servo.h>

    Servo myServo;  // Erstellen eines Servo-Objekts

    const int servoPin = 9;  // Servo angeschlossen an digitalen Pin 9
    const int lightSensorPin = A0;  // Lichtsensor angeschlossen an analogen Pin A0

    void setup() {
        Serial.begin(9600);        // Starten der seriellen Kommunikation
        myServo.attach(servoPin);  // Servo-Objekt an den angegebenen Pin anschließen
        myServo.write(0);          // Anfangsposition auf 0 Grad setzen
    }

4. Erstellen Sie nun in der Funktion ``void loop()`` eine Variable ``lightValue``, um den ausgelesenen Wert des Fotowiderstands zu speichern, und geben Sie diesen dann im seriellen Monitor aus.

.. note::

    Um Störungen durch den Servo zu vermeiden, können Sie den servo-bezogenen Code mit ``Ctrl+/`` auskommentieren.

    Behalten Sie einen ``delay(100)``, um die gedruckten Daten im seriellen Monitor besser lesen zu können.

.. code-block:: Arduino
    :emphasize-lines: 15-17,22

    #include <Servo.h>

    Servo myServo;  // Erstellen eines Servo-Objekts

    const int servoPin = 9;  // Servo angeschlossen an digitalen Pin 9
    const int lightSensorPin = A0;  // Lichtsensor angeschlossen an analogen Pin A0
    
    void setup() {
        Serial.begin(9600);        // Starten der seriellen Kommunikation
        myServo.attach(servoPin);  // Servo-Objekt an den angegebenen Pin anschließen
        myServo.write(0);          // Anfangsposition auf 0 Grad setzen
    }

    void loop() {
        int lightValue = analogRead(lightSensorPin);  // Wert vom Lichtsensor auslesen
        Serial.print("Lichtsensorwert: ");
        Serial.println(lightValue);  // Lichtsensorwert im seriellen Monitor ausgeben

        // myServo.write(30);  // Servo auf 30 Grad setzen
        // delay(100);         // 100ms Verzögerung
        // myServo.write(0);   // Servo auf 0 Grad setzen
        delay(100);         // 100ms Verzögerung
    }

5. Laden Sie nun den Code auf das Arduino Uno R3 hoch, um die gedruckten Daten anzuzeigen.

**4. Daten anzeigen**

Sie müssen das Dinosaurierspiel auf der Offline-Seite von Chrome öffnen und den Fotowiderstand verwenden, um den Unterschied der Werte zwischen dem leeren Bereich und dem schwarzen Kaktus-Symbol zu erkennen und einen Schwellenwert festzulegen. Auf diese Weise können Sie erkennen, ob ein schwarzer Kaktus erkannt wird, indem Sie den Wert mit dem Schwellenwert vergleichen.

Öffnen Sie Google Chrome und geben Sie „chrome://dino/“ ein. Sie sehen eine Aufforderung mit der Meldung „Leertaste drücken, um zu spielen“. Drücken Sie die Leertaste und lassen Sie den Dinosaurier auf einen schwarzen Kaktus treffen, um einen stabilen Bildschirm zu erhalten.

.. image:: img/14_dinosaur_google.png
    :width: 600
    :align: center

2. Öffnen Sie Google Chrome und Arduino IDE nebeneinander.

.. image:: img/14_dinosaur_google_arduino.png
    :width: 600
    :align: center

3. Platzieren Sie nun das Steckbrett auf dem Bildschirm des Computers und verwenden Sie den Fotowiderstand, um den Wert im seriellen Monitor im weißen Bereich zu ermitteln. Mein Wert liegt bei etwa 268.

.. note::

    * Stellen Sie sicher, dass der Fotowiderstand vollständig gegen den Bildschirm des Computers gedrückt ist.
    * Es wird empfohlen, die Bildschirmhelligkeit auf Maximum einzustellen, um den besten Kontrastwert zu erzielen.

.. image:: img/14_dinosaur_read_pho_white.png

4. Bewegen Sie den Fotowiderstand nun an die Stelle, an der sich der Dinosaurier befindet, und notieren Sie den gedruckten Wert. Mein Wert liegt bei etwa 355.

.. image:: img/14_dinosaur_read_pho_black.png

5. Sie können die Leertaste drücken, um das Spiel laufen zu lassen, und mehrmals testen, um die Werte zu ermitteln, die Sie im weißen Bereich und beim schwarzen Kaktus erhalten.

.. note::

    * Basierend auf meinen Testergebnissen würde ich den Schwellenwert auf 310 setzen (jeder Wert zwischen 268 und 355 ist akzeptabel, aber es ist am besten, einen Mittelwert zu wählen). 
    * Wenn der Wert des Fotowiderstands größer als 310 ist, bedeutet dies, dass er das schwarze Kaktus-Symbol erkennt; andernfalls erkennt er den leeren Raum.

Der Fotowiderstand ist nun einsatzbereit und Sie können mit dem nächsten Schritt fortfahren, um den Servo und den Fotowiderstand zu kombinieren und das Dinosaurierspiel zu spielen.

**4. Spielen Sie das Dinosaurierspiel**
------------------------------------------

Hier müssen wir den Fotowiderstand an einer geeigneten Stelle auf dem Bildschirm befestigen und dann einen Code schreiben, um den Servo basierend auf dem Wert des Fotowiderstands zu drehen. Zum Beispiel sollte der Servo auf 30 Grad drehen, wenn der Wert des Fotowiderstands 310 überschreitet; andernfalls sollte er auf 0 Grad bleiben.

Schauen wir uns an, wie das geht.

**1. Schreiben des Codes**

Öffnen Sie den zuvor gespeicherten Sketch „Lesson14_Photoresistor“. Wählen Sie im Menü „Datei“ die Option „Speichern unter...“ und benennen Sie ihn in „Lesson14_Dinosaur_Game“ um. Klicken Sie auf „Speichern“.

Verwenden Sie in ``void loop()`` eine ``if-else``-Anweisung, um die Bedingungen für die Bewegung des Servos festzulegen.

Wie im vorherigen Schritt bestimmt, sollte der Servo auf 30 Grad drehen, wenn der Wert des Fotowiderstands 310 überschreitet und somit ein schwarzes Kaktus-Symbol erkannt wird, um die Leertaste zu drücken und den Dinosaurier über den Kaktus springen zu lassen.

.. code-block:: Arduino
    :emphasize-lines: 19-24

    #include <Servo.h>

    Servo myServo;  // Erstellen eines Servo-Objekts

    const int servoPin = 9;         // Servomotor angeschlossen an digitalen Pin 9
    const int lightSensorPin = A0;  // Lichtsensor angeschlossen an analogen Pin A0

    void setup() {
        Serial.begin(9600);        // Starten der seriellen Kommunikation
        myServo.attach(servoPin);  // Servo-Objekt an den angegebenen Pin anschließen
        myServo.write(0);          // Anfangsposition auf 0 Grad setzen
    }

    void loop() {
        int lightValue = analogRead(lightSensorPin);  // Wert vom Lichtsensor auslesen
        // Serial.print("Lichtsensorwert: ");
        // Serial.println(lightValue);  // Lichtsensorwert im seriellen Monitor ausgeben

        if (lightValue > 310) {
            myServo.write(30);  // Wenn der Lichtsensorwert größer als 310 ist, Servo auf 30 Grad bewegen
            delay(50);
        } else {
            myServo.write(0);  // Ansonsten bleibt der Servo bei 0 Grad
        }
    }

3. Jetzt können Sie den Code auf das Arduino Uno R3 hochladen.

**2. Anbringen des Fotowiderstands**

Die Position des Fotowiderstands beeinflusst das Spielerlebnis.

* Ist er zu nah am Dinosaurier, wird der Kaktus zu spät erkannt und der Dinosaurier hat nicht genug Zeit zum Springen.
* Ist er zu weit vom Dinosaurier entfernt, springt er zu früh, nachdem der Kaktus erkannt wurde.
* Die Höhe zur Horizontalen beeinflusst die Empfindlichkeit bei der Erkennung des schwarzen Kaktus.

Bringen Sie nun den Fotowiderstand mit Klebeband in Position. Drücken Sie die Leertaste, um das Spiel zu starten, und sehen Sie, ob der Dinosaurier über den schwarzen Kaktus springt. Wenn er nicht darüber springt, bewegen Sie das Steckbrett etwas nach rechts; wenn er zu früh springt, bewegen Sie es etwas nach links. Passen Sie es mehrmals an, um die beste Position zu finden.

Nun können Sie die Leertaste drücken und mit dem Dinosaurierspiel beginnen.

.. raw:: html

    <video width="600" loop>
        <source src="_static/video/14_dinosaur_game.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

**Zusammenfassung**

In dieser spannenden Lektion haben wir uns von den Grundlagen der Servos und Fotowiderstände zu einem Aufbau vorgearbeitet, der das Chrome-Dinosaurier-Spiel von selbst spielt. Wir haben gelernt, eine Schaltung zu montieren, die Lichtsignale mit einem Fotowiderstand interpretiert und einem Servo befiehlt, entsprechend zu reagieren. Unser abschließender Aufbau hat nicht nur das Spiel gemeistert, sondern sich auch an seine Herausforderungen angepasst, was eine fantastische Verschmelzung von einfachem Spiel und Grundlagen der Elektronik-Automatisierung darstellt. Durch die Automatisierung des Dinosaurierspiels haben wir den ersten Schritt in die Welt der Robotik und Sensorik gemacht und damit den Weg für komplexere und aufregendere Projekte in der Zukunft geebnet.


.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer ein in Raspberry Pi, Arduino und ESP32 mit gleichgesinnten Technikbegeisterten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Sonderrabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

23. „Twinkle, Twinkle, Little Star“ spielen
==============================================
In dieser Lektion tauchen wir in die faszinierende Verbindung zwischen Musik und Technologie ein. Du lernst, wie verschiedene Tonhöhen durch Frequenzänderungen erzeugt werden und wie dieses Prinzip mit einem Mikrocontroller wie Arduino genutzt werden kann, um einen Piezo-Summer zu steuern. Am Ende dieser Lektion wirst du nicht nur die Grundlagen der musikalischen Frequenzen verstehen, sondern auch in der Lage sein, ein Arduino so zu programmieren, dass es eine einfache Melodie spielt.

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/23_little_star.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Am Ende dieser Lektion wirst du in der Lage sein:

* Zu verstehen, wie musikalische Tonhöhen spezifischen Frequenzen entsprechen.
* Arrays zu verwenden, um Noten zu speichern und zu manipulieren und dadurch das Programmieren zu vereinfachen.
* Ein Programm zu schreiben und auszuführen, das einen passiven Piezo-Summer steuert, um "Twinkle, Twinkle, Little Star" zu spielen.

Musikalische Frequenzen und Klangerzeugung
------------------------------------------------
.. image:: img/7_sound.png
  :width: 400
  :align: center

Verschiedene Musikinstrumente erzeugen unterschiedliche Tonhöhen durch Änderung der Frequenz.
Zum Beispiel bringen beim Klavier die Tasten die entsprechenden Saiten zum schnellen Schwingen, wodurch spezifische Tonhöhen erzeugt werden.
Wissenschaftler und Musiker haben verschiedene Methoden der Musiksstimmung und Tonhöhenstandards entwickelt, indem sie diese Schwingungsfrequenzen präzise gemessen haben.

Wenn du ein Arduino oder einen anderen Mikrocontroller steuerst, um ein elektrisches Signal an einen Piezo-Summer zu senden, schwingt die Membran des Summers je nach Frequenz des Signals schnell hin und her und erzeugt so einen Klang. Ein auf 440 Hz eingestelltes Signal erzeugt zum Beispiel die Standard-Tonhöhe "A4", die als Referenzpunkt in der Musikstimmung dient.
Wenn die Frequenz steigt oder fällt, ändert sich auch die erzeugte Tonhöhe entsprechend, sodass eine Bandbreite von tiefen bis hohen Tönen in einer musikalischen Komposition erreicht wird.


In der westlichen Musik umfasst eine Oktave 12 Tonhöhen (Halbtöne), von C bis B und dann zurück zu einem höheren C.

Zum Beispiel beträgt die Frequenz von Mittlerem C (meistens als C4 bezeichnet) etwa 261,63 Hz. Die Frequenz einer Note kann mit der folgenden Formel berechnet werden:

.. image:: img/7_music_format.png

wobei f_0 die Referenztonhöhe (in der Regel A4 mit einer Frequenz von 440 Hz) ist, und n die Anzahl der Halbtonschritte von der Referenztonhöhe bis zur Zieltonhöhe angibt (positive Zahlen bedeuten eine Erhöhung, negative Zahlen eine Absenkung).
Mit dieser Formel können wir die Frequenz jeder Note berechnen.

Hier ist eine Frequenztabelle:

* C (C4): 262 Hz (actually close to 261.63 Hz, rounded to 262)
* D (D4): 294 Hz
* E (E4): 330 Hz
* F (F4): 349 Hz
* G (G4): 392 Hz
* A (A4): 440 Hz
* B (B4): 494 Hz

Nun werden wir die Geheimnisse der Noten mit Arduino und einem Piezo-Summer erkunden. Lass uns den passiven Summer die ersten zwei Zeilen von „Twinkle, Twinkle, Little Star“ spielen lassen:

.. note::

  Die Melodie von „Twinkle, Twinkle, Little Star“ basiert auf einfachen Notenkombinationen,
  und die Melodie dieses Liedes geht auf Variationen von „Ah vous dirai-je, Maman“ des französischen Komponisten Wolfgang Amadeus Mozart zurück,
  was sie für Anfänger sehr geeignet macht.

  Hier ist das grundlegende Notenblatt für „Twinkle, Twinkle, Little Star“, einschließlich jeder Note:

  .. code-block:: 

    C C G G A A G
    F F E E D D C
    G G F F E E D
    G G F F E E D
    C C G G A A G
    F F E E D D C

Schaltungsaufbau
-----------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Steckbrett
     - 1 * Passiver Summer
     - Jumper-Kabel
   * - |list_uno_r3| 
     - |list_breadboard| 
     - |list_passive_buzzer| 
     - |list_wire| 
   * - 1 * USB-Kabel
     -
     - 
     - 
   * - |list_usb_cable| 
     -
     - 
     - 



**Schritt-für-Schritt Aufbau**

Diese Lektion verwendet die gleiche Schaltung wie :ref:`ar_siren_sound`.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Codeerstellung - Array
--------------------------
1. Öffne die Arduino IDE und starte ein neues Projekt, indem du "Neue Datei" aus dem Menü "Datei" wählst.
2. Speichere deinen Sketch unter dem Namen ``Lesson23_Array`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Erstelle nun zu Beginn des Codes ein Array, das die Noten von „Twinkle, Twinkle, Little Star“ speichert.

.. code-block:: Arduino

  // Definiere die Frequenzen für die Noten der C-Dur-Tonleiter (Oktave beginnend mit mittlerem C)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Hohes C

  // Definiere ein Array, das die Reihenfolge der Noten in der Melodie enthält
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };

Ein Array ist eine Datenstruktur, die in der Arduino-Programmierung verwendet wird, um mehrere Elemente des gleichen Typs zu speichern.
Es ist ein sehr grundlegendes und leistungsfähiges Werkzeug, das bei richtiger Verwendung die Programmier-Effizienz und -Leistung erheblich steigern kann.
Arrays können Elemente wie ganze Zahlen, Gleitkommazahlen und Zeichen speichern.

Ähnlich wie bei der Erstellung von Variablen und Funktionen wird auch bei der Erstellung eines Arrays der Array-Typ und der Array-Name angegeben - ``int melody[]``.

Die Elemente innerhalb der ``{}`` Klammern werden als Array-Elemente bezeichnet, beginnend bei Index 0, sodass ``melody[0]`` dem ersten ``c(262)`` entspricht und ``melody[13]`` ebenfalls ``c(262)`` ist.

4. Nun drucke die Elemente an den Indizes 0 und 13 des Arrays ``melody[]`` im seriellen Monitor aus.

.. code-block:: Arduino
  :emphasize-lines: 17,18

  // Definiere die Frequenzen für die Noten der C-Dur-Tonleiter (Oktave beginnend mit mittlerem C)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Hohes C

  // Definiere ein Array, das die Reihenfolge der Noten in der Melodie enthält
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };

  void setup() {
    // Stelle deinen Setup-Code hier bereit, der einmal ausgeführt wird:
    Serial.begin(9600);  // Initialisiere die serielle Kommunikation mit einer Baudrate von 9600
    Serial.println(melody[0]);
    Serial.println(melody[13]);
  }
  
  void loop() {
    // Stelle deinen Hauptcode hier bereit, der wiederholt ausgeführt wird:
  }

5. Nach dem Hochladen des Codes auf das Arduino Uno R3 öffne den seriellen Monitor, und du wirst zweimal 262 sehen.

.. code-block::

  262
  262

6. Wenn du jedes Element im Array ``melody[]`` einzeln ausdrucken möchtest, musst du zuerst die Länge des Arrays kennen. Du kannst die Funktion ``sizeof()`` verwenden, um die Anzahl der Elemente im Array zu berechnen.

.. code-block:: Arduino
  :emphasize-lines: 4

  void setup() {
    // Stelle deinen Setup-Code hier bereit, der einmal ausgeführt wird:
    Serial.begin(9600);  // Initialisiere die serielle Kommunikation mit einer Baudrate von 9600
    int notes = sizeof(melody) / sizeof(melody[0]); // Berechne die Anzahl der Elemente
  }

  
* ``sizeof(melody)`` gibt die Gesamtanzahl der Bytes zurück, die alle Elemente im Array belegen.
* ``sizeof(melody[0])`` gibt die Anzahl der Bytes zurück, die ein einzelnes Element im Array belegt.
* Die Division der Gesamtbytes durch die Bytes pro Element ergibt die Gesamtanzahl der Elemente im Array.

7. Verwende dann eine ``for``-Schleife, um durch die Elemente des Arrays ``melody[]`` zu iterieren und drucke sie mit der Funktion ``Serial.println()`` aus.

.. code-block:: Arduino

  // Definiere die Frequenzen für die Noten der C-Dur-Tonleiter (Oktave beginnend mit mittlerem C)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Hohes C

  // Definiere ein Array, das die Reihenfolge der Noten in der Melodie enthält
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };

  void setup() {
    // Stelle deinen Setup-Code hier bereit, der einmal ausgeführt wird:
    Serial.begin(9600);                              // Initialisiere die serielle Kommunikation mit einer Baudrate von 9600
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Melody-Array
    for (int i = 0; i < notes; i = i + 1) {
      // Drucke die Frequenz jeder Note auf dem seriellen Monitor aus
      Serial.println(melody[i]);
    }
  }

  void loop() {
    // Stelle deinen Hauptcode hier bereit, der wiederholt ausgeführt wird:
  }

8. Nach dem Hochladen des Codes auf das Arduino Uno R3 öffne den seriellen Monitor, und du wirst die Elemente im Array ``melody[]`` nacheinander gedruckt sehen.

.. code-block::

  262
  262
  392
  392
  440
  440
  392
  349
  349
  330
  ...

**Fragen**

Du kannst auch Operationen auf den Elementen im Array durchführen, wie zum Beispiel das Ändern zu ``Serial.println(melody[i] * 1.3);``. Welche Daten wirst du erhalten und warum?


Codeerstellung - „Twinkle, Twinkle, Little Star“ spielen
-----------------------------------------------------------------

Da wir nun ein solides Verständnis für die Erstellung von Arrays, den Zugriff auf Array-Elemente und die Berechnung ihrer Längen und Operationen haben, wollen wir dieses Wissen anwenden, um einen passiven Piezo-Summer so zu programmieren, dass er „Twinkle, Twinkle, Little Star“ mit gespeicherten Frequenzen und Intervallen spielt.

1. Öffne den zuvor gespeicherten Sketch, ``Lesson23_Array``. Wähle „Speichern unter...“ aus dem Menü „Datei“ und benenne es in ``Lesson23_Little_Star`` um. Klicke auf "Speichern".

2. Definiere zuerst den Pin für den Summer.

.. code-block:: Arduino

  const int buzzerPin = 9;  // Weist dem Pin 9 die Konstante für den Summer zu


3. Erstelle nun ein weiteres Array, um die Dauer der Noten zu speichern.

.. code-block:: Arduino
  :emphasize-lines: 3

  // Richte die Reihenfolge der Noten und deren Dauer in Millisekunden ein
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };
  int noteDurations[] = { 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000 };

4. Verschiebe nun einen Teil des Codes von ``void setup()`` in ``void loop()``.

.. code-block:: Arduino
  :emphasize-lines: 8-13

  void setup() {
    // Stelle deinen Setup-Code hier bereit, der einmal ausgeführt wird:
    Serial.begin(9600);                              // Initialisiere die serielle Kommunikation mit einer Baudrate von 9600
  }

  void loop() {
    // Stelle deinen Hauptcode hier bereit, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Melody-Array
    for (int i = 0; i < notes; i = i + 1) {
      // Drucke die Frequenz jeder Note auf dem seriellen Monitor aus
      Serial.println(melody[i]);
    }
  }

5. Kommentiere im ``for``-Statement den Druckbefehl aus und verwende die ``tone()``-Funktion, um die Noten abzuspielen.

.. code-block:: Arduino
  :emphasize-lines: 9

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Melody-Array
    for (int i = 0; i < notes; i = i + 1) {
      // Drucke jede Frequenz der Noten auf den seriellen Monitor
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Spiele die Note
    }
  }


6. Um die Melodie natürlicher klingen zu lassen, füge nach jeder Note eine kurze Pause hinzu. Hier multiplizieren wir die Notendauer mit 1,30, um das Intervall zu berechnen und die Melodie weniger gehetzt wirken zu lassen.

.. code-block:: Arduino
  :emphasize-lines: 10

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Melody-Array
    for (int i = 0; i < notes; i = i + 1) {
      // Drucke jede Frequenz der Noten auf den seriellen Monitor
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Spiele die Note
      delay(noteDurations[i] * 1.30);                // Warte, bevor die nächste Note gespielt wird
    }
  }

7. Verwende die ``noTone()``-Funktion, um die Tonausgabe am aktuellen Pin zu stoppen. Dies ist ein notwendiger Schritt, um sicherzustellen, dass jede Note klar gespielt wird, ohne in die nächste überzugehen.

.. code-block:: Arduino
  :emphasize-lines: 11

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Melody-Array
    for (int i = 0; i < notes; i = i + 1) {
      // Drucke jede Frequenz der Noten auf den seriellen Monitor
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Spiele die Note
      delay(noteDurations[i] * 1.30);                // Warte, bevor die nächste Note gespielt wird
      noTone(buzzerPin);                             // Stoppe das Spielen der Note
    }
  }

8. Dein vollständiger Code ist unten dargestellt. Sobald du den Code auf das Arduino Uno R3 hochgeladen hast, wirst du hören, wie der Summer "Twinkle Twinkle Little Star" spielt.

.. code-block:: Arduino

  int buzzerPin = 9;  // Weist den Pin 9 als Konstante für den Summer zu

  // Definiere die Frequenzen für die Noten der C-Dur-Tonleiter (Oktave beginnend mit mittlerem C)
  int c = 262;
  int d = 294;
  int e = 330;
  int f = 349;
  int g = 392;
  int a = 440;
  int b = 494;
  int C = 523;  // Hohes C

  // Richte die Reihenfolge der Noten und deren Dauer in Millisekunden ein
  int melody[] = { c, c, g, g, a, a, g, f, f, e, e, d, d, c, g, g, f, f, e, e, d, g, g, f, f, e, e, d, c, c, g, g, a, a, g, f, f, e, e, d, d, c };
  int noteDurations[] = { 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000, 500, 500, 500, 500, 500, 500, 1000 };

  void setup() {
    // Initialisiere den Setup-Code, der einmal ausgeführt wird:
    Serial.begin(9600);  // Initialisiere die serielle Kommunikation mit einer Baudrate von 9600
  }

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    int notes = sizeof(melody) / sizeof(melody[0]);  // Berechne die Anzahl der Elemente
    // Schleife durch jede Note im Melody-Array
    for (int i = 0; i < notes; i = i + 1) {
      // Drucke jede Frequenz der Noten auf den seriellen Monitor
      // Serial.println(melody[i]);

      tone(buzzerPin, melody[i], noteDurations[i]);  // Spiele die Note
      delay(noteDurations[i] * 1.30);                // Warte, bevor die nächste Note gespielt wird
      noTone(buzzerPin);                             // Stoppe das Spielen der Note
    }
  }
  
9. Vergiss nicht, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Frage**

Wenn du den passiven Summer in der Schaltung durch einen aktiven Summer ersetzt, kannst du dann trotzdem „Twinkle Twinkle Little Star“ spielen? Warum?

**Zusammenfassung**

Nachdem der Unterricht nun beendet ist, haben wir in dieser Lektion gelernt, wie man Arrays verwendet, um Daten zu speichern, die Länge von Arrays zu berechnen, Elemente innerhalb eines Arrays zu indexieren und Operationen mit jedem Element durchzuführen. Indem wir Notenfrequenzen und Zeitintervalle in Arrays speicherten und sie mithilfe einer For-Schleife durchliefen, haben wir erfolgreich einen passiven Summer so programmiert, dass er „Twinkle, Twinkle, Little Star“ spielt.

Zusätzlich haben wir gelernt, wie man die Wiedergabe einer Note mit der ``noTone()``-Funktion pausiert.

Diese Lektion hat nicht nur unser Verständnis von Array-Operationen und Kontrollstrukturen in der Programmierung vertieft, sondern auch gezeigt, wie diese Konzepte angewendet werden können, um Musik mit elektronischen Komponenten zu erzeugen. Auf unterhaltsame und ansprechende Weise verknüpften wir theoretisches Wissen mit praktischen Anwendungen.


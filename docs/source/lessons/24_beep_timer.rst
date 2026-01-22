.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche tiefer in Raspberry Pi, Arduino und ESP32 zusammen mit anderen Enthusiasten ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalte frühzeitig Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nimm an Gewinnspielen und festlichen Aktionen teil.

    👉 Bereit, mit uns zu erkunden und zu erschaffen? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

24. Der Pomodoro-Timer
===========================================

In dieser Lektion werden wir die Schnittstelle zwischen Zeitmanagement und Technologie erkunden, indem wir einen Pomodoro-Timer mit einem Arduino und einem aktiven Summer erstellen. Du wirst lernen, wie du die internen Zeitfunktionen des Arduino nutzt, um einen Timer zu bauen, der Arbeitsintervalle von 25 Minuten Fokusarbeit und 5 Minuten Pause unterteilt. Diese Methode, bekannt als die Pomodoro-Technik, steigert Produktivität und Konzentration. Während des Kurses wirst du eine solide Grundlage in der elektronischen Zeitmessung erlangen und praktische Erfahrungen in Programmierung und Schaltungsaufbau sammeln. Am Ende wirst du einen funktionalen Pomodoro-Timer gebaut haben, der dir hilft, deine Zeit effizient zu nutzen!

.. image:: img/19_tomato_timer.jpg
  :width: 500
  :align: center

.. raw:: html

     <video controls style = "max-width:90%">
        <source src="_static/video/24_beep_timer.mp4" type="video/mp4">
        Your browser does not support the video tag.
    </video>

Am Ende dieser Lektion wirst du in der Lage sein:

* Die historische Bedeutung von Klang in der Zeitmessung zu verstehen.
* Die Komponenten zu identifizieren, die zum Bau einer elektronischen Timer-Schaltung erforderlich sind.
* Einen Arduino zu programmieren, um einen Summer für das Zeitmanagement mit den Funktionen ``delay()`` und ``millis()`` zu steuern.
* Die Pomodoro-Technik in der Praxis anzuwenden, indem du einen Timer erstellst, der zwischen Arbeits- und Pausenphasen wechselt.

Uhren und Klang
--------------------

In der Antike wurden große Glockenschläge verwendet, um den Zeitablauf und bestimmte gesellschaftliche Ereignisse zu markieren.
Beispielsweise nutzten mittelalterliche europäische Städte Kirchenglocken, um Gebetszeiten sowie den Beginn und das Ende der Arbeitstage zu signalisieren.
Diese Glockenschläge waren mehr als nur Zeitmarkierungen; sie dienten als Werkzeuge für die soziale Ordnung, um die sich das tägliche Leben der Gemeinschaft drehte.

**Mechanische Uhren und Klang**

.. image:: img/7_big_ben.png
  :width: 500
  :align: center

Mit der Entwicklung mechanischer Uhren, insbesondere mit der Konstruktion des Big Ben, wurden Uhren mit komplexeren Glocken- und Zeitmechanismen ausgestattet.
Der Klang von Big Ben wird von seinen großen Bronzeklocken getragen, die sowohl die Reichweite des Schalls als auch die Präzision der Zeitansage verbessern.
In vielen Städten und Gemeinden wurde der Klang von Big Ben zu einer Referenz für die Bewohner, ihre täglichen Aktivitäten zu koordinieren. Er spielte eine entscheidende Rolle bei der präziseren Zeitplanung für die Navigation, Zugfahrpläne und mehr.

**Klangsteuerung im elektronischen Zeitalter**

.. image:: img/19_timer.jpg
  :width: 500
  :align: center

Im elektronischen Zeitalter erlebten Klang-Timer eine neue Entwicklung. Durch die Einführung elektronischer Summer, insbesondere mit Hilfe von Mikrocontrollern wie Arduino,
wurde die Zeitmessung unabhängig von großen mechanischen Geräten. Diese kleinen Geräte können Töne mit unterschiedlichen Frequenzen und Tonhöhen erzeugen,
die für verschiedene Zeitsteuerungsanwendungen verwendet werden können, von einfachen Küchentimern bis hin zu komplexen industriellen Prozesssteuerungssystemen.
Beispiele sind Rufsysteme in modernen Krankenhäusern, Schulglocken und Erinnerungen in persönlichen elektronischen Geräten, die alle elektronische Summer zur Zeitmessung verwenden.

Aufbau der Schaltung
--------------------------

**Benötigte Komponenten**


.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Steckbrett
     - 1 * Aktiver Summer
     - Verbindungskabel
   * - |list_uno_r3| 
     - |list_breadboard| 
     - |list_active_buzzer| 
     - |list_wire| 
   * - 1 * USB-Kabel
     -
     - 
     - 
   * - |list_usb_cable| 
     -
     - 
     - 



**Schritt-für-Schritt-Anleitung**

Diese Lektion verwendet denselben Schaltkreis wie :ref:`ar_morse_code`.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Coding Creation - Tick Tick
-------------------------------

In Arduino ist ``delay()`` die einfachste und am häufigsten verwendete Zeitfunktion.
Wir verwenden sie oft, um das Programm für kurze Zeit anzuhalten, was in Kombination mit Schleifen einen blinkenden LED-Effekt erzeugen kann. Hier verwenden wir die ``delay()``-Funktion, um den Summer einmal pro Sekunde ertönen zu lassen.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „New Sketch“ aus dem Menü „Datei“ auswählst.
2. Speichere deinen Sketch als ``Lesson24_Timer_Tick_Tick`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Schreibe den folgenden Code:

.. code-block:: Arduino

  const int buzzerPin = 9;   // Weist die Konstante für den Summer dem Pin 9 zu  
  
  void setup() {
    // Initialisierungscode, der einmal ausgeführt wird:
    pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 auf Ausgang
  } 

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    digitalWrite(buzzerPin, HIGH);  // Schaltet den Summer ein
    delay(100);                     // Piepton-Dauer: 100 Millisekunden
    digitalWrite(buzzerPin, LOW);   // Schaltet den Summer aus
    delay(1000);                    // Intervall zwischen den Signalen: 1000 Millisekunden
  }

In dieser Konfiguration hält die erste ``delay()``-Funktion das Arduino Uno R3 für 100 Millisekunden an, während der Summer ertönt. Die zweite ``delay()``-Funktion pausiert das Arduino für 1000 Millisekunden (1 Sekunde), während der Summer stumm bleibt.

4. Nachdem du den Code auf das Arduino Uno R3 hochgeladen hast, wirst du hören, wie der Summer einmal pro Sekunde piept.

Coding Creation - ``millis()``
---------------------------------

Die Verwendung von ``delay()`` pausiert deinen Code, was manchmal unpraktisch sein kann.

Stell dir zum Beispiel vor, du erhitzt eine Pizza in der Mikrowelle und wartest auf wichtige E-Mails.
Du stellst die Pizza in die Mikrowelle und stellst den Timer auf 10 Minuten. Der Vergleich mit der Nutzung von ``delay()`` wäre, vor der Mikrowelle zu sitzen und zuzusehen, wie der Timer von 10 Minuten auf null herunterzählt. Falls du während dieser Zeit eine wichtige E-Mail erhältst, wirst du sie verpassen.

Normalerweise würdest du die Pizza in die Mikrowelle stellen, dann deine E-Mails checken und zwischendurch gelegentlich nachsehen, ob der Timer abgelaufen ist.

Arduino bietet auch eine Zeitfunktion, die das Programm nicht pausiert: ``millis()``.

``millis()`` ist eine sehr wichtige Funktion in der Arduino-Programmierung. Sie gibt die Anzahl der Millisekunden zurück, die seit dem Start des Arduino-Boards vergangen sind.

  * ``time = millis()``: Gibt die Anzahl der Millisekunden seit dem Start des Arduino-Boards oder dem letzten Reset zurück. Diese Zahl läuft nach etwa 50 Tagen über (zurück auf null).

  **Parameter**
    Keine

  **Rückgabewert**
    Anzahl der seit dem Programmstart vergangenen Millisekunden. Datentyp: unsigned long.


Hier lassen wir den Summer ebenfalls einmal pro Sekunde ertönen.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „New Sketch“ aus dem Menü „Datei“ auswählst.
2. Speichere deinen Sketch als ``Lesson24_Timer_Millis`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Erstelle zunächst eine Konstante namens ``buzzerPin`` und setze sie auf Pin 9.

.. code-block:: Arduino
  :emphasize-lines: 1

  const int buzzerPin = 9;   // Weist die Konstante für den Summer dem Pin 9 zu

  void setup() {
    // Initialisierungscode, der einmal ausgeführt wird:
  }

4. Erstelle zwei Variablen vom Typ „long“: ``previousMillis`` speichert den Zeitstempel des letzten Pieptons und ``interval`` legt fest, wie oft der Summer piept, in Millisekunden. Hier soll der Summer alle 1000 Millisekunden (oder jede Sekunde) ertönen.

.. code-block:: Arduino
  :emphasize-lines: 3,4

  const int buzzerPin = 9;  // Weist die Konstante für den Summer dem Pin 9 zu

  unsigned long previousMillis = 0;  // Speichert den Zeitstempel des letzten Pieptons
  long interval = 1000;              // Intervall für das Piepen (Millisekunden)



5. Setze in der ``void setup()``-Funktion den Summer-Pin auf den Ausgangsmodus.

.. code-block:: Arduino
  :emphasize-lines: 8

  const int buzzerPin = 9;  // Weist die Konstante für den Summer dem Pin 9 zu

  unsigned long previousMillis = 0;  // Speichert den Zeitstempel des letzten Pieptons
  long interval = 1000;              // Intervall für das Piepen (Millisekunden)

  void setup() {
    // Initialisierungscode, der einmal ausgeführt wird:
    pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 auf Ausgang
  }

6. Erstelle in der Funktion ``void loop()`` eine Variable vom Typ ``unsigned long`` namens ``currentMillis``, um die aktuelle Zeit zu speichern.

.. code-block:: Arduino
  :emphasize-lines: 3

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    unsigned long currentMillis = millis();
  }

7. Wenn die aktuelle Laufzeit abzüglich der letzten Aktualisierungszeit 1000ms überschreitet, löse einige Funktionen aus. Aktualisiere auch ``previousMillis`` auf die aktuelle Zeit, damit der nächste Auslöser nach 1 Sekunde erfolgt.

.. code-block:: Arduino
  :emphasize-lines: 5,6

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Speichert die letzte Zeit, als der Summer ertönte
    }
  }

8. Füge die Hauptfunktionen hinzu, die periodisch ausgeführt werden sollen. In diesem Fall soll der Summer ertönen.

.. code-block:: Arduino
  :emphasize-lines: 7,8,9

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Speichert die letzte Zeit, als der Summer ertönte
      digitalWrite(buzzerPin, HIGH);   // Lasse den Summer ertönen
      delay(100);
      digitalWrite(buzzerPin, LOW);  // Stille
    }
  }

9. Dein vollständiger Code sollte so aussehen. Lade ihn auf das Arduino Uno R3 hoch, und du wirst feststellen, dass der Summer einmal pro Sekunde ertönt.

.. code-block:: Arduino

  const int buzzerPin = 9;  // Weist die Konstante für den Summer dem Pin 9 zu

  unsigned long previousMillis = 0;  // Speichert den Zeitstempel des letzten Pieptons
  long interval = 1000;              // Intervall für das Piepen (Millisekunden)

  void setup() {
    // Initialisierungscode, der einmal ausgeführt wird:
    pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 auf Ausgang
  }

  void loop() {
    // Hauptcode, der wiederholt ausgeführt wird:
    unsigned long currentMillis = millis();

    if (currentMillis - previousMillis >= interval) {
      previousMillis = currentMillis;  // Speichert die letzte Zeit, als der Summer ertönte
      digitalWrite(buzzerPin, HIGH);   // Lasse den Summer ertönen
      delay(100);
      digitalWrite(buzzerPin, LOW);  // Stille
    }
  }

**Frage**

Was passiert, wenn ``delay(100);`` auf ``delay(1000);`` geändert wird? Warum?

Coding Creation - Pomodoro Timer
------------------------------------

Die Pomodoro-Technik, auch bekannt als Tomaten-Technik, ist eine Zeitmanagement-Methode, die in den späten 1980er Jahren von Francesco Cirillo entwickelt wurde.
Diese Methode verwendet einen Timer, um die Arbeit in 25-minütige Intervalle zu unterteilen, gefolgt von kurzen Pausen.
Jedes Arbeitsintervall wird als "Pomodoro" bezeichnet, benannt nach dem tomatenförmigen Küchentimer, den Cirillo während seiner Studienzeit verwendete.

.. image:: img/19_tomato_timer.jpg
  :width: 500
  :align: center

Die grundlegenden Schritte der Pomodoro-Technik umfassen:

1. **Definiere die Aufgabe**: Entscheide dich für die Aufgabe, die du vor dem Start erledigen möchtest.
2. **Stelle den Pomodoro-Timer**: Stelle einen Timer auf 25 Minuten Arbeitszeit ein.
3. **Arbeite intensiv**: Konzentriere dich voll auf die Aufgabe während dieser 25 Minuten und vermeide jede Form von Ablenkung.
4. **Mache eine kurze Pause**: Sobald die Arbeitszeit abgelaufen ist, mache eine 5-minütige Pause. In dieser Zeit kannst du dich bewegen, strecken, Wasser trinken usw., aber vermeide arbeitsbezogene Aktivitäten.

Die Vorteile der Pomodoro-Technik umfassen eine verbesserte Konzentration, reduzierte Ermüdung, klare Abgrenzung von Arbeits- und Pausenzeiten, die dabei helfen, Ablenkungen zu minimieren, sowie eine erhöhte Motivation und Zufriedenheit durch das Erreichen von Aufgaben. Außerdem erfordert die Pomodoro-Technik keine komplizierten Werkzeuge oder Technologien – ein einfacher Timer ist ausreichend.

Als Nächstes werden wir einen Timer programmieren, der alle 25 Minuten piept, um das Ende einer Arbeitsperiode anzuzeigen, gefolgt von einer Erinnerung an eine 5-minütige Pause:

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du „New Sketch“ aus dem Menü „Datei“ auswählst.
2. Speichere deinen Sketch als ``Lesson24_Timer_Millis_Pomodoro`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Definiere einige Konstanten und Variablen vor ``void setup()``.

* ``buzzerPin`` identifiziert, an welchem Pin der Summer angeschlossen ist.
* ``startMillis`` verfolgt, wann der Timer gestartet wurde.
* ``workPeriod`` und ``breakPeriod`` definieren, wie lange jede Periode dauert.
* ``isWorkPeriod`` ist eine boolesche Variable, die verwendet wird, um zu verfolgen, ob es Zeit zum Arbeiten oder für eine Pause ist.

.. code-block:: Arduino

  const int buzzerPin = 9;          // Weist die Konstante für den Summer dem Pin 9 zu
  unsigned long startMillis;        // Speichert die Startzeit des Timers
  const long workPeriod = 1500000;  // Arbeitsperiode von 25 Minuten
  const long breakPeriod = 300000;  // Pausenperiode von 5 Minuten
  static bool isWorkPeriod = true;  // Verfolgt, ob es eine Arbeits- oder Pausenperiode ist
  
4. Initialisiere den Summer-Pin als Ausgang und starte den Timer, indem du die Startzeit mit ``millis()`` speicherst.

.. code-block:: Arduino
  :emphasize-lines: 2,3
  
  void setup() {
    pinMode(buzzerPin, OUTPUT); // Initialisiere den Summer-Pin als Ausgang
    startMillis = millis(); // Speichere die Startzeit
  }

5. Erstelle in der Funktion ``void loop()`` eine Variable vom Typ ``unsigned long`` namens ``currentMillis``, um die aktuelle Zeit zu speichern.

.. code-block:: Arduino
  :emphasize-lines: 2

  void loop() {
    unsigned long currentMillis = millis(); // Aktualisiere die aktuelle Zeit
  }


6. Verwende ``if else if``-Bedingungsanweisungen, um festzustellen, ob es sich um eine Arbeitsperiode handelt.

.. code-block:: Arduino
  :emphasize-lines: 4-6

  void loop() {
    unsigned long currentMillis = millis(); // Aktualisiere die aktuelle Zeit

    if (isWorkPeriod){ 
    } else if (!isWorkPeriod){
    }
  }

7. Falls es eine Arbeitsperiode ist, prüfe, ob die aktuelle Zeit die ``workPeriod`` überschritten hat. Wenn ja, setze den Timer zurück, wechsle zur Pausenperiode und aktiviere den Summer, um zweimal für eine längere Dauer zu ertönen.

.. code-block:: Arduino
  :emphasize-lines: 5-16

  void loop() {
    unsigned long currentMillis = millis();  // Aktualisiere die aktuelle Zeit

    if (isWorkPeriod) {
      if (currentMillis - startMillis >= workPeriod) {
        startMillis = currentMillis;  // Setze den Timer zurück
        isWorkPeriod = false;         // Wechsle zur Pausenperiode
        digitalWrite(buzzerPin, HIGH);  // Schalte den Summer ein
        delay(500);                     // Summer an für 500 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Schalte den Summer aus
        delay(200);                     // Summer aus für 200 Millisekunden
        digitalWrite(buzzerPin, HIGH);  // Schalte den Summer ein
        delay(500);                     // Summer an für 500 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Schalte den Summer aus
        delay(200);                     // Summer aus für 200 Millisekunden
      }
    } else if (!isWorkPeriod) {
    }
  }


8. Verwende ``else if``-Bedingungsanweisungen, um festzustellen, ob es sich um eine Pausenperiode handelt, und prüfe ähnlich, ob die aktuelle Zeit die ``breakPeriod`` überschritten hat. Wenn ja, setze den Timer zurück, wechsle zurück zur Arbeitsperiode und aktiviere den Summer, um zweimal kurz zu ertönen.

.. code-block:: Arduino

  } else if (!isWorkPeriod) {
    if (currentMillis - startMillis >= breakPeriod) {
      startMillis = currentMillis;  // Setze den Timer zurück
      isWorkPeriod = true;          // Wechsle zur Arbeitsperiode
      digitalWrite(buzzerPin, HIGH);  // Schalte den Summer ein
      delay(200);                     // Summer an für 200 Millisekunden
      digitalWrite(buzzerPin, LOW);   // Schalte den Summer aus
      delay(200);                     // Summer aus für 200 Millisekunden
      digitalWrite(buzzerPin, HIGH);  // Schalte den Summer ein
      delay(200);                     // Summer an für 200 Millisekunden
      digitalWrite(buzzerPin, LOW);   // Schalte den Summer aus
      delay(200);                     // Summer aus für 200 Millisekunden
    }
  }


9. Dein vollständiger Code sollte so aussehen, und du kannst ihn auf das Arduino Uno R3 hochladen, um die Effekte zu sehen.

.. note::

  Wenn du das Warten auf eine 25-minütige Arbeitsperiode und eine 5-minütige Pause während des Debuggens zu lange findest, 
  kannst du die ``workPeriod`` auf 15000 Millisekunden und die ``breakPeriod`` auf 3000 Millisekunden verkürzen. Du wirst dann hören, wie der Summer alle 15 Sekunden zweimal lang ertönt, gefolgt von zweimal kurzem Piepen nach 3 Sekunden.


.. code-block:: Arduino

  const int buzzerPin = 9;          // Weist die Konstante für den Summer dem Pin 9 zu
  unsigned long startMillis;        // Speichert die Startzeit des Timers
  const long workPeriod = 1500000;  // Arbeitsperiode von 25 Minuten
  const long breakPeriod = 300000;  // Pausenperiode von 5 Minuten
  static bool isWorkPeriod = true;  // Verfolgt, ob es eine Arbeits- oder Pausenperiode ist

  void setup() {
    pinMode(buzzerPin, OUTPUT); // Initialisiere den Summer-Pin als Ausgang
    startMillis = millis(); // Speichere die Startzeit
  }

  void loop() {
    unsigned long currentMillis = millis(); // Aktualisiere die aktuelle Zeit

    if (isWorkPeriod){ 
      if(currentMillis - startMillis >= workPeriod) {
        startMillis = currentMillis; // Setze den Timer zurück
        isWorkPeriod = false; // Wechsle zur Pausenperiode
        digitalWrite(buzzerPin, HIGH);  // Schalte den Summer ein
        delay(500);                     // Summer an für 500 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Schalte den Summer aus
        delay(200);                     // Summer aus für 200 Millisekunden
        digitalWrite(buzzerPin, HIGH);  // Schalte den Summer ein
        delay(500);                     // Summer an für 500 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Schalte den Summer aus
        delay(200);                     // Summer aus für 200 Millisekunden
      }
    } else if (!isWorkPeriod) 
      if(currentMillis - startMillis >= breakPeriod) {
        startMillis = currentMillis; // Setze den Timer zurück
        isWorkPeriod = true; // Wechsle zur Arbeitsperiode
        digitalWrite(buzzerPin, HIGH);  // Schalte den Summer ein
        delay(200);                     // Summer an für 200 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Schalte den Summer aus
        delay(200);                     // Summer aus für 200 Millisekunden
        digitalWrite(buzzerPin, HIGH);  // Schalte den Summer ein
        delay(200);                     // Summer an für 200 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Schalte den Summer aus
        delay(200);                     // Summer aus für 200 Millisekunden
      }
    }
  }

10. Denke daran, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.

**Frage**

Denke über andere Situationen in deinem Leben nach, in denen du Zeit "hörst". Liste einige Beispiele auf und schreibe sie in dein Notizbuch!

**Zusammenfassung**

Im heutigen Kurs haben wir erfolgreich eine elektronische Version des Pomodoro-Timers gebaut, ein wertvolles Werkzeug zur Steigerung der Produktivität durch strukturierte Arbeits- und Pausenintervalle. Durch dieses Projekt haben die Schüler die Nützlichkeit von Summern im Zeitmanagement und die praktische Anwendung der ``millis()``-Funktion kennengelernt, um nicht blockierende Timer-Code in Arduino zu erstellen. Dieser Ansatz ermöglicht Multitasking in Mikrocontroller-Anwendungen und spiegelt komplexere Systeme in Technologie und Industrie wider.


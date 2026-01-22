.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauche mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum mitmachen?**

    - **Expertenunterstützung**: Löse Probleme nach dem Kauf und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tausche Tipps und Tutorials aus, um deine Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalte frühzeitigen Zugang zu neuen Produktankündigungen und Einblicken hinter die Kulissen.
    - **Spezielle Rabatte**: Genieße exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nimm an Verlosungen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicke auf [|link_sf_facebook|] und tritt noch heute bei!

.. _ar_morse_code:

10. Morsecode
========================

Morsecode ist wie eine Geheimsprache, die aus Punkten (.) und Strichen (-) besteht und in den 1840er Jahren von Samuel Morse erfunden wurde. Er wurde entwickelt, um Nachrichten über weite Entfernungen mit Hilfe von Telegrafen zu übermitteln. Jeder Buchstabe des Alphabets und jede Zahl wird durch eine einzigartige Kombination dieser Signale dargestellt. Zum Beispiel ist die berühmteste Morsecode-Nachricht "SOS" (··· ––– ···), das internationale Notsignal. Morsecode war vor der Erfindung des Telefons und des Internets für die Kommunikation unerlässlich und war besonders bei Schiffs- und Flugzeugbetreibern beliebt. Heute macht es Spaß, Morsecode zu lernen, um geheime Nachrichten an deine Freunde zu senden!

.. raw:: html

    <video controls style = "max-width:90%">
        <source src="_static/video/10_morse_code.mp4" type="video/mp4">
        Dein Browser unterstützt das Video-Tag nicht.
    </video>

In dieser Lektion wirst du lernen:

* Verstehe die Funktionsweise eines aktiven Buzzers.
* Lerne, das SOS-Signal im Morsecode zu codieren, damit du Nachrichten mit einem Buzzer in Morsecode senden kannst.


Morsecode-Magie!
-------------------

.. image:: img/7_morse.jpeg

Stell dir vor, du erfindest eine Möglichkeit, geheime Nachrichten nur mit Punkten und Strichen zu senden! Das ist es, was Samuel Morse 1836 mit dem Morsecode gemacht hat. Ursprünglich war Morse ein Maler, doch während einer Schiffsreise ließ er sich inspirieren und entwickelte später gemeinsam mit seinem Freund Alfred Vail den Telegrafen, um Nachrichten über Drähte zu senden.

Der Morsecode verwendet Punkte (kurze Signale) und Striche (lange Signale), um Buchstaben und Zahlen darzustellen. Die erste Morsecode-Nachricht? „What hath God wrought“ – gesendet 1844 von Washington D.C. nach Baltimore, was die Telegrafen-Ära einleitete.

Heutzutage wird der Morsecode nicht mehr so oft verwendet, aber er ist immer noch in Bereichen wie der Luftfahrt und unter Funkamateuren beliebt. Nun wollen wir erkunden, wie der Morsecode mit Arduino und einem Buzzer funktioniert und dabei Spaß mit diesem historischen Kommunikationsmittel haben!


Schaltkreis aufbauen
-----------------------

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Aktiver Buzzer
     - 1 * Breadboard
     - Jumper-Kabel
   * - |list_uno_r3| 
     - |list_active_buzzer| 
     - |list_breadboard| 
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

1. Finde einen aktiven Buzzer, der normalerweise einen weißen Aufkleber auf der Vorderseite und eine versiegelte schwarze Rückseite hat.

.. image:: img/7_beep_2.png

Buzzer, als elektronische Schallgeräte, haben eine reiche Geschichte, die bis ins 19. Jahrhundert zurückreicht. Der Vorläufer moderner Buzzer geht auf das Jahr 1831 zurück, als Michael Faraday die elektromagnetische Induktion entdeckte, die das grundlegende Prinzip für den Betrieb elektromagnetischer Buzzer bildet. Nach Faradays bahnbrechender Entdeckung untersuchten viele Wissenschaftler und Erfinder, wie elektromagnetische Theorien auf praktische Geräte angewendet werden könnten. Heutzutage werden Buzzer in aktive und passive unterteilt:

**Aktiver Buzzer**

.. image:: img/7_beep_ac.png
    :width: 300
    :align: center

Versiegelt auf der Rückseite, enthalten aktive Buzzer einen internen Oszillator, der beim Einschalten einen Ton erzeugt, typischerweise einen Ein-Ton-Piepton.

**Passiver Buzzer**

.. image:: img/7_beep_pa.png
    :width: 300
    :align: center

Mit offener Rückseite benötigen passive Buzzer ein externes Frequenzsignal von einem Mikrocontroller, um Töne zu erzeugen, was eine Reihe von Tonhöhen ermöglicht.

1. Ein aktiver Buzzer ist ebenfalls ein polares Bauteil. Die Vorderseite hat ein "+"-Zeichen, das seinen positiven Anschluss (Anode) anzeigt, der auch der längere Pin ist. Setze nun den Buzzer ins Breadboard, wobei die Anode in Loch 15F und die Kathode in Loch 18F gesteckt wird.

.. image:: img/16_morse_code_buzzer.png
    :width: 500
    :align: center

2. Verbinde die Kathode mit dem GND-Pin des Arduino Uno R3.

.. image:: img/16_morse_code_gnd.png
    :width: 500
    :align: center

3. Wenn du die Anode des Buzzers in den 5V-Pin des Arduino Uno R3 steckst, wirst du sofort einen Ton vom aktiven Buzzer hören. Natürlich kannst du diese Methode auch verwenden, um zu überprüfen, ob der Buzzer korrekt funktioniert. Ein passiver Buzzer wird keinen Ton erzeugen, wenn er direkt an eine Stromquelle angeschlossen wird.

.. image:: img/16_morse_code_5v.png
    :width: 500
    :align: center

4. Entferne nun das Kabel, das in den 5V-Pin gesteckt ist, und stecke es in Pin 9 des Arduino Uno R3, sodass der Buzzer per Code gesteuert werden kann.

.. image:: img/16_morse_code.png
    :width: 500
    :align: center


Codeerstellung - Den Buzzer ertönen lassen
-----------------------------------------------
1. Öffne die Arduino IDE und starte ein neues Projekt, indem du im Menü „Datei“ „Neue Skizze“ auswählst.
2. Speichere deine Skizze unter dem Namen ``Lesson10_Beep`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Erstelle zuerst eine Konstante namens ``buzzerPin`` und setze sie auf Pin 9.

.. code-block:: Arduino
    :emphasize-lines: 1

    const int buzzerPin = 9;   // Weist Pin 9 der Konstante für den Buzzer zu

    void setup() {
        // Setup-Code hier einfügen, der einmal ausgeführt wird:
    }

4. Initialisiere den Pin: Setze im ``void setup()``-Funktionsblock den Buzzer-Pin auf den Ausgabemodus.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int buzzerPin = 9;   // Weist Pin 9 der Konstante für den Buzzer zu

    void setup() {
        // Setup-Code hier einfügen, der einmal ausgeführt wird:
        pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 als Ausgang
    }

5. Einen aktiven Buzzer zu ertönen zu bringen, ist genauso einfach wie das Einschalten einer LED; du musst nur ``digitalWrite()`` verwenden, um Pin 9 auf high oder low zu setzen, und ``delay()``, um das Timing zu steuern.

.. code-block:: Arduino
    :emphasize-lines: 10-13

    const int buzzerPin = 9;   // Weist Pin 9 der Konstante für den Buzzer zu

    void setup() {
        // Setup-Code hier einfügen, der einmal ausgeführt wird:
        pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 als Ausgang
    }

    void loop() {
        // Hauptcode hier einfügen, der wiederholt ausgeführt wird:
        digitalWrite(buzzerPin, HIGH);  // Buzzer einschalten
        delay(250);                     // Piepdauer: 250 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Buzzer ausschalten
        delay(250);                     // Intervall zwischen Signalen: 250 Millisekunden
    }

6. Du kannst deinen Code auf das Arduino Uno R3 hochladen und dann den "Beep Beep"-Ton hören.

Codeerstellung - "SOS"
--------------------------
Nun wollen wir den Code schreiben, um den Buzzer Morsezeichen senden zu lassen.

Im Morsecode gibt es traditionelle Zeitregeln für Punkte (kurze Signale), Striche (lange Signale) und die Intervalle zwischen den Signalen, um sicherzustellen, dass die Nachricht korrekt empfangen und verstanden wird. Hier sind einige Grundregeln:

    * Länge eines Punktes: die Grundeinheit der Zeit.
    * Länge eines Striches: entspricht drei Punkten.
    * Intervall zwischen Punkten: die Länge eines Punktes.
    * Intervall innerhalb eines Zeichens (zwischen Punkten und Strichen eines Buchstabens oder einer Zahl): die Länge eines Punktes.
    * Intervall zwischen Zeichen (z. B. zwischen zwei Buchstaben): drei Punkte.
    * Intervall zwischen Wörtern (z. B. zwischen zwei Wörtern): sieben Punkte.

1. Öffne die Arduino IDE und starte ein neues Projekt, indem du im Menü „Datei“ „Neue Skizze“ auswählst.
2. Speichere deine Skizze unter dem Namen ``Lesson10_Morse_Code`` mit ``Strg + S`` oder durch Klicken auf „Speichern“.

3. Zuerst initialisiere den Pin, der mit dem Buzzer verbunden ist.

.. code-block:: Arduino
    :emphasize-lines: 5

    const int buzzerPin = 9;   // Weist Pin 9 der Konstante für den Buzzer zu

    void setup() {
        // Setup-Code hier einfügen, der einmal ausgeführt wird:
        pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 als Ausgang
    }

4. Nun erstellen wir eine Funktion zum Aussenden von Punkten (kurze Signale). Im Laufe deiner Programmierreise hast du bereits die integrierten Arduino-Funktionen wie ``pinMode()``, ``digitalWrite()`` und ``delay()`` verwendet. Jetzt tauchen wir in die Erstellung benutzerdefinierter Funktionen ein. Benutzerdefinierte Funktionen ermöglichen es dir, deinen Code zu vereinfachen, was ihn logischer und übersichtlicher macht.

Um eine Funktion zu erstellen, füge sie einfach am Ende deiner Skizze nach der geschweiften Klammer von ``void loop()`` hinzu. Wie bei ``void setup()`` und ``void loop()`` beginnen Funktionen mit dem Schlüsselwort void, gefolgt von einem Namen, den du wählst. Die Namensregeln für Funktionen ähneln denen für Variablen oder Konstanten. Du kannst einer Funktion jeden Namen geben, der kein Schlüsselwort in der Arduino-IDE ist, und ihre Befehle innerhalb geschweifter Klammern einschließen.

.. code-block:: Arduino
    :emphasize-lines: 9,10

    void loop() {
        // Hauptcode hier einfügen, der wiederholt ausgeführt wird:
        digitalWrite(buzzerPin, HIGH);  // Buzzer einschalten
        delay(250);                     // Piepdauer: 250 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Buzzer ausschalten
        delay(250);                     // Intervall zwischen Signalen: 250 Millisekunden
    }

    void dot() {
    }

5. In der erstellten Funktion ``void dot()``, lege das Zeitintervall für einen Punkt auf 250 ms fest.

.. code-block:: Arduino
    :emphasize-lines: 9-14

    void loop() {
        // Hauptcode hier einfügen, der wiederholt ausgeführt wird:
        digitalWrite(buzzerPin, HIGH);  // Buzzer einschalten
        delay(250);                     // Piepdauer: 250 Millisekunden
        digitalWrite(buzzerPin, LOW);   // Buzzer ausschalten
        delay(250);                     // Intervall zwischen Signalen: 250 Millisekunden
    }

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Kurze Dauer für einen Punkt
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervall zwischen Signalen
    }

6. Erstelle nun eine weitere Funktion zum Aussenden von Strichen (lange Signale). Laut den Grundregeln des Morse-Codes setze das Zeitintervall für einen Strich auf das Dreifache eines Punktes (750 ms).

.. code-block:: Arduino
    :emphasize-lines: 8-13

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Kurze Dauer für einen Punkt
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervall zwischen Signalen
    }

    void dash() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Längere Dauer für einen Strich
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervall zwischen Signalen
    }

7. Nun kannst du Morsecode senden. Um beispielsweise "SOS" (... --- ...) zu senden, besteht der Morsecode für 'S' aus drei Punkten und für 'O' aus drei Strichen, sodass du einfach die Punkt- und Strichfunktionen jeweils dreimal aufrufst.

.. code-block:: Arduino
    :emphasize-lines: 2-11

    void loop() {
        dot();
        dot();
        dot();  // S: ...
        dash();
        dash();
        dash();  // O: ---
        dot();
        dot();
        dot();       // S: ...
        delay(750);  // Nach einer Pause wiederholen
    }

8. Hier ist dein vollständiger Code. Du kannst jetzt auf „Upload“ klicken, um den Code auf das Arduino Uno R3 hochzuladen, und danach hörst du den Morsecode für „SOS“ (... --- ...).

.. code-block:: Arduino

    const int buzzerPin = 9;   // Weist Pin 9 der Konstante für den Buzzer zu
    
    void setup() {
        // Setup-Code hier einfügen, der einmal ausgeführt wird:
        pinMode(buzzerPin, OUTPUT);  // Setzt Pin 9 als Ausgang
    }

    void loop() {
        dot();
        dot();
        dot();  // S: ...
        dash();
        dash();
        dash();  // O: ---
        dot();
        dot();
        dot();       // S: ...
        delay(750);  // Nach einer Pause wiederholen
    }

    void dot() {
        digitalWrite(buzzerPin, HIGH);
        delay(250);  // Kurze Dauer für einen Punkt
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervall zwischen Signalen
    }

    void dash() {
        digitalWrite(buzzerPin, HIGH);
        delay(750);  // Längere Dauer für einen Strich
        digitalWrite(buzzerPin, LOW);
        delay(250);  // Intervall zwischen Signalen
    }

9. Denke daran, deinen Code zu speichern und deinen Arbeitsplatz aufzuräumen.


**Zusammenfassung**

In dieser Lektion hast du die Grundlagen des Morse-Codes erforscht, eine einzigartige Kommunikationsform, die in den 1840er Jahren von Samuel Morse entwickelt wurde. Du hast gelernt, wie man einen aktiven Buzzer verwendet, um den Morse-Code für SOS, ein international anerkanntes Notsignal, zu senden. Diese Lektion vermittelte dir nicht nur die Einrichtung und Programmierung eines aktiven Buzzers, sondern auch einen Einblick in die historische Bedeutung des Morse-Codes in der Telekommunikation. Mit diesen Fähigkeiten kannst du nun geheime Morse-Botschaften an Freunde senden oder dessen Anwendungen in modernen Geräten weiter erkunden.

In dieser Lektion haben wir nur die Morse-Codes für die Buchstaben "S" und "O" verwendet. Hier ist die Tabelle des Morse-Codes für die 26 Buchstaben und 10 Ziffern.

.. list-table::
    :widths: 8 8 8 8 8 8 8 8
    :header-rows: 1

    * - Buchstabe
      - Code
      - Buchstabe
      - Code
      - Buchstabe
      - Code
      - Buchstabe
      - Code
    * - A
      - \.-
      - B
      - \-...
      - C
      - \-.\-.
      - D
      - \-..
    * - E
      - \.
      - F
      - \..-.
      - G
      - \-\-.
      - H
      - \....
    * - I
      - \..
      - J
      - \.\-\-\-
      - K
      - \-.-
      - L
      - \.-..
    * - M
      - \--
      - N
      - \-.
      - O
      - \-\-\-
      - P
      - \.-\-.
    * - Q
      - \-\-.-
      - R
      - \.-.
      - S
      - \...
      - T
      - \-
    * - U
      - \..-
      - V
      - \...-
      - W
      - \.-\-
      - X
      - \-..-
    * - Y
      - \-.-\-
      - Z
      - \-\-..
      - 1
      - \.\-\-\-\-
      - 2
      - \..\-\-\-
    * - 3
      - \...-\-
      - 4
      - \....-
      - 5
      - \.....
      - 6
      - \-....
    * - 7
      - \-\-...
      - 8
      - \-\-\-..
      - 9
      - \-\-\-\-.
      -
      -

**Frage**

Verwende die bereitgestellte Morse-Code-Tabelle und schreibe einen Code, um die Nachricht "Hello" zu senden.


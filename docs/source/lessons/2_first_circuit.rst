.. note::

    Hallo und herzlich willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Community auf Facebook! Tauchen Sie gemeinsam mit anderen Enthusiasten tiefer in die Welt von Raspberry Pi, Arduino und ESP32 ein.

    **Warum beitreten?**

    - **Expertenunterstützung**: Lösen Sie nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Tutorials aus, um Ihre Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und ersten Einblicken.
    - **Spezielle Rabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Verlosungen**: Nehmen Sie an Verlosungen und Sonderaktionen während der Feiertage teil.

    👉 Bereit, mit uns zu entdecken und zu kreieren? Klicken Sie auf [|link_sf_facebook|] und treten Sie noch heute bei!

.. _2_first_circuit:

2. Ihr erstes Schaltkreis
============================

Willkommen in der spannenden Welt Ihres ersten Schaltkreises, in der ein einfacher Schalter Ihre Umgebung erhellen kann und ein Klick Geräte zum Leben erweckt. Diese Lektion ist Ihr Tor zum Verständnis der unsichtbaren Kraft des Stroms, der die Geräte antreibt, die wir täglich nutzen. Haben Sie sich schon einmal gefragt, wie Ihre Lieblingsgeräte funktionieren oder was die Lichter zum Leuchten bringt? Es ist an der Zeit, eine praktische Erkundung des Schaltkreisbaus zu beginnen.

Zu Beginn dieses Abenteuers erkunden wir die Ursprünge des elektrischen Stroms und verfolgen den Weg der Elektronen, während sie durch Schaltkreise fließen. Diese Lektion dient als praktische Einführung in die Komponenten eines Schaltkreises und deren Zusammenspiel zur Ausführung verschiedener Funktionen. Sie übernehmen auch die Rolle eines elektrischen Detektivs und entdecken, wie Sie diese lebhafte Kraft effektiv nutzen und messen können.

Machen Sie sich bereit für einige spannende Experimente! Folgendes werden Sie erreichen:

* Verwenden Sie ein Breadboard für den einfachen Bau von Schaltkreisen.
* Lesen Sie Widerstandsfarbcodes, um den Stromfluss zu steuern.
* Verstehen Sie, wie LEDs den Stromfluss steuern.
* Lernen Sie die Spannungsversorgung von Arduino Uno R3 kennen.
* Entdecken Sie, wie Elektronen durch einen Schaltkreis fließen.
* Erkennen Sie verschiedene Arten von Schaltkreisen und deren Funktionen.

Sind Sie bereit, in Ihre erste Schaltkreisbauerfahrung einzutauchen? Lassen Sie uns aufladen und diese erhellende Reise beginnen!

Benötigte Komponenten
--------------------------

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 1 * Rote LED
     - 1 * 220Ω Widerstand
     - Jumperkabel
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * USB-Kabel
     - 1 * Breadboard
     -
     -   
   * - |list_usb_cable| 
     - |list_breadboard| 
     -
     - 

Breadboard
-------------

1. Nehmen Sie Ihr Breadboard zur Hand.

Das Breadboard, das Sie verwenden werden, wird als lötfreies Breadboard bezeichnet. Jedes Loch im Breadboard enthält einen Metallkontakt, der den Draht beim Einsetzen festhält. Dies verhindert, dass der Draht herausgezogen wird, und sorgt für eine sichere Verbindung in Ihrem Schaltkreis.

.. image:: img/2_breadboard_half.png
    :width: 500
    :align: center

Haben Sie sich jemals gefragt, warum das essentielle elektronische Werkzeug in Ihrer Hand denselben Namen trägt wie das Küchenbrett zum Schneiden von Brot? Es ist eine interessante Geschichte! In den Tagen vor den 1970er Jahren wurden elektronische Bauteile auf echten Holzplatten montiert, manchmal sogar auf umfunktionierten Küchenbrettern, indem die Komponenten darauf genagelt oder geklebt und mit Drähten verbunden wurden.

.. image:: img/2_breadboard_circuit.jpg
    :width: 500
    :align: center

Von den 1960er bis zu den 1980er Jahren experimentierten Ingenieure mit dem sogenannten Wire-Wrapping für komplexere Schaltungen. Diese Methode war semipermanent und erforderte spezielle Werkzeuge, erwies sich jedoch letztendlich als zu umständlich und ungeeignet für wiederholte Verwendung.

.. image:: img/2_breadboard_wire_wrap.jpg
    :width: 500
    :align: center

Dann, Anfang der 1970er Jahre, revolutionierte Ronald J. Portugal das Prototyping mit der Erfindung des "lötfreien Breadboards", wodurch der Zusammenbau von Schaltkreisen schneller und einfacher wurde, ohne dass gelötet werden musste. Dieses innovative Werkzeug übertraf schnell das Wire-Wrapping und führte zu den Breadboards, die wir heute kennen und die nach ihren historischen Vorgängern benannt sind, aber für den modernen Maker entwickelt wurden.

.. image:: img/2_breadboard_full+.png
    :width: 500
    :align: center

Neugierig, was sich unter der Oberfläche eines Breadboards verbirgt? Hinter seiner Kunststoffverkleidung und einer Schicht aus klebrigem Schaum, die von gelbem Schutzpapier bedeckt ist, liegt das Herzstück der Funktionalität des Breadboards: Dutzende von Metallstreifen.

.. note::
    Es ist besser, diese Schutzschicht nicht zu entfernen. Wir haben es hier nur getan, um Ihnen zu zeigen, was sich darunter befindet.

.. image:: img/2_breadboard_internal0.jpg
    :width: 500
    :align: center

Wenn Sie (was wir dringend nicht empfehlen) diese Metallteile mit einer Zange herausziehen würden, würden Sie feststellen, dass jedes Stück ein Metallclip mit kleinen Zähnen ist. Jeder Streifen hat fünf Zähne, die den fünf Löchern auf der Oberfläche des Breadboards in jeder Reihe entsprechen. Die Stromschienen haben längere Streifen mit fünfzig Zähnen.

.. image:: img/2_breadboard_internal1.jpg
    :width: 500
    :align: center

Diese winzigen Zähne sind perfekt dafür geeignet, die Beinchen von elektronischen Komponenten zu greifen. Wenn eine Komponente in das Breadboard eingesetzt wird, öffnet sich der Clip leicht, um das Metallbeinchen fest zu greifen. Jede andere Komponente, die in dieselbe Zahnreihe eingesetzt wird, ist elektrisch verbunden.

.. image:: img/2_breadboard_internal2.jpg
    :width: 500
    :align: center

Dieses clevere Design ermöglicht ein einfaches und flexibles Prototyping ohne Löten und macht Breadboards zu einem unverzichtbaren Werkzeug für Elektronikbegeisterte und Profis gleichermaßen.

Die meisten Breadboards haben einige Nummern, Buchstaben sowie Plus- und Minussymbole darauf. Obwohl die Bezeichnungen von Breadboard zu Breadboard unterschiedlich sein können, bleibt die Funktion im Wesentlichen dieselbe. Diese Beschriftungen helfen Ihnen dabei, die entsprechenden Löcher beim Bau Ihres Schaltkreises schneller zu finden. Die Reihennummern und Spaltenbuchstaben helfen Ihnen, die Löcher auf dem Breadboard genau zu lokalisieren, z. B. ist das Loch "C15" der Schnittpunkt der Spalte C mit der Reihe 15.

.. image:: img/2_breadboard_letter_number.jpg
    :width: 500
    :align: center

Die Seiten des Breadboards sind in der Regel durch rote und blaue (oder andere) Farben sowie durch Plus- und Minussymbole gekennzeichnet und werden üblicherweise zur Verbindung mit der Stromversorgung, dem sogenannten Power-Bus, verwendet. Beim Bau eines Schaltkreises ist es üblich, den Minuspol mit der blauen (-) Spalte und den Pluspol mit der roten (+) Spalte zu verbinden.

.. image:: img/2_breadboard_plus_minus.jpg
    :width: 500
    :align: center



Widerstand
---------------------

2. Suchen Sie einen 220-Ohm-Widerstand.

.. image:: img/2_220_resistor.png
    :align: center

Widerstände helfen, den Stromfluss in einem Schaltkreis zu steuern, indem sie elektrische Energie in Wärme umwandeln. Jeder Widerstand hat zwei Drähte, einen an jedem Ende, die es ermöglichen, dass Strom in beide Richtungen fließen kann, was bedeutet, dass sie in beliebiger Richtung im Schaltkreis platziert werden können.

Der Ohmwert eines Widerstands gibt an, wie viel Widerstand er hinzufügt. Ein höherer Ohmwert bedeutet mehr Widerstand. Beispielsweise fügt ein 220-Ohm-Widerstand 220 Ohm Widerstand hinzu, und ein 10-Kiloohm-Widerstand fügt 10 Kiloohm hinzu.

Um den Wert eines Widerstands zu lesen, überprüfen Sie die Farbbänder. Diese Tabelle erklärt die Bedeutung jedes Farbbands auf einem Widerstand. Der Multiplikator wird in wissenschaftlicher Notation dargestellt, wobei der Exponent die Anzahl der Nullen angibt, die zu der durch die Farbbänder dargestellten Zahl hinzugefügt werden. Zum Beispiel beginnt ein 4-Band-Widerstand oben in der Tabelle mit einem grünen Band. Grün steht für die Zahl 5, also beginnt der Widerstandswert mit 5. Das zweite Band ist braun, daher ist die nächste Zahl 1. Das Multiplikatorband ist rot und hat den Wert 2, was bedeutet, dass wir zwei Nullen hinzufügen. Dies ergibt einen Gesamtwiderstand von 5100 Ohm oder 5,1 Kiloohm (5,1 kΩ).

.. image:: img/2_resistor_card.png

Die hier gezeigte Tabelle stellt alle Widerstände dar, die in Ihrem Kit enthalten sind. Für diese Lektion verwenden wir einen 220-Ohm-Widerstand.

.. image:: img/2_all_resistor.png
    :width: 500
    :align: center

3. Biegen Sie die Beinchen des Widerstands so, dass sie in dieselbe Richtung zeigen.

.. image:: img/2_220_resistor_pin.png
    :width: 200
    :align: center

4. Stecken Sie ein Beinchen in das obere Loch auf der negativen Seite des Breadboards, um den Widerstand mit der Stromquelle zu verbinden. Stecken Sie das andere Beinchen des 220-Ohm-Widerstands in das Loch 1b des Breadboards.

    .. note::
        
        Widerstände gelten als unpolarisierte Bauelemente, was bedeutet, dass die Richtung, in der sie im Schaltkreis angeordnet sind, keine Rolle spielt.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center


LED
-----------------

5. Finden Sie die rote LED.

.. image:: img/2_red_led.png
    :align: center

LEDs, oder Licht emittierende Dioden, sind spezielle elektronische Komponenten, die Licht abgeben, wenn Strom in einer bestimmten Richtung durch sie fließt.

.. image:: img/2_led_polarity.jpg
    :width: 200
    :align: center

Die gängigsten LED-Farben sind Rot, Gelb, Blau, Grün und Weiß, wobei das abgegebene Licht in der Regel der Farbe der LED selbst entspricht.

.. image:: img/2_led_color.png
    :width: 600
    :align: center

Diese Bauelemente sind mit zwei Beinchen ausgestattet: einem längeren, dem sogenannten Anode, und einem kürzeren, dem sogenannten Kathode. Damit sie ordnungsgemäß funktionieren, sollte die Anode mit dem Pluspol der Stromquelle verbunden werden, und die Kathode sollte mit dem Minuspol oder der Masse verbunden werden. Einige LEDs haben eine flache Kante auf der Seite der Kathode, um die richtige Platzierung zu erleichtern.

.. image:: img/2_led_pin.jpg
    :width: 100
    :align: center


6. Stecken Sie die Kathode der LED (das kurze Beinchen) in das Loch 1e auf dem Breadboard. Dies verbindet die LED mit dem 220Ω Widerstand. Denken Sie daran, dass die Löcher 1b und 1e unter dem Breadboard verbunden sind.

.. note::

        LEDs gelten als polarisierte Bauelemente, was bedeutet, dass Strom nur in einer Richtung durch sie fließen kann. Wenn die LED nicht aufleuchtet, versuchen Sie, die Verbindungen zu vertauschen.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center


Jumperkabel
----------------------

7. Finden Sie ein Jumperkabel.

Ihr Kit enthält Jumperkabel in verschiedenen Farben und Längen, die alle gleich funktionieren. Verwenden Sie verschiedene Farben zur einfachen Identifizierung des Schaltkreises und kürzere Kabel für eine ordentliche Anordnung. Jedes Kabel besteht aus einem leitenden Kern und einer isolierenden Beschichtung, um unbeabsichtigte Kontakte zu verhindern.

.. image:: img/2_wire_color.jpg
    :width: 500
    :align: center

8. Stecken Sie ein Ende des Jumperkabels in das Loch 1j auf dem Breadboard. Dies verbindet das Jumperkabel mit der LED, da die Löcher 1f und 1j unter dem Breadboard verbunden sind. Stecken Sie das andere Ende des Jumperkabels in das obere Loch der positiven Schiene des Breadboards. Jetzt verbindet das Jumperkabel die LED und das Massekabel miteinander.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

Arduino Uno R3
------------------

9. Finden Sie Ihr Arduino Uno R3.

.. image:: img/1_uno_board.png
    :width: 400
    :align: center

In dieser Lektion verwenden wir das Arduino Uno R3 als Stromversorgung. Sein 5V-Pin dient als Pluspol und der GND-Pin als Minuspol, wodurch ein stabiler 5V-Strom an den Schaltkreis geliefert wird.

.. image:: img/1_uno_power_pin.png
    :width: 500
    :align: center

Wenn Sie jedoch die Anschlüsse der Stromversorgung direkt ohne Last verbinden, kann dies zu einem Kurzschluss führen, der Wärme erzeugt und möglicherweise Schäden oder Brände verursacht. Fügen Sie immer eine Last wie eine LED oder einen Widerstand hinzu, um Kurzschlüsse zu vermeiden.

.. image:: img/2_short_circuit.png
    :width: 500
    :align: center

10. Verbinden Sie ein Kabel von der positiven Schiene auf der rechten Seite des Breadboards mit dem 5V-Pin des Arduino Uno R3. Es wird empfohlen, ein rotes oder oranges Kabel zu verwenden, um den Pluspol darzustellen. Dies kann besonders hilfreich sein, um die Verbindungen in komplexeren Projekten schnell zu identifizieren.

.. image:: img/2_uno_5v.png
    :width: 600
    :align: center

11. Verbinden Sie schließlich ein Kabel von der negativen Schiene auf der linken Seite des Breadboards mit dem GND-Pin des Arduino Uno R3. Es wird empfohlen, für Konsistenz ein schwarzes oder grünes Kabel zu verwenden, um in allen Schaltkreisen dieselbe Farbe für den Minuspol zu verwenden.

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

12. Verbinden Sie abschließend das Arduino Uno R3 über das im Kit enthaltene USB-Kabel mit einem Computer oder einer Steckdose, und die LED sollte aufleuchten.

    .. image:: img/2_first_circuit.png
        :width: 600
        :align: center


Nachdem Sie Ihr Arduino Uno R3 angeschlossen und das Aufleuchten der LED beobachtet haben, sehen Sie nicht nur einen einfachen Schaltkreis – Sie erleben die Grundlagen der Elektrizität in Aktion. Lassen Sie uns untersuchen, was Ihren Schaltkreis zum Leben erweckt.


Elektrizität in Schaltkreisen verstehen
-------------------------------------------

**Die Grundlagen der Elektrizität**

Der Fluss von Elektronen vom Minuspol zum Pluspol ist das, was wir als tatsächlichen Elektronenfluss verstehen. Anfangs glaubten Wissenschaftler wie Ben Franklin, dass der Strom eine Bewegung positiver Ladungen sei, weshalb der konventionelle Stromfluss als von positiv nach negativ definiert ist.

.. image:: img/2_uno_current.png
    :width: 600
    :align: center

In Wirklichkeit bewegen sich jedoch Elektronen, die eine negative Ladung tragen, vom Minuspol zum Pluspol. In den meisten Ländern wird heute noch das Modell des konventionellen Stromflusses verwendet. Daher wird in Diagrammen und beim Design elektronischer Komponenten der Strom als von positiv nach negativ fließend dargestellt, obwohl sich die Elektronen tatsächlich in die entgegengesetzte Richtung bewegen.

.. image:: img/2_uno_electron.png
    :width: 600
    :align: center

* **A** Traditionelle Stromflussrichtung
* **B** Tatsächliche Elektronenflussrichtung
* **C** Elektronen (nicht maßstabsgetreu)
* **D** Draht

Es gibt zwei Arten von Strom, die von einer Stromquelle erzeugt werden: Wechselstrom (AC) und Gleichstrom (DC). Eine Batterie oder ein Mikrocontroller wie das Arduino Uno R3 liefert Gleichstrom, bei dem der Strom in eine Richtung fließt – vom Pluspol zum Minuspol.

Beim Wechselstrom hingegen ändert der Strom seine Richtung periodisch. Die Spannung im Schaltkreis kehrt sich um, wenn der Strom die Richtung ändert, wodurch er in die entgegengesetzte Richtung fließt. Die meisten Häuser und Gebäude werden von Wechselstromkreisen gespeist, wie z. B. die 120 Volt bei 60 Hz aus Steckdosen in amerikanischen Haushalten oder 220 Volt bei 50 Hz in vielen europäischen Haushalten.

**Sicherheit in Schaltkreisen**

Beim Anschluss einer Stromquelle ist es ratsam, zuerst den Pluspol mit dem Schaltkreis zu verbinden und dann den Minuspol. Beim Trennen sollten Sie umgekehrt vorgehen und zuerst den Minuspol entfernen, um Kurzschlüsse zu vermeiden. In diesem Kurs wird mit niedriger Spannung und Stromstärke gearbeitet, sodass keine Gefahr eines Stromschlags oder einer Verletzung besteht. Aber gute Sicherheitspraktiken können Schäden verhindern, wenn mit höheren Spannungen und Strömen gearbeitet wird, wie z. B. beim Wechseln von Autobatterien oder bei der Reparatur von Steckdosen.

**Geschlossene und offene Schaltkreise**

Wenn der Strom durch die LED, den Widerstand, die Jumperkabel und zurück in die negative Schiene des Breadboards fließt, bildet er einen sogenannten geschlossenen Stromkreis. Wenn Sie ein Kabel vom Breadboard entfernen, geht die LED aus, da der Stromfluss unterbrochen wurde – der Stromkreis ist jetzt offen.

.. image:: img/2_open_circuit.png
    :width: 600
    :align: center

Wenn Sie diese Grundlagen beherrschen, sind Sie auf dem besten Weg, komplexere elektronische Schaltungen zu verstehen und zu erstellen, die unsere Welt antreiben.


**Fragen:**

1. Entfernen Sie das rote Kabel vom Breadboard und experimentieren Sie, indem Sie es in verschiedene Löcher des Breadboards stecken. Beobachten Sie die Veränderungen an der LED. Skizzieren Sie die Positionen der Löcher, die die LED zum Leuchten bringen.

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

2. Was passiert, wenn Sie die Beinchen der LED vertauschen? Leuchtet sie auf? Warum oder warum nicht?


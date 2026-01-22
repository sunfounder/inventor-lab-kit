.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community auf Facebook! Tauchen Sie tiefer in die Welt von Raspberry Pi, Arduino und ESP32 mit Gleichgesinnten ein.

    **Warum mitmachen?**

    - **Expertenunterstützung**: Lösen Sie nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Tutorials aus, um Ihre Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und Vorschauen.
    - **Sonderrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu forschen und zu kreieren? Klicken Sie auf [|link_sf_facebook|] und treten Sie noch heute bei!


5. Reihenschaltung vs. Parallelschaltung
=================================================

In dieser Lektion bauen und analysieren Sie sowohl Reihen- als auch Parallelschaltungen, lernen, wie sich die Spannung in verschiedenen Schaltungsanordnungen verhält, und verwenden ein Multimeter, um die Spannung und den Widerstand der von Ihnen konstruierten Schaltungen zu messen. Sie erhalten praktische Einblicke in die Dynamik von Schaltungen.

In dieser spannenden Lektion lernen Sie:

* Schaltpläne mit realen Schaltungen zu verbinden.
* Ein Multimeter zur Messung von Widerstand und Spannung zu verwenden.
* Reihen- und Parallelschaltungen mit einem Steckbrett zu bauen.
* Das Verhalten der Spannung in Reihen- und Parallelschaltungen zu vergleichen.

Diese Ziele ermöglichen es Ihnen, die Lücke zwischen theoretischem Wissen und praktischer Anwendung zu schließen und Ihr Verständnis für Elektronik durch praktische Erfahrung zu vertiefen.


Reihenschaltung vs. Parallelschaltung
------------------------------------------

In unseren vorherigen Lektionen haben wir erfolgreich eine einfache Schaltung mit einem Arduino Uno R3, einem Widerstand und einer LED aufgebaut. Der Strom in dieser Anordnung fließt in einer Reihenschaltung: vom Pin 13 des Boards, durch die LED, durch den Widerstand und zurück zum GND-Pin. Dies ist ein einfaches Beispiel für eine Reihenschaltung.

Aber wenn wir tiefer in die Welt der Elektronik eintauchen, stoßen wir auf komplexere Schaltungen, die aus Komponenten bestehen, die in Reihe oder parallel angeordnet sind. Um diese Anordnungen und ihre Auswirkungen auf Strom und Spannung zu verstehen, müssen wir uns mit Schaltplänen, auch bekannt als Schemata, vertraut machen.

**Verdrahtungsdiagramme vs. Schaltpläne**

Wir haben bisher Verdrahtungsdiagramme verwendet – bildliche Darstellungen, die die physische Anordnung der Schaltungskomponenten nachahmen. Diese Diagramme sind intuitiv und eignen sich gut für Montagezwecke:

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

Um jedoch die Funktionalität und die logische Gestaltung einer Schaltung zu verstehen, sind Schaltpläne unerlässlich. Schaltpläne destillieren Schaltungen auf ihre Essenz und verwenden standardisierte Symbole, um jede Komponente darzustellen. Sie zeigen die elektrischen Verbindungen zwischen den Komponenten, ohne das Durcheinander der physischen Anordnung.

Hier sind die Symbole für eine LED, einen Widerstand und eine Batterie, die Sie häufig in Schaltplänen finden werden:

.. image:: img/5_led_resistor_symbol.png
  :align: center

Ein Schaltplan, der auf unserer vorherigen Verdrahtung basiert, würde so aussehen, wobei das gesamte Arduino Uno R3 als Batterie fungiert, die die Schaltung mit Strom versorgt. Anhand dieses Schaltplans können Sie den Stromfluss und die Stromrichtung klar erkennen, was die Komplexität der physischen Verbindungen vereinfacht.

.. image:: img/5_serial_circuit_1led.png
  :align: center

**Reihen- vs. Parallelkonfigurationen**

In einer Reihenschaltung sind die Komponenten hintereinander angeordnet, sodass der Strom nur einen Weg hat, dem er folgen kann. Wenn eine Komponente ausfällt, wird der gesamte Stromkreis unterbrochen – ähnlich wie bei einer alten Lichterkette, bei der eine durchgebrannte Glühbirne die gesamte Kette dunkel werden ließ.

.. image:: img/5_serial_circuit_2led.png
  :align: center

Eine Parallelschaltung hingegen teilt den Strom auf mehrere Wege auf. Jede Komponente arbeitet unabhängig, sodass, wenn ein Weg unterbrochen wird, die anderen weiterhin funktionieren. Denken Sie an das elektrische System Ihres Hauses: Wenn Sie eine Lampe ausschalten, kann der Fernseher trotzdem weiterlaufen.

.. image:: img/5_parallel_circuit.png
  :align: center


In die Reihenschaltung eintauchen
----------------------------------------

Aufbauend auf unserem Verständnis der Unterschiede zwischen Reihen- und Parallelschaltungen konzentriert sich diese Aktivität darauf, eine Reihenschaltung mit mehreren LEDs zu konstruieren. Denken Sie daran, dass in einer Reihenschaltung der elektrische Strom durch einen einzigen Pfad fließt. Lassen Sie uns die einzigartigen Eigenschaften von Reihenschaltungen durch diese praktische Übung erkunden.

**Benötigte Komponenten**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 3 * Rote LEDs
     - 3 * 220Ω Widerstände
     - Jumperkabel
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * USB-Kabel
     - 1 * Steckbrett
     - 1 * Multimeter
     -   
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter|
     - 

**Die Schaltung bauen**

1. Passen Sie die vorherige LED-Schaltung an, indem Sie das Jumperkabel zwischen 1J und der positiven Seite des Steckbretts auf der rechten Seite entfernen. Nehmen Sie dann eine weitere rote LED und stecken Sie ihre Kathode (das kürzere Bein) in 1J und die Anode in die positive Seite des Steckbretts, sodass Sie eine weitere LED in die Schaltung seriell einfügen.

.. image:: img/5_serial_circuit.png

Jetzt haben Sie eine Reihenschaltung mit zwei LEDs. Verfolgen Sie den Stromfluss durch die Schaltung:

* Der Strom fließt von 5V auf dem Arduino Uno R3 über ein langes Jumperkabel zum positiven Anschluss des Steckbretts.
* Dann fließt der Strom durch die erste LED, die aufgrund des Stromflusses aufleuchtet.
* Der Strom fließt dann durch die Metallklammern des Steckbretts zur zweiten LED, die ebenfalls aufleuchtet.
* Nachdem der Strom die zweite LED passiert hat, gelangt er in den 220Ω-Widerstand, wo er auf Widerstand trifft, der die Stromstärke reduziert. Ohne diesen Widerstand wäre der Strom durch die LEDs zu hoch und könnte sie zerstören.
* Schließlich fließt der Strom zurück zum GND-Pin des Arduino Uno R3 und schließt damit den Stromkreis.

**Frage**

Was passiert in dieser Reihenschaltung, wenn Sie eine LED entfernen? Warum geschieht dies?

.. image:: img/5_serial_circuit_remove.png
    :width: 600
    :align: center


**Spannung messen**

1. Stellen Sie das Multimeter auf die Einstellung für 20 Volt DC.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Verwenden Sie das Multimeter, um die Spannung über dem Widerstand zu messen.

    .. note::
        
        Das Messen der Spannung an einer Komponente in einem Stromkreis bedeutet, die Spannung über dieser Komponente zu prüfen. Im Wesentlichen stellt die Spannung den Energiedifferenz zwischen zwei Punkten dar. Wenn Sie die Spannung an einer Komponente messen, messen Sie die Energiedifferenz von einer Seite zur anderen.

.. image:: img/5_serial_circuit_voltage_resistor.png
    :width: 600
    :align: center

3. Notieren Sie die Spannung über dem Widerstand, Spannungseinheit: Volt (V).

.. note::

    * Meine betrug 1,13V, tragen Sie Ihre Messung entsprechend ein.

    * Aufgrund von Verdrahtungsproblemen und der Instabilität Ihrer Hand kann die Spannung schwanken. Halten Sie Ihre Hand ruhig und beobachten Sie mehrmals, um einen stabilen Spannungswert zu erhalten.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Schaltung
     - Widerstandsspannung
     - LED1 Spannung
     - LED2 Spannung
     - Gesamtspannung 
   * - 2 LEDs
     - *≈1.13 Volt*
     - 
     - 
     - 

4. Messen Sie nun die Spannung über der LED 1 in der Schaltung.

.. image:: img/5_serial_circuit_voltage_led1.png
    :width: 600
    :align: center

5. Notieren Sie die Spannung über der LED 1 in der Tabelle.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Schaltung
     - Widerstandsspannung
     - LED1 Spannung
     - LED2 Spannung
     - Gesamtspannung 
   * - 2 LEDs
     - *≈1.13 Volt*
     - *≈1.92 Volt*
     - 
     - 

6. Messen Sie die Spannung über der LED 2 in der Schaltung.

.. image:: img/5_serial_circuit_voltage_led2.png
    :width: 600
    :align: center

7. Notieren Sie die Spannung über der LED 2 in der Tabelle.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Schaltung
     - Widerstandsspannung
     - LED1 Spannung
     - LED2 Spannung
     - Gesamtspannung 
   * - 2 LEDs
     - *≈1.13 Volt*
     - *≈1.92 Volt*
     - *≈1.92 Volt*
     - 

8. Messen Sie nun die Gesamtspannung in der Schaltung.

.. image:: img/5_serial_circuit_voltage.png
    :width: 600
    :align: center

9. Tragen Sie die gemessene Spannung in die Spalte Gesamtspannung der Tabelle ein.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Schaltung
     - Widerstandsspannung
     - LED1 Spannung
     - LED2 Spannung
     - Gesamtspannung 
   * - 2 LEDs
     - *≈1.13 Volt*
     - *≈1.92 Volt*
     - *≈1.92 Volt*
     - *≈4.97 Volt*


Durch unsere Messungen werden Sie Folgendes feststellen:

.. code-block::

  4,97 Volt ≈ 1,13 Volt + 1,92 Volt + 1,92 Volt

  Gesamtspannung = Widerstandsspannung + LED 1 Spannung + LED 2 Spannung

Sie können auch berechnen, ob Ihre Messergebnisse dieser Gleichung entsprechen.


.. note::
    
    Aufgrund der Stabilität der Verdrahtung oder geringfügiger Fertigungsunterschiede bei den LEDs und dem Widerstand muss die Summe der Spannung am Widerstand und den beiden LEDs möglicherweise nicht genau der gemessenen Gesamtspannung entsprechen. Dies ist auch in Ordnung, solange es sich innerhalb eines vernünftigen Bereichs bewegt.


Dies ist ein Merkmal einer Reihenschaltung, bei der die Gesamtspannung über den Stromkreis die Summe der Spannungen über jede Komponente darstellt.

**Strom messen**

Nachdem wir die Spannungseigenschaften von Reihenschaltungen verstanden haben, wollen wir nun den Stromfluss in der Schaltung mithilfe eines Multimeters untersuchen.

1. Stellen Sie das Multimeter auf die 20 Milliampere Position ein. Der Strom wird 20 mA nicht überschreiten, daher wurde diese Einstellung gewählt. Wenn Sie unsicher sind, beginnen Sie mit der 200-mA-Einstellung.

.. image:: img/multimeter_20a.png
  :width: 300
  :align: center

2. Um den Strom zu messen, muss das Multimeter in den Stromkreis integriert werden. Lassen Sie die Anode der LED in Loch 1F und verschieben Sie die Kathode (das kürzere Bein) von Loch 1E zu Loch 3E.

.. image:: img/5_serial_circuit_led1_current.png
    :width: 600
    :align: center

3. Messen Sie den Strom über der LED 1 in der Schaltung.

.. image:: img/5_serial_circuit_led1_current1.png
    :width: 600
    :align: center

4. Notieren Sie den gemessenen Strom in der Tabelle.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Schaltung
     - LED1 Strom
     - LED2 Strom
   * - 2 LEDs
     - *≈4,43 Milliampere*
     - 

5. Setzen Sie die Kathode der ersten LED wieder in ihre ursprüngliche Position und verschieben Sie die Kathode der zweiten LED (das kürzere Bein) von Loch 1J zu Loch 2J.

.. image:: img/5_serial_circuit_led2_current.png
    :width: 600
    :align: center

6. Messen Sie den Strom über der LED 2 in der Schaltung.

.. image:: img/5_serial_circuit_led2_current1.png
    :width: 600
    :align: center

7. Notieren Sie den gemessenen Strom in der Tabelle.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Schaltung
     - LED1 Strom
     - LED2 Strom
   * - 2 LEDs
     - *≈4,43 Milliampere*
     - *≈4,43 Milliampere*

Unsere Messungen haben ein grundlegendes Prinzip von Reihenschaltungen verdeutlicht: Der Strom, der durch jede Komponente fließt, ist identisch. Dieser gleichmäßige Fluss unterstreicht die Verbundenheit der Komponenten in einer Reihenschaltung, wobei die Unterbrechung des Stroms in einem Teil die gesamte Schaltung beeinträchtigt.

Die Untersuchung von Spannung, Strom und Widerstand bereichert nicht nur unser Verständnis von Reihenschaltungen, sondern legt auch den Grundstein für komplexere Konzepte der Elektrotechnik. Durch diese praktischen Experimente überbrücken wir die Kluft zwischen Theorie und praktischer Anwendung und machen den Lernprozess sowohl ansprechend als auch informativ.

**Frage**

Wenn eine weitere LED zu dieser Schaltung hinzugefügt wird, sodass drei LEDs vorhanden sind, wie ändert sich die Helligkeit der LEDs? Warum? Wie verändern sich die Spannungen über die drei LEDs?



Eintauchen in Parallelschaltungen
---------------------------------------

**Benötigte Komponenten**

* 1 * Arduino Uno R3
* 3 * Rote LEDs
* 3 * 220Ω Widerstände
* Mehrere Jumperkabel
* 1 * USB-Kabel
* 1 * Steckbrett
* 1 * Multimeter mit Messleitungen

**Die Schaltung bauen**

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center
  
1. Schließen Sie einen 220Ω Widerstand an das Steckbrett an. Ein Ende sollte im negativen Anschluss sein, das andere Ende in Loch 1B.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

2. Fügen Sie eine rote LED zum Steckbrett hinzu. Die Anode der LED (langes Bein) sollte in Loch 1F sein. Die Kathode (kurzes Bein) sollte in Loch 1E sein.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

3. Verwenden Sie ein kurzes Jumperkabel, um die LED und die Stromquelle zu verbinden. Ein Ende des Jumperkabels sollte in Loch 1J sein, das andere Ende im positiven Anschluss.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

4. Verbinden Sie das lange Jumperkabel, das mit dem positiven Anschluss des Steckbretts verbunden ist, mit dem 5V-Pin auf dem Arduino Uno R3. Die LED sollte sich einschalten und anbleiben. Der 5V-Pin liefert eine konstante Gleichspannung von 5 Volt an die Schaltung. Dies unterscheidet sich vom Pin 13, der über die Arduino IDE-Software programmiert werden kann, um ein- und auszuschalten.

.. image:: img/5_parallel_circuit_5v.png
    :width: 600
    :align: center

5. Verbinden Sie den negativen Anschluss des Steckbretts mit einem der Erdungspins auf dem Arduino Uno R3. Die Erdungspins sind mit "GND" gekennzeichnet.

.. image:: img/5_parallel_circuit_gnd.png
    :width: 600
    :align: center

6. Nehmen Sie einen weiteren 220Ω Widerstand, verbinden Sie ein Ende mit dem negativen Anschluss und das andere Ende mit Loch 6B.

.. image:: img/5_parallel_circuit_resistor.png
    :width: 600
    :align: center

7. Nehmen Sie eine weitere rote LED. Die Anode der LED (langes Bein) sollte in Loch 6F sein. Die Kathode (kurzes Bein) sollte in Loch 6E sein.

.. image:: img/5_parallel_circuit_led.png
    :width: 600
    :align: center

8. Platzieren Sie schließlich ein Ende eines kurzen Jumperkabels in Loch 6J und das andere Ende im positiven Anschluss. Damit ist die Parallelschaltung vollständig.

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center

Nun hat diese Schaltung zwei LEDs in einer Parallelschaltung. Es gibt zwei Wege, durch die der Strom fließen kann:

* Im ersten Pfad: Der Strom tritt durch das Jumperkabel in die erste LED ein, fließt durch den Strombegrenzungswiderstand und dann zur negativen Seite des Steckbretts.
* Im zweiten Pfad: Der Strom tritt durch das Jumperkabel in die zweite LED ein, fließt durch den Strombegrenzungswiderstand und dann zur negativen Seite des Steckbretts.
* Auf der negativen Seite konvergieren die beiden Wege wieder und fließen dann durch das schwarze Stromkabel zum Erdungspin auf dem Arduino Uno R3.


**Frage**

Was passiert in dieser Parallelschaltung, wenn eine LED entfernt wird? Warum tritt dieses Phänomen auf?

.. image:: img/5_parallel_circuit_remove.png
    :width: 600
    :align: center


**Schritte zur Spannungsmessung**

1. Stellen Sie das Multimeter auf den Modus 20 Volt DC ein.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Denken Sie daran, dass in einer Parallelschaltung jeder Zweig die gesamte Spannung von der Stromquelle erhält. In Ihrem Aufbau sollte jeder Zweig etwa 5 Volt anzeigen. Beginnen Sie damit, die Spannung entlang des ersten Pfades zu messen.

.. image:: img/5_parallel_circuit_voltage1.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Schaltung
     - Pfad1 Spannung
     - Pfad2 Spannung
   * - 2 LEDs
     - *≈5,00 Volt*
     - 

3. Überprüfen Sie als Nächstes den Spannungsabfall entlang des zweiten Pfades. Auch hier sollten es etwa 5 Volt sein.

.. image:: img/5_parallel_circuit_voltage2.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Schaltung
     - Pfad1 Spannung
     - Pfad2 Spannung
   * - 2 LEDs
     - *≈5,00 Volt*
     - *≈5,00 Volt*

Unser Spannungsmessungs-Experiment in einer Parallelschaltung zeigt klar, dass jeder Zweig einen gleichen Anteil der Gesamtspannung von der Quelle erhält, in diesem Fall etwa 5 Volt. Diese Konstanz in den verschiedenen Pfaden bestätigt das grundlegende Prinzip von Parallelschaltungen, bei denen die Spannung über jeden Zweig gleich bleibt, trotz möglicher geringfügiger Abweichungen aufgrund von Fertigungstoleranzen bei Komponenten wie LEDs und Widerständen.


**Schritte zur Strommessung**

Aus unseren früheren Messungen haben wir gelernt, dass jeder Zweig in einer Parallelschaltung die volle Spannung von der Quelle erhält. Aber wie sieht es mit dem Strom aus? Messen wir ihn jetzt.

1. Stellen Sie das Multimeter auf die Position 200 Milliampere ein.

.. image:: img/multimeter_200ma.png
    :width: 300
    :align: center

2. Für die Strommessung muss das Multimeter in den Strompfad der Schaltung integriert werden. Lassen Sie ein Ende des Widerstands am negativen Anschluss des Steckbretts und verschieben Sie das andere Ende zu Loch 3B.

.. note::
    
    Dieser Schritt führt dazu, dass LED 1 erlischt, während LED 2 weiterhin leuchtet. Dies zeigt eine Eigenschaft von Parallelschaltungen: Die Unterbrechung eines Pfades beeinflusst die anderen Pfade nicht.

.. image:: img/5_parallel_circuit_led1_current.png
    :width: 600
    :align: center

3. Platzieren Sie die roten und schwarzen Messleitungen des Multimeters zwischen der LED und dem Widerstand, und LED 1 wird wieder aufleuchten.

.. image:: img/5_parallel_circuit_led1_current1.png
    :width: 600
    :align: center

4. Notieren Sie den gemessenen Strom in der Tabelle.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Schaltung
     - LED1 Strom
     - LED2 Strom
     - Gesamtstrom
   * - 2 LEDs
     - *≈12,6 Milliampere*
     -
     - 

5. Setzen Sie den ersten Widerstand wieder in seine ursprüngliche Position und lassen Sie ein Ende des zweiten Widerstands am negativen Anschluss des Steckbretts, während Sie das andere Ende zu Loch 9B verschieben.

.. image:: img/5_parallel_circuit_led2_current.png
    :width: 600
    :align: center

6. Messen Sie nun den Strom über LED 2 in der Schaltung.

.. image:: img/5_parallel_circuit_led2_current1.png
    :width: 600
    :align: center

7. Notieren Sie den gemessenen Strom in der Tabelle.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Schaltung
     - LED1 Strom
     - LED2 Strom
     - Gesamtstrom
   * - 2 LEDs
     - *≈12,6 Milliampere*
     - *≈12,6 Milliampere*
     - 

8. Nachdem Sie den Strom in beiden Pfaden gemessen haben, wie hoch ist der Gesamtstrom, wenn die Pfade zusammengeführt werden? Bewegen Sie jetzt das Jumperkabel vom negativen Anschluss des Steckbretts zu Loch 25C.

.. image:: img/5_parallel_circuit_total_current.png
    :width: 600
    :align: center

9. Messen Sie nun den Gesamtstrom der Schaltung.

.. image:: img/5_parallel_circuit_total_current1.png
    :width: 600
    :align: center

10. Tragen Sie die gemessenen Ergebnisse in die Tabelle ein.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Schaltung
     - LED1 Strom
     - LED2 Strom
     - Gesamtstrom
   * - 2 LEDs
     - *≈12,6 Milliampere*
     - *≈12,6 Milliampere*
     - *≈25,3 Milliampere*

Unsere Untersuchung der Parallelschaltungen hat einen wichtigen Aspekt hervorgehoben: Der Gesamtstrom entspricht der Summe der Ströme der einzelnen Zweige und entspricht den grundlegenden Prinzipien elektrischer Schaltungen. Diese praktische Übung verstärkt nicht nur unser Verständnis von Parallelschaltungen, sondern zeigt auch deren spezifisches Verhalten im Vergleich zu Reihenschaltungen auf und vermittelt ein klares Bild davon, wie Komponenten in parallelen Schaltungen die elektrische Last teilen. Diese Erkenntnisse bilden die Grundlage für weitergehende Untersuchungen zur Schaltungsentwicklung und -funktionalität.

**Frage**:

1. Wenn eine weitere LED zu dieser Schaltung hinzugefügt wird, wie verändert sich die Helligkeit der LEDs? Warum? Notieren Sie Ihre Antwort in Ihrem Handbuch.

.. image:: img/5_parallel_circuit_3led.png
    :width: 600
    :align: center



Zusammenfassung von Reihen- und Parallelschaltungen
----------------------------------------------------

**Reihenschaltungen**

* **Vorteile**: Da der Strom im gesamten Stromkreis gleich ist, lässt sich der Strom leicht kontrollieren. Wenn eine Komponente ausfällt, stoppt der Stromfluss. Die Verdrahtung ist einfacher und reduziert die Kosten für den Bau großer Schaltungen.
* **Nachteile**: Wenn ein Teil des Stromkreises beschädigt ist, funktioniert der gesamte Stromkreis nicht mehr. Da der Strom im Stromkreis konstant ist, können keine Komponenten verwendet werden, die unterschiedliche Ströme benötigen.

**Parallelschaltungen**

* **Vorteile**: Wenn ein Pfad im Stromkreis unterbrochen ist, beeinflusst dies nicht die anderen Zweige des Stromkreises. Ein Gerät in einem Zweig kann unabhängig von anderen Geräten funktionieren. Weitere Zweige können jederzeit problemlos zum Stromkreis hinzugefügt werden.
* **Nachteile**: Mit zunehmender Anzahl von Geräten im Stromkreis wird mehr Strom benötigt. Dies kann gefährlich werden, da der Stromkreis sich erhitzt und möglicherweise einen Brand auslöst. Sicherungen oder Leistungsschalter werden verwendet, um den Stromkreis bei zu hohem Strom abzuschalten, um eine Überhitzung zu vermeiden. Die Verdrahtung ist komplexer und erhöht die Kosten für den Bau großer Schaltungen.

**Regeln für Reihen- und Parallelschaltungen**

Hier sind die Regeln für Reihen- und Parallelschaltungen, die Sie mit einem Multimeter weiter überprüfen können:

.. .. list-table::
..    :widths: 10 25 25 25
..    :header-rows: 1

..    * - Schaltung
..      - Spannung
..      - Strom
..      - Widerstand  
..    * - Reihen
..      - Die Gesamtspannung des Stromkreises entspricht der Summe der Spannungen, die von jeder Komponente verbraucht wird (Gesamtspannung = V1 + V2 + V3 + ...).
..      - Der Strom an jedem Punkt des Stromkreises ist gleich (Gesamtstrom = I1 = I2 = I3 = ...).
..      - Der Gesamtwiderstand eines Stromkreises entspricht der Summe der Widerstände jeder Komponente (Gesamtwiderstand = R1 + R2 + R3 + ...).
..    * - Parallel
..      - Die Spannung, die von jeder Last verwendet wird, entspricht der Gesamtspannung, die vom Stromkreis verwendet wird (Gesamtspannung = V1 = V2 = V3 = ...)
..      - Der Gesamtstrom des Stromkreises entspricht der Summe der Ströme, die von jeder Komponente verwendet werden (Gesamtstrom = I1 + I2 + I3 + ...).
..      - Der Kehrwert des Gesamtwiderstands entspricht der Summe der Kehrwerte der Widerstände jeder Komponente (1/Gesamtwiderstand = 1/R1 + 1/R2 + 1/R3 + ...)   


**Reihenschaltung**

  - Die Gesamtspannung des Stromkreises entspricht der Summe der Spannungen, die von jeder Komponente verbraucht wird (Gesamtspannung = V1 + V2 + V3 + ...).
  - Der Strom an jedem Punkt des Stromkreises ist gleich (Gesamtstrom = I1 = I2 = I3 = ...).
  - Der Gesamtwiderstand eines Stromkreises entspricht der Summe der Widerstände jeder Komponente (Gesamtwiderstand = R1 + R2 + R3 + ...).

**Parallelschaltung**

  - Die Spannung, die von jeder Last verwendet wird, entspricht der Gesamtspannung, die vom Stromkreis verwendet wird (Gesamtspannung = V1 = V2 = V3 = ...)
  - Der Gesamtstrom des Stromkreises entspricht der Summe der Ströme, die von jeder Komponente verwendet werden (Gesamtstrom = I1 + I2 + I3 + ...).
  - Der Kehrwert des Gesamtwiderstands entspricht der Summe der Kehrwerte der Widerstände jeder Komponente (1/Gesamtwiderstand = 1/R1 + 1/R2 + 1/R3 + ...)   



.. note::

    Hallo, willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community auf Facebook! Tauchen Sie tiefer in die Welt von Raspberry Pi, Arduino und ESP32 mit Gleichgesinnten ein.

    **Warum mitmachen?**

    - **Expertenunterstützung**: Lösen Sie nach dem Kauf auftretende Probleme und technische Herausforderungen mit Hilfe unserer Community und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Tutorials aus, um Ihre Fähigkeiten zu erweitern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und Vorschauen.
    - **Sonderrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

    👉 Bereit, mit uns zu forschen und zu kreieren? Klicken Sie auf [|link_sf_facebook|] und treten Sie noch heute bei!


4. Ohmsches Gesetz: Eine Reise durch die Grundlagen elektrischer Schaltkreise
===================================================================================

Jedes elektronische Gerät basiert auf Prinzipien, die durch Schaltungen und Schaltkreise geregelt werden. Damit diese Geräte ordnungsgemäß funktionieren, müssen Elektroingenieure den Fluss der Elektrizität genau verstehen und kontrollieren können. Ein entscheidendes Konzept in diesem Bereich ist das Ohmsche Gesetz, das eine grundlegende Beziehung zwischen Spannung, Stromstärke und Widerstand in elektrischen Schaltkreisen beschreibt. Diese Lektion taucht in das Ohmsche Gesetz ein und untersucht dessen Auswirkungen und Anwendungen.

Diese Lektion erforscht die grundlegenden Prinzipien, die jedem elektronischen Gerät zugrunde liegen, das wir heute verwenden. Das Verständnis dieser Prinzipien, insbesondere des Ohmschen Gesetzes, ist für Elektroingenieure unerlässlich, um das Verhalten von Schaltungen effektiv zu steuern und vorherzusagen.



Der Funke der Elektrizität
-------------------------------

Die Geschichte der Elektrizität beginnt mit frühen Experimenten und tiefgreifenden Erkenntnissen. Benjamin Franklin, der mit seinem Drachenexperiment zwar nicht die Elektrizität entdeckte, weckte jedoch Neugierde und inspirierte weitere Forschungen zu elektrischen Ladungen und deren Kräften.

.. image:: img/2_electronic.webp
    :width: 600
    :align: center

Seine Experimente legten den Grundstein für das Verständnis, dass Elektrizität die Bewegung von positiven und negativen Ladungen beinhaltet, ähnlich den Naturphänomenen des Blitzes. Inspiriert von Franklin demonstrierte der französische Wissenschaftler Thomas-François Dalibard praktische Beispiele dafür, wie elektrische Ströme natürlich auftreten können.

Diese Ära erlebte auch die Rivalität und gemeinsamen Errungenschaften von Nikola Tesla und Thomas Edison, deren Bemühungen unsere moderne elektrische Infrastruktur prägten. Teslas Entwicklung des Wechselstroms (AC) und Edisons Einführung der Glühbirne sind Beispiele für die rasanten Fortschritte in der Elektrotechnik.

.. image:: img/2_lamp.webp
    :width: 400
    :align: center

Die Fortschritte setzten sich mit der Erfindung des Transistors im Jahr 1947 fort, einer Komponente, die die Grundlage aller modernen Elektronik bildet. Dieses winzige, aber leistungsstarke Bauteil ermöglichte die Entwicklung von Mikrochips und elektronischen Schaltern, die in unserer heutigen technikgetriebenen Welt eine Schlüsselrolle spielen.

.. image:: img/2_transistor.jpg
    :width: 300
    :align: center
    

Georg Ohm und sein Gesetz
------------------------------

Inmitten dieser technologischen Fortschritte begann der deutsche Physiker Georg Ohm mit Experimenten, die die Grundprinzipien elektrischer Schaltkreise definieren sollten. Zu einer Zeit, als Elektrizität noch ein neues wissenschaftliches Feld war, erforschte Ohm das Verhalten elektrischer Ströme unter verschiedenen Bedingungen mithilfe einfacher, aber effektiver experimenteller Aufbauten mit Drähten, Batterien und selbstgebauten Widerständen.

Ohms akribische Experimente offenbarten eine konsistente proportionale Beziehung zwischen Spannung, Stromstärke und Widerstand, die in der Formel V=IR zusammengefasst ist – heute als Ohmsches Gesetz bekannt. Diese Entdeckung lieferte nicht nur eine mathematische Beschreibung der Elektrizität, sondern ermöglichte auch das vorhersehbare Design und den Betrieb elektrischer Geräte.

.. code-block::

    Spannung = Strom x Widerstand
    Oder
    V = I • R

Ohms Durchhaltevermögen trotz anfänglicher Skepsis unterstrich die Bedeutung seiner Erkenntnisse, die den Grundstein für zukünftige technologische Fortschritte legten und eine neue Ära der Elektrotechnik einläuteten.



Verständnis von Strom, Spannung und Widerstand
----------------------------------------------------

Um das Ohmsche Gesetz vollständig zu verstehen und anzuwenden, ist es wichtig, die Grundkonzepte von Strom, Spannung und Widerstand zu erfassen. Diese Komponenten sind unverzichtbare Elemente jeder Schaltung und können mit den Elementen eines fließenden Flusses verglichen werden.

- **Strom (I)**: Der Fluss von Elektronen durch einen Leiter, gemessen in Ampere (A).
- **Spannung (V)**: Die elektrische Kraft oder der Druck, der Elektronen durch einen Leiter antreibt.
- **Widerstand (R)**: Der Widerstand gegen den Elektronenfluss, gemessen in Ohm (Ω) und typischerweise durch den griechischen Buchstaben Omega dargestellt.

.. image:: img/2_resistance.png
    :width: 400
    :align: center

Ein Vergleich mit einem Gartenschlauch hilft, diese Konzepte zu verdeutlichen:

- **Strom** ist vergleichbar mit dem Wasserfluss, der die Geschwindigkeit angibt, mit der sich Elektronen durch einen Leiter bewegen.
- **Spannung** ist wie der Wasserhahn, der die Kraft regelt, die das Wasser antreibt.
- **Widerstand** ist vergleichbar mit Knoten oder Biegungen im Schlauch, die den Weg des Wassers behindern und den Fluss verlangsamen.

Diese Erklärung hilft uns, das theoretische Wissen des Ohmschen Gesetzes mit dem Verhalten tatsächlicher Schaltungen zu verbinden und bildet die Grundlage für weiteres Lernen und Anwendungen.

Das Ohmsche Gesetz in praktischen Experimenten erkunden
---------------------------------------------------------------

Nun wenden wir das Ohmsche Gesetz praktisch an, indem wir mit einer einfachen LED-Schaltung die Auswirkungen von sich änderndem Widerstand und Spannung beobachten.

**Experimentaufbau**

1. Sie beginnen mit einer einfachen Schaltung, die eine LED und einen 220-Ohm-Widerstand enthält.
   
   .. image:: img/2_uno_gnd.png
     :width: 600
     :align: center

2. Ersetzen Sie den 220-Ohm-Widerstand durch andere Widerstände mit verschiedenen Werten, wie unten aufgeführt. Notieren Sie die Helligkeitsveränderungen der LED bei jedem Austausch, um zu beobachten, wie der Widerstand den Strom und folglich die Lichtausgabe beeinflusst.

   .. list-table::
      :widths: 25 100
      :header-rows: 1

      * - Widerstand
        - Beobachtungen
      * - 100Ω
        - 
      * - 1KΩ
        - 
      * - 10KΩ
        - 
      * - 1MΩ
        - 

  
  Sie werden feststellen, dass die LED nur mit dem 100Ω-Widerstand heller leuchtet als mit dem vorherigen 220Ω-Widerstand. Bei höheren Widerständen nimmt die Helligkeit der LED ab, bis sie bei 1MΩ vollständig erlischt. Warum ist das so?

  Laut dem Ohmschen Gesetz (I = V/R) nimmt der Strom durch die LED bei konstant gehaltener Spannung mit steigendem Widerstand ab, wodurch die LED dunkler wird. Bei 1MΩ ist der Strom zu gering, um die LED zum Leuchten zu bringen.

3. Nachdem Sie die Auswirkungen der Widerstandsänderung beobachtet haben, belassen Sie den Widerstand bei 220 Ohm und ändern die Spannungsversorgung der Schaltung von 5V auf 3,3V. Notieren Sie alle Änderungen in der Helligkeit der LED.

  Sie werden feststellen, dass die LED bei 3,3V etwas dunkler ist als bei 5V. Warum ist das so?

  Laut dem Ohmschen Gesetz sollte der Strom, unter Berücksichtigung des Widerstands und der neuen Spannung, I = V/R sein. Mit einer verringerten Spannung und einem konstanten Widerstand nimmt der Strom ab, wodurch die LED dunkler wird.

**Zusammenfassung**

Durch diese Experimente haben Sie direkt beobachtet, wie grundlegend das Ohmsche Gesetz für das Verständnis und die Gestaltung elektrischer Schaltungen ist. Diese praktische Anwendung hilft, die zuvor besprochenen theoretischen Konzepte zu festigen und zeigt die realen Auswirkungen von Spannung, Strom und Widerstand in der Elektrotechnik.


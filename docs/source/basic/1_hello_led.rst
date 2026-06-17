.. include:: /index.rst
   :start-after: start_hello_message
   :end-before: end_hello_message

1. Hello LED
======================

Welcome to your first hardware lesson! In the Get Started section, you blinked the onboard LED on the UNO Q. Now you'll build a real circuit on a breadboard and control an external LED with code — the "Hello World" of electronics.

Before we start, let's briefly cover the basics:

**What is an LED?**

LED stands for **Light Emitting Diode**. It's a tiny light that turns on when current flows through it in the correct direction. Current enters through the **anode** (long leg, +) and exits through the **cathode** (short leg, −). If you connect it backwards, it simply won't light up — no damage done.

**Why do we need a resistor?**

An LED will draw as much current as it can get. Without a resistor to limit the flow, the LED burns out in seconds. The 220Ω resistor acts like a narrow pipe — it lets just the right amount of current through to keep the LED bright and safe.

In this lesson, you will learn to:

* Build a circuit with an LED, resistor, and jumper wires on a breadboard
* Import and run an Arduino sketch in App Lab
* Use ``pinMode()`` and ``digitalWrite()`` to control an external LED
* Use ``delay()`` to create a blinking pattern

1. Build the Circuit
----------------------

**Components Needed**

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno Q
     - 1 * Red LED
     - 1 * 220Ω Resistor
     - Jumper Wires
   * - |list_uno_q|
     - |list_red_led|
     - |list_220ohm|
     - |list_wire|
   * - 1 * Breadboard
     - 1 * USB Cable
     -
     -
   * - |list_breadboard|
     - |list_usb_cable|
     -
     -

.. tip::

   The 220Ω resistor has color bands **Red → Red → Brown → Gold**. You can also use your Resistor Card to identify it.

**Wiring Diagram**

Follow the diagram below to place each component on the breadboard and connect the wires.

.. image:: img/1_hello_led_fritzing.png
   :width: 700
   :align: center

Here are the connections to make:

#. Place the 220Ω resistor between the LED's cathode row and the breadboard's **negative (−) rail**.

#. Insert the red LED with the **anode** (long leg) and **cathode** (short leg) in separate rows, so the cathode shares a row with the resistor.

   Can't tell the legs apart? Look at the LED's plastic dome — the cathode side has a **flat edge**.

#. Connect the LED's anode row to **digital pin 5** on the UNO Q with a Male-to-Female jumper wire.

#. Connect the breadboard's **negative (−) rail** to any **GND** pin on the UNO Q with another Male-to-Female jumper wire.

.. warning::

   Never connect an LED directly between a pin and GND without a resistor. The LED will draw too much current and burn out immediately.

**Circuit Diagram**

The schematic below shows the same circuit in electrical notation. Learning to read schematics will help you understand how any circuit works, even without a physical photo.

.. image:: img/1_hello_led_schematic.png
   :width: 500
   :align: center

When pin 5 outputs 5V (HIGH), current flows along this path:

  **Pin 5 → LED anode → LED cathode → 220Ω resistor → GND**

The resistor limits the current to a safe level. When pin 5 outputs 0V (LOW), no current flows and the LED turns off.

2. Code
----------

**Import the Code**

All code for this course is provided as ``.zip`` files that you can import directly into App Lab.

#. Open **Arduino App Lab**, go to **My Apps**.

#. Click the dropdown arrow next to **Create new app +** and select **Import App**.

   .. image:: img/1_import_app.png
      :width: 600
      :align: center

#. Navigate to the ``unoq-ai-kit/basic/`` folder and select ``1_hello_led.zip``.

#. The app will appear in **My Apps**. Click it to open.

   .. image:: img/1_app_open.png
      :width: 600
      :align: center

**Run the Code**

#. With the app open, click the **Run** button (▶) in the top-right corner.

   .. image:: img/1_app_run.png
      :width: 600
      :align: center

#. Wait a few seconds for the upload to finish, then check your breadboard — the LED should blink: half a second on, half a second off.

.. image:: img/1_blink_result.gif
   :width: 400
   :align: center

**The Code**

Now that you've seen the LED blink, let's look at the code that makes it happen.

.. code-block:: cpp
   :linenos:

   /*
    * Lesson 1: Hello LED
    * Blinks an external LED connected to pin 5.
    */

   const int ledPin = 5;  // LED connected to digital pin 5

   void setup() {
       pinMode(ledPin, OUTPUT);  // Set pin 5 as an output
   }

   void loop() {
       digitalWrite(ledPin, HIGH);  // Turn the LED on (5V)
       delay(500);                  // Wait half a second
       digitalWrite(ledPin, LOW);   // Turn the LED off (0V)
       delay(500);                  // Wait half a second
   }

**How it Works**

Every Arduino sketch has two functions, and this program follows a simple rhythm:

.. code-block:: text

   setup() → runs once at startup:
       Configure pin 5 as OUTPUT

   loop() → runs over and over forever:
       LED ON  → wait 500ms
       LED OFF → wait 500ms
       (repeat)

Here's what each part does:

* ``const int ledPin = 5;`` — Gives pin 5 a meaningful name. If you ever move the LED to a different pin, you only need to change this one line.
* ``pinMode(ledPin, OUTPUT);`` — Tells the UNO Q that this pin will **send** voltage out (rather than **read** voltage in). Called once in ``setup()`` because the pin's role doesn't change.
* ``digitalWrite(ledPin, HIGH);`` — Sets the pin to 5V. Current flows from the pin, through the LED, through the resistor, to GND → the LED lights up.
* ``digitalWrite(ledPin, LOW);`` — Sets the pin to 0V. No voltage difference → no current → the LED turns off.
* ``delay(500);`` — Pauses the program for 500 milliseconds (half a second). Without ``delay()``, the on/off switching happens millions of times per second — too fast for your eyes to see.

3. Experiment
----------------

**Change the Blink Speed**

Try adjusting the ``delay()`` values and observe how the blink changes:

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Delay Values
     - Effect
   * - ``delay(100)``
     - Fast flicker — 10 blinks per second
   * - ``delay(1000)``
     - Slow blink — once per second
   * - ON ``delay(100)``, OFF ``delay(900)``
     - Quick flash, long pause

**Challenge: Heartbeat Pattern**

Make the LED pulse like a heartbeat — two quick beats, then a rest:

.. code-block:: cpp

   void loop() {
       // First beat
       digitalWrite(ledPin, HIGH);
       delay(100);
       digitalWrite(ledPin, LOW);
       delay(100);

       // Second beat
       digitalWrite(ledPin, HIGH);
       delay(100);
       digitalWrite(ledPin, LOW);
       delay(700);  // Pause between heartbeats
   }

**Challenge: SOS Signal**

SOS in Morse code is three short, three long, three short (··· −−− ···). Can you turn this into code?

.. dropdown:: Click to reveal solution
   :open:

   .. code-block:: cpp

      void loop() {
          // S: three dots
          for (int i = 0; i < 3; i++) {
              digitalWrite(ledPin, HIGH); delay(200);
              digitalWrite(ledPin, LOW);  delay(200);
          }
          delay(400);  // gap between letters

          // O: three dashes
          for (int i = 0; i < 3; i++) {
              digitalWrite(ledPin, HIGH); delay(600);
              digitalWrite(ledPin, LOW);  delay(200);
          }
          delay(400);

          // S: three dots
          for (int i = 0; i < 3; i++) {
              digitalWrite(ledPin, HIGH); delay(200);
              digitalWrite(ledPin, LOW);  delay(200);
          }
          delay(2000);  // pause before repeating
      }

4. Troubleshooting
--------------------

**LED does not light up**

* **Cause:** The LED is connected backwards, or a jumper wire is loose.
* **Solution:** Check that the long leg (anode) connects to pin 5, and the short leg (cathode) connects to the resistor and GND. Push all wires firmly into the breadboard.

**LED is very dim**

* **Cause:** Wrong resistor value.
* **Solution:** The 220Ω resistor is Red-Red-Brown-Gold. A 10kΩ resistor (Brown-Black-Orange) will make the LED barely visible. Use your Resistor Card to double-check.

**LED always on, never blinks**

* **Cause:** Code wasn't uploaded, or ``delay()`` values are too small.
* **Solution:** Make sure you clicked the **Run** button. If the delay is 1ms, the blink is too fast to see — try 500ms.

**LED was bright for a moment, then died**

* **Cause:** The LED was connected without a resistor and burned out.
* **Solution:** Replace the LED with a new one. Double-check that the 220Ω resistor is correctly in the circuit before running again.

**Run button does nothing**

* **Cause:** The board is not connected, or App Lab can't find it.
* **Solution:** Check the USB-C cable is firmly connected at both ends. Try unplugging and re-plugging it. In App Lab, make sure your UNO Q is detected.

5. Summary
-------------

Congratulations! You've built your first circuit and controlled it with code. In this lesson, you learned:

* How to wire an LED, a resistor, and jumper wires on a breadboard
* How to read a wiring diagram and a circuit schematic
* How to import and run a sketch in App Lab
* How ``pinMode()``, ``digitalWrite()``, and ``delay()`` work together
* That ``setup()`` runs once, and ``loop()`` runs forever

These four building blocks appear in every Arduino sketch you'll write from here on. In the next lesson, you'll add a button to control the LED — your first input device!

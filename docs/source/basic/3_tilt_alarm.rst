Tilt Alarm
========================

**Overview**

In this lesson, you will build a simple **tilt alarm** using a **tilt switch** and an **active buzzer**.  
When the device tilts, the buzzer will sound to provide a warning.

--------------------------------------------------

How It Works
--------------------------

A tilt switch changes its internal connection depending on its position.

In this project:

- The **tilt switch** is connected to **pin 2**
- The **active buzzer** is connected to **pin 5**

The tilt switch used here is **closed when upright** and **open when tilted**.  
So when the board tilts, the signal on pin 2 changes and the buzzer is activated.

--------------------------------------------------

Wiring
--------------------------

Connect the components as follows:

- Tilt switch:
  
  - One pin → **GND**
  - The other pin → **D2**

- Active buzzer:
  
  - **VCC** → **D5**
  - **GND** → **GND**

.. note::

   The tilt switch is used with ``INPUT_PULLUP``, so no external resistor is required.

--------------------------------------------------

Program
--------------------------

Upload the following code to the board:

.. code-block:: cpp

    // Tilt alarm with rhythmic buzzer
    // Tilt switch on pin 2, active buzzer on pin 5

    const int tiltPin = 2;
    const int buzzerPin = 5;

    void setup() {
        pinMode(tiltPin, INPUT_PULLUP);
        pinMode(buzzerPin, OUTPUT);
        digitalWrite(buzzerPin, LOW);
    }

    void loop() {
        int tiltState = digitalRead(tiltPin);

        // The switch is open when tilted, so the pin reads HIGH
        if (tiltState == HIGH) {
            delay(30);  // simple debounce

            if (digitalRead(tiltPin) == HIGH) {
                // Rhythmic alarm sound
                digitalWrite(buzzerPin, HIGH);
                delay(100);
                digitalWrite(buzzerPin, LOW);
                delay(100);

                digitalWrite(buzzerPin, HIGH);
                delay(300);
                digitalWrite(buzzerPin, LOW);
                delay(200);
            }
        } else {
            digitalWrite(buzzerPin, LOW);
        }
    }

--------------------------------------------------

Code Explanation
--------------------------

- ``pinMode(tiltPin, INPUT_PULLUP)`` enables the internal pull-up resistor
- When the tilt switch is **upright**, it is closed, so pin 2 reads **LOW**
- When the tilt switch is **tilted**, it opens, so pin 2 reads **HIGH**
- A short ``delay(30)`` is added before checking again to reduce switch bouncing
- The buzzer uses a simple rhythmic pattern to make the alarm sound clearer

--------------------------------------------------

Result
--------------------------

After uploading the code:

- When the tilt switch remains upright, the buzzer stays off
- When the tilt switch is tilted, the buzzer sounds in a rhythmic warning pattern

--------------------------------------------------

Summary
--------------------------

In this lesson, you learned how to:

- Read a tilt switch using a digital input
- Use ``INPUT_PULLUP`` for simple wiring
- Control an active buzzer as an alarm output
- Add a small debounce delay to make the detection more stable
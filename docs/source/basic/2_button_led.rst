2. Button LED
======================

按键一端接2引脚，一端接GND，不需要上下拉和电容。


.. code-block:: arduino

    // Button on pin 2 controls LED on pin 5

    const int buttonPin = 2;
    const int ledPin = 5;

    void setup() {
        pinMode(buttonPin, INPUT_PULLUP); // Use internal pull-up resistor
        pinMode(ledPin, OUTPUT);
    }

    void loop() {
        int buttonState = digitalRead(buttonPin);

        // Button pressed (LOW because of INPUT_PULLUP)
        if (buttonState == LOW) {
            digitalWrite(ledPin, HIGH); // Turn LED ON
        } else {
            digitalWrite(ledPin, LOW);  // Turn LED OFF
        }
    }
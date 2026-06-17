7. Ultrasonic buzzer
============================

.. code-block:: arduino

    #include <Arduino_RouterBridge.h>

    const int trigPin = 2;
    const int echoPin = 3;
    const int buzzerPin = 5;

    long duration;
    float distanceCm;

    void setup() {
        Monitor.begin();

        pinMode(trigPin, OUTPUT);
        pinMode(echoPin, INPUT);
        pinMode(buzzerPin, OUTPUT);

        digitalWrite(trigPin, LOW);
        digitalWrite(buzzerPin, LOW);
    }

    float getDistance() {
        // Send trigger pulse
        digitalWrite(trigPin, LOW);
        delayMicroseconds(2);
        digitalWrite(trigPin, HIGH);
        delayMicroseconds(10);
        digitalWrite(trigPin, LOW);

        // Read echo pulse
        duration = pulseIn(echoPin, HIGH, 30000);  // timeout: 30 ms

        // If no signal is received, return -1
        if (duration == 0) {
            return -1;
        }

        // Convert to distance in cm
        return duration * 0.0343 / 2;
    }

    void beepOnce(int onTime, int offTime) {
        digitalWrite(buzzerPin, HIGH);
        delay(onTime);
        digitalWrite(buzzerPin, LOW);
        delay(offTime);
    }

    void loop() {
        distanceCm = getDistance();

        Monitor.print("Distance: ");
        if (distanceCm < 0) {
            Monitor.println("Out of range");
            digitalWrite(buzzerPin, LOW);
            delay(300);
            return;
        } else {
            Monitor.print(distanceCm);
            Monitor.println(" cm");
        }

        // Parking radar logic
        if (distanceCm > 100) {
            // Safe distance, no alarm
            digitalWrite(buzzerPin, LOW);
            delay(300);
        } 
        else if (distanceCm > 50) {
            // Slow beep
            beepOnce(100, 500);
        } 
        else if (distanceCm > 20) {
            // Medium beep
            beepOnce(100, 250);
        } 
        else {
            // Very close, fast beep
            beepOnce(100, 100);
        }
    }
.. note::

    Hello, welcome to the SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebook! Dive deeper into Raspberry Pi, Arduino, and ESP32 with fellow enthusiasts.

    **Why Join?**

    - **Expert Support**: Solve post-sale issues and technical challenges with help from our community and team.
    - **Learn & Share**: Exchange tips and tutorials to enhance your skills.
    - **Exclusive Previews**: Get early access to new product announcements and sneak peeks.
    - **Special Discounts**: Enjoy exclusive discounts on our newest products.
    - **Festive Promotions and Giveaways**: Take part in giveaways and holiday promotions.

    👉 Ready to explore and create with us? Click [|link_sf_facebook|] and join today!

FAQ
====================

What is included in the kit?
-------------------------------

The kit includes an Arduino Uno R3 and a variety of sensors, modules, components, and accessories for building experiments and projects.

See: :ref:`include_in_kit`


What is the difference between “Video Tutorials” and “Hands-on Lessons”?
--------------------------------------------------------------------------------

* **Video Tutorials** help you understand concepts and see demonstrations.
* **Hands-on Lessons** guide you through building circuits and writing code using the kit components.

Tip:

* Watch the video first, then complete the hands-on lesson for better retention.


Why the Arduino UNO R3 Cannot Be Used
----------------------------------------------

Even when using an official Arduino UNO R3, the board may fail to work properly due to environmental or operational reasons.  
Below are the most common causes and explanations.

#. **USB driver or operating system issues**

   The Arduino UNO R3 uses an **ATmega16U2** USB interface chip, which is normally recognized automatically on Windows 10 / 11 and macOS.
   
   However, on older systems (such as Windows 7 or lightweight Windows installations), the required USB CDC driver may be missing.  
   In this case, the computer may fail to recognize the Arduino serial device.
   
   **Solution:**
   
   * Manually update or install the Arduino USB driver via **Device Manager**.
   * It is recommended to include USB driver update instructions in the FAQ for reference.


#. **Incorrect board or port selected in Arduino IDE**

   If the correct **Board** or **Port** is not selected in the Arduino IDE, uploading sketches will fail.
   
   A common error message is::
   
       stk500_recv(): programmer not responding
   
   This is a configuration issue and **does not indicate hardware damage**.
   
   **Solution:**
   
   * Select **Arduino UNO** under *Tools → Board*
   * Select the correct serial port under *Tools → Port*


#. **Using a USB hub or unstable USB port**

   If the Arduino is connected through:
   
   * USB hubs
   * USB ports on monitors
   * USB ports integrated into keyboards
   
   The power supply and signal may be unstable, causing the Arduino to fail USB enumeration.
   
   **Recommendation:**
   
   * Connect the Arduino **directly to the computer’s USB port**.


#. USB port issues on the computer

   Some USB ports may have issues such as:
   
   * Insufficient power (common on front-panel USB ports)
   * Poor physical contact
   * Damaged USB ports
   
   **Recommendation:**
   
   * Try a different USB port
   * Preferably use the **rear USB ports on the motherboard**


#. Using USB power and external power at the same time

   If the Arduino is powered by USB while external power is also supplied via **5V** or **Vin**, it may cause:
   
   * Voltage regulator lock-up
   * Overheating of the power circuit
   * Unstable USB communication
   
   This may cause the Arduino to appear disconnected or unstable.
   
   **Recommendation:**
   
   * Avoid supplying USB power and external power at the same time unless required and properly designed.


#. **Wiring errors causing USB chip damage**


   When connecting external modules, incorrect wiring may cause damage to the **ATmega16U2 USB chip**, including:
   
   * Reversing **5V** and **GND**
   * Applying high voltage (such as 12V) to Arduino pins
   * Power conflicts between USB and external supplies
   
   In this case, the Arduino may still power on, but the computer will not recognize the serial port.
   
   **Note:**
   
   This type of failure is caused by incorrect operation and is **not a quality issue** with the Arduino board itself.


Why the Multimeter Cannot Be Used
-----------------------------------

Even if the multimeter itself is functioning normally, incorrect usage may cause it to appear as *not turning on* or *unable to measure*.  
Below are the most common causes and solutions.

#. **Battery not installed**

   Although a 9V battery is included in the kit, it must be installed by the user. If no battery is installed, the multimeter screen will not turn on.
   
   A video tutorial for battery installation is available in :ref:`use_multimeter`.

#. Test leads connected to the wrong jacks

   If the red test lead is inserted into the **10A** or **mA** jack, the multimeter will not display readings when measuring voltage or resistance.
   
   * For voltage or resistance measurements:
   
     * Red lead → **VΩ**
     * Black lead → **COM**

#. **Incorrect measurement range selected**

   If the selected mode does not match the measurement target, for example:
   
   * Measuring DC voltage using AC range
   * Measuring voltage using resistance mode
   
   The multimeter will not show correct readings.
   
   **Solution:**
   
   * Select the appropriate range:
     * **DCV** for DC voltage
     * **Ω** for resistance

#. Multimeter powers on but cannot measure

   If the multimeter displays values but cannot measure accurately, the test leads may be damaged.
   
   Repeated pulling or twisting of the leads can cause internal wire breakage and unstable contact.
   
   **Solution:**
   
   * Replace the test leads if unstable or intermittent readings occur


How do I run my first Arduino program?
------------------------------------------------

1. Connect the Arduino board to your computer using a USB cable.
2. Open Arduino IDE and select the correct **Board** and **Port**.
3. Open an example sketch (such as Blink) and click **Upload**.
4. Confirm the on-board LED behavior to verify it works.

See: :ref:`first_sketch`



My circuit does not work as expected. What should I do first?
-------------------------------------------------------------------

* Re-check wiring against the tutorial diagram (most issues are wiring mistakes).
* Verify component polarity (LED direction, electrolytic capacitor polarity, etc.).
* Confirm power and ground are connected correctly.
* Use a multimeter to verify voltage at key points if available.


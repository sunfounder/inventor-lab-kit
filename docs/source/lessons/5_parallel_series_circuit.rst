.. note::

    Hello, welcome to the SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebook! Dive deeper into Raspberry Pi, Arduino, and ESP32 with fellow enthusiasts.

    **Why Join?**

    - **Expert Support**: Solve post-sale issues and technical challenges with help from our community and team.
    - **Learn & Share**: Exchange tips and tutorials to enhance your skills.
    - **Exclusive Previews**: Get early access to new product announcements and sneak peeks.
    - **Special Discounts**: Enjoy exclusive discounts on our newest products.
    - **Festive Promotions and Giveaways**: Take part in giveaways and holiday promotions.

    👉 Ready to explore and create with us? Click [|link_sf_facebook|] and join today!

5. Series Circuit vs. Parallel Circuit
=================================================

In this lesson, you will engage in building and analyzing both series and parallel circuits, learning to measure and understand how voltage behaves in different circuit configurations. Utilizing a multimeter, you will measure the voltage and resistance of the circuits you construct, gaining practical insights into circuit dynamics.

In this exciting lesson, you'll:

* Connect schematic diagrams with actual circuits.
* Use a multimeter to measure resistance and voltage.
* Build series and parallel circuits using a breadboard.
* Compare the behavior of voltage in series and parallel circuits.

These objectives will empower you to bridge the gap between theoretical knowledge and practical application, enriching your understanding of electronics through hands-on experience.


Series Circuit vs. Parallel Circuit
------------------------------------------

In our previous lessons, we've successfully constructed a simple circuit with an Arduino Uno R3, a resistor, and an LED. The current in this setup flows in a series configuration: from the board's Pin 13 pin, through the LED, through the resistor, and back to the GND pin. This is a straightforward example of a series circuit.

But as we delve deeper into the world of electronics, we encounter circuits that are more complex, comprising components arranged in series or parallel. To comprehend these arrangements and their implications on current and voltage, we need to familiarize ourselves with circuit diagrams, also known as schematic diagrams.

**Wiring Diagrams vs. Schematic Diagrams**

We've been using wiring diagrams—pictorial representations that mimic the physical layout of circuit components. These diagrams are intuitive and serve well for assembly purposes:

.. image:: img/2_uno_gnd.png
    :width: 600
    :align: center

However, to grasp a circuit's functionality and design logic, schematic diagrams are indispensable. Schematic diagrams distill circuits down to their essence, using standardized symbols to represent each component. They reveal the electrical relationships between components without the clutter of physical layouts.

Here are the symbols for a LED, a resistor, and a battery that you'll often find in schematics:

.. image:: img/5_led_resistor_symbol.png
  :align: center

A schematic diagram based on our previous wiring would look like this, with the entire Arduino Uno R3 acting as a battery powering the circuit. From this schematic, you can clearly indicate the flow and direction of current, simplifying the complexity of physical connections.

.. image:: img/5_serial_circuit_1led.png
  :align: center

**Series vs. Parallel Configurations**

In a series circuit, components are lined up in a row, so the current has a single path to follow. If one component fails, the entire circuit is interrupted—much like a string of old Christmas lights where one burnt-out bulb would darken the whole chain.

.. image:: img/5_serial_circuit_2led.png
  :align: center

A parallel circuit, on the other hand, divides the current into multiple paths. Each component operates independently, so if one path is broken, the others continue to function. Think of your home's electrical system: if you switch off a light, the TV can still be on.

.. image:: img/5_parallel_circuit.png
  :align: center


Diving into Series Circuits
------------------------------

Building on our understanding of the differences between series and parallel circuits, this activity focuses on constructing a series circuit with multiple LEDs. Remember, in a series circuit, the electrical current flows through a single pathway. Let's explore the unique characteristics of series circuits through this practical exercise.

**Components Needed**

.. list-table:: 
   :widths: 25 25 25 25
   :header-rows: 0

   * - 1 * Arduino Uno R3
     - 3 * Red LEDs
     - 3 * 220Ω Resistor
     - Jumper Wires
   * - |list_uno_r3| 
     - |list_red_led| 
     - |list_220ohm| 
     - |list_wire| 
   * - 1 * USB Cable
     - 1 * Breadboard
     - 1 * Multimeter
     -   
   * - |list_usb_cable| 
     - |list_breadboard| 
     - |list_meter|
     - 

**Building the Circuit**

1. Adjust the previous LED circuit by removing the jumper wire between 1J and the breadboard's positive side on the right. Then, take another red LED and insert its cathode (the shorter leg) into 1J, and the anode into the breadboard's positive side, so you can serially connect another LED in the circuit.

.. image:: img/5_serial_circuit.png

Now you have a series circuit with two LEDs. Follow the current through the circuit:

* Current flows from 5V on the Arduino Uno R3, through a long jumper wire to the breadboard's positive terminal.
* Then the current flows through the first LED, lighting it up due to the flow of current.
* The current then flows through the breadboard's metal clips to the second LED, which also lights up.
* After leaving the second LED, it enters the 220Ω resistor, where it encounters resistance, reducing the amount of current. Without this resistor, the current through the LEDs would be too high and could burn them out.
* It then flows back to the Arduino Uno R3's ground pin, completing the circuit.

**Question** 

In this series circuit, what happens if you remove one LED? Why does this occur?

.. image:: img/5_serial_circuit_remove.png
    :width: 600
    :align: center


**Measuring Voltage**

1. Set the multimeter to the 20 volts DC setting.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Use the multimeter to measure the voltage across the resistor.

    .. note::
        
        Measuring a component's voltage in a circuit means checking the voltage across it. Essentially, voltage represents the energy difference between two points. So, when you measure a component's voltage, you're gauging the energy difference from one side to the other.

.. image:: img/5_serial_circuit_voltage_resistor.png
    :width: 600
    :align: center

3. Record the voltage across the resistor, voltage unit: Volts (V).

.. note::

    * Mine was 1.13V, you should fill in according to your measurement.

    * Due to wiring issues and your hand's instability, you may see the voltage fluctuate. You need to keep your hand steady, then observe several times to get a fairly stable voltage value.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Resistor Voltage
     - LED1 Voltage
     - LED2 Voltage
     - Total Voltage 
   * - 2 LEDs
     - *≈1.13 volts*
     - 
     - 
     - 

4. Now, measure the voltage across LED 1 in the circuit.

.. image:: img/5_serial_circuit_voltage_led1.png
    :width: 600
    :align: center

5. Record the voltage across LED 1 in the table.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Resistor Voltage
     - LED1 Voltage
     - LED2 Voltage
     - Total Voltage 
   * - 2 LEDs
     - *≈1.13 volts*
     - *≈1.92 volts*
     - 
     - 

6. Measure the voltage across LED 2 in the circuit.

.. image:: img/5_serial_circuit_voltage_led2.png
    :width: 600
    :align: center

7. Record the voltage across LED 2 in the table.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Resistor Voltage
     - LED1 Voltage
     - LED2 Voltage
     - Total Voltage 
   * - 2 LEDs
     - *≈1.13 volts*
     - *≈1.92 volts*
     - *≈1.92 volts*
     - 

8. Now measure the total voltage in the circuit.

.. image:: img/5_serial_circuit_voltage.png
    :width: 600
    :align: center

9. Fill in the measured voltage into the Total Voltage column of the table.

.. list-table::
   :widths: 25 25 25 25 25
   :header-rows: 1

   * - Circuit
     - Resistor Voltage
     - LED1 Voltage
     - LED2 Voltage
     - Total Voltage 
   * - 2 LEDs
     - *≈1.13 volts*
     - *≈1.92 volts*
     - *≈1.92 volts*
     - *≈4.97 volts*


Through our measurements, you will discover:

.. code-block::

  4.97 volts ≈ 1.13 volts + 1.92 volts + 1.92 volts

  Total Voltage = Resistor Voltage + LED 1 Voltage + LED 2 Voltage

You can also calculate whether your measurement results conform to the above equation.


.. note::
    
    Due to wiring stability, or minor manufacturing differences in the LEDs and resistor, the sum of the resistor voltage and the two LEDs' voltages might not equal the total voltage you measured. This is also okay, as long as it's within a reasonable range.


This is a characteristic of a series circuit, where the total voltage across the circuit is the sum of the voltages across each component.

**Measuring Current**

Having understood the voltage characteristics of series circuits, let's now explore the current within the circuit using a multimeter.


1. Set the multimeter to the 20 milliamps position. The current won't exceed 20mA, so this setting is chosen. If unsure, it's recommended to start with the 200mA setting.

.. image:: img/multimeter_20a.png
  :width: 300
  :align: center

2. For current measurement, the multimeter must be integrated into the circuit's flow path. Keep the LED's anode in hole 1F and shift its cathode (the shorter leg) from hole 1E to hole 3E.

.. image:: img/5_serial_circuit_led1_current.png
    :width: 600
    :align: center

3. Measure the current across LED 1 in the circuit.

.. image:: img/5_serial_circuit_led1_current1.png
    :width: 600
    :align: center

4. Record the measured current in the table.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuit
     - LED1 Current
     - LED2 Current
   * - 2 LEDs
     - *≈4.43 milliamps*
     - 

5. Move the first LED's cathode back to its original position and shift the second LED's cathode (the shorter leg) from hole 1J to hole 2J.

.. image:: img/5_serial_circuit_led2_current.png
    :width: 600
    :align: center

6. Measure the current across LED 2 in the circuit.

.. image:: img/5_serial_circuit_led2_current1.png
    :width: 600
    :align: center

7. Record the measured current in the table.

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuit
     - LED1 Current
     - LED2 Current
   * - 2 LEDs
     - *≈4.43 milliamps*
     - *≈4.43 milliamps*

Our measurements have illustrated a fundamental principle of series circuits: the current that flows through each component is identical. This consistent flow underscores the interconnectedness of components in series, where the interruption of current in one part affects the entire circuit.

The exploration of voltage, current, and resistance not only enriches our understanding of series circuits but also lays the groundwork for more complex electrical engineering concepts. It's through these hands-on experiments that we bridge the gap between theory and practical application, making the learning process both engaging and informative.


**Question**

If another LED is added to this circuit, resulting in three LEDs, how does the brightness of the LEDs change? why? How do the voltages across the three LEDs change? 



Diving into Parallel Circuits
---------------------------------------

**Components Needed**

* 1 * Arduino Uno R3
* 3 * Red LEDs
* 3 * 220Ω Resistors
* Several Jumper Wires
* 1 * USB Cable
* 1 * Breadboard
* 1 * Multimeter with Test Leads

**Building the Circuit**

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center
  
1. Connect a 220Ω resistor to the breadboard. One end should be in the negative terminal, and the other end should be in hole 1B.

.. image:: img/2_connect_resistor.png
    :width: 300
    :align: center

2. Add a red LED to the breadboard. The LED's anode (long leg) should be in hole 1F. The cathode (short leg) should be in hole 1E.

.. image:: img/2_connect_led.png
    :width: 300
    :align: center

3. Use a short jumper wire to connect the LED and the power source. One end of the jumper wire should be in hole 1J. The other end should be in the positive terminal.

.. image:: img/2_connect_wire.png
    :width: 300
    :align: center

4. Connect the long jumper wire connected to the breadboard's positive terminal to the 5V pin on the Arduino Uno R3. The LED should turn on and stay on. The 5V pin provides a constant 5 volts DC to the circuit. This is different from pin 13, which can be programmed via the Arduino IDE software to turn on and off.

.. image:: img/5_parallel_circuit_5v.png
    :width: 600
    :align: center

5. Connect the breadboard's negative terminal to one of the ground pins on the Arduino Uno R3. The ground pins are marked as "GND".

.. image:: img/5_parallel_circuit_gnd.png
    :width: 600
    :align: center

6. Take another 220Ω resistor, connect one end to the negative terminal and the other end to hole 6B.

.. image:: img/5_parallel_circuit_resistor.png
    :width: 600
    :align: center

7. Take another red LED. The LED's anode (long leg) should be in hole 6F. The cathode (short leg) should be in hole 6E.

.. image:: img/5_parallel_circuit_led.png
    :width: 600
    :align: center

8. Finally, place one end of a short jumper wire in hole 6J and the other end in the positive terminal. This completes the parallel circuit.

.. image:: img/5_parallel_circuit_bb.png
    :width: 600
    :align: center


Now, this circuit has two LEDs in a parallel configuration. There are two paths for current to flow through:

* In the first path: current enters the first LED from the jumper wire, flows through the current-limiting resistor, and then to the negative side of the breadboard.
* In the second path: current enters the second LED from the jumper wire, flows through the current-limiting resistor, and then to the negative side of the breadboard.
* At the negative side, the two paths converge again and then flow through the black power wire to reach the ground pin on the Arduino Uno R3.


**Question**

In this parallel circuit, what happens if one LED is removed? Why does this occur? 

.. image:: img/5_parallel_circuit_remove.png
    :width: 600
    :align: center


**Voltage Measurement Steps**

1. Adjust the multimeter to the DC 20 volts mode.

.. image:: img/multimeter_dc_20v.png
    :width: 300
    :align: center

2. Remember, in a parallel circuit, each branch gets the entire voltage from the power source. So, each branch in your setup should show around 5 volts. Start by measuring the voltage along the first path.

.. image:: img/5_parallel_circuit_voltage1.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuit
     - Path1 Voltage
     - Path2 Voltage
   * - 2 LEDs
     - *≈5.00 volts*
     - 

3. Next, check the voltage drop across the second path. Expect it to be near 5 volts as well.

.. image:: img/5_parallel_circuit_voltage2.png
    :width: 600
    :align: center

.. list-table::
   :widths: 25 25 25
   :header-rows: 1

   * - Circuit
     - Path1 Voltage
     - Path2 Voltage
   * - 2 LEDs
     - *≈5.00 volts*
     - *≈5.00 volts*

Our voltage measurement exercise in a parallel circuit clearly demonstrates that each branch receives an equal share of the total voltage from the source, approximately 5 volts in this case. This consistency across different paths confirms the fundamental nature of parallel circuits, where voltage remains constant across each branch, despite potential minor variations due to manufacturing differences in components like LEDs and resistors.


**Current Measurement Steps**

From our previous measurements, we learned that each branch in a parallel circuit receives the full voltage from the source. But what about the current? Let's measure it now.

1. Set the multimeter to the 200 milliamps position.

.. image:: img/multimeter_200ma.png
    :width: 300
    :align: center

2. For current measurement, the multimeter must be integrated into the circuit's flow path. Leave one end of the resistor on the breadboard's negative terminal and move the other end to hole 3B.

.. note::
    
    This step will cause LED 1 to turn off while LED 2 remains lit. This demonstrates a characteristic of parallel circuits: the disconnection of one path does not affect the other paths.

.. image:: img/5_parallel_circuit_led1_current.png
    :width: 600
    :align: center

3. Place the multimeter's red and black leads between the LED and the resistor, and you will see LED1 light up again.

.. image:: img/5_parallel_circuit_led1_current1.png
    :width: 600
    :align: center

4. Record the measured current in the table.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuit
     - LED1 Current
     - LED2 Current
     - Total Current
   * - 2 LEDs
     - *≈12.6 milliamps*
     -
     - 

5. Return the first resistor to its original position, and keep one end of the second resistor at the breadboard's negative terminal while moving the other end to hole 9B.

.. image:: img/5_parallel_circuit_led2_current.png
    :width: 600
    :align: center

6. Now, measure the current across LED 2 in the circuit.

.. image:: img/5_parallel_circuit_led2_current1.png
    :width: 600
    :align: center

7. Record the measured current in the table.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuit
     - LED1 Current
     - LED2 Current
     - Total Current
   * - 2 LEDs
     - *≈12.6 milliamps*
     - *≈12.6 milliamps*
     - 

8. Having measured the current in both paths, what is the total current when the paths converge? Now, move the jumper wire from the breadboard's negative terminal to hole 25C.

.. image:: img/5_parallel_circuit_total_current.png
    :width: 600
    :align: center

9. Measure the total current of the circuit now.

.. image:: img/5_parallel_circuit_total_current1.png
    :width: 600
    :align: center

10. Fill in the measured results in the table.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Circuit
     - LED1 Current
     - LED2 Current
     - Total Current
   * - 2 LEDs
     - *≈12.6 milliamps*
     - *≈12.6 milliamps*
     - *≈25.3 milliamps*

Our exploration into parallel circuits has illuminated a key aspect: the total current mirrors the sum of individual branch currents, adhering to the fundamental principles of electrical circuits. This hands-on activity not only strengthens our understanding of parallel circuitry but also highlights its distinct behavior compared to series circuits, offering a clear picture of how components in parallel share the electrical load. As we continue our journey through the world of electronics, these insights lay the groundwork for deeper investigations into circuit design and functionality.

**Question**:

1. If another LED is added to this circuit, what happens to the brightness of the LEDs? Why? Record your answer in your handbook.

.. image:: img/5_parallel_circuit_3led.png
    :width: 600
    :align: center



Summary of Series and Parallel Circuits
-----------------------------------------------------

**Series Circuits**

* **Advantages**: Since the current throughout the circuit is the same, it's easy to control the current. If one component fails, the current will stop. Its wiring is simpler, reducing the cost of building large circuits.
* **Disadvantages**: If one part of the circuit is damaged, the whole circuit will stop working. Since the current in the circuit is steady, you can't use components that require different currents.

**Parallel Circuits**

* **Advantages**: If any path in the circuit is disconnected, it does not affect the other branches in the circuit. A device in one branch can operate independently of other devices. More branches can be easily added to the circuit at any time.
* **Disadvantages**: As more devices are added to the circuit, more current is drawn. This can become dangerous as the circuit heats up, potentially leading to fire. Fuses or circuit breakers are used to disconnect the circuit when the current is too high to avoid overheating. Its wiring is more complex, increasing the cost of making large circuits.

**Rules of Series and Parallel Circuits**

Here are the rules for series and parallel circuits, which you can continue to verify with a multimeter:

.. .. list-table::
..    :widths: 10 25 25 25
..    :header-rows: 1

..    * - Circuit
..      - Voltage
..      - Current
..      - Resistance  
..    * - Series
..      - The total voltage of the circuit equals the sum of the voltages used by each component (Total voltage = V1 + V2 + V3 + ...).
..      - The current at any point in the circuit is the same (Total current = I1 = I2 = I3 = ...).
..      - The total resistance of a circuit equals the sum of the resistances of each component (Total resistance = R1 + R2 + R3 + ...).
..    * - Parallel
..      - The voltage used by each load equals the total voltage used by the circuit (Total voltage = V1 = V2 = V3 = ...)
..      - The total current of the circuit equals the sum of the currents used by each component (Total current = I1 + I2 + I3 + ...).
..      - The reciprocal of the total resistance equals the sum of the reciprocals of each component's resistance (1/ Total resistance = 1/R1 + 1/R2 + 1/R3 + ...)   


**Series**

  - The total voltage of the circuit equals the sum of the voltages used by each component (Total voltage = V1 + V2 + V3 + ...).
  - The current at any point in the circuit is the same (Total current = I1 = I2 = I3 = ...).
  - The total resistance of a circuit equals the sum of the resistances of each component (Total resistance = R1 + R2 + R3 + ...).

**Parallel**

  - The voltage used by each load equals the total voltage used by the circuit (Total voltage = V1 = V2 = V3 = ...)
  - The total current of the circuit equals the sum of the currents used by each component (Total current = I1 + I2 + I3 + ...).
  - The reciprocal of the total resistance equals the sum of the reciprocals of each component's resistance (1/ Total resistance = 1/R1 + 1/R2 + 1/R3 + ...)   





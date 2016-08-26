# Using the RTC / Low-Power Operation

When using the Riffle to log data for extended periods, there are several techniques to extending battery life.  

## Putting the 328 chip to Sleep

One of the most basic is to put the Atmel 328 chip into a "sleep" mode that consumes less power, during times that no active sensing is being done.  This is accomplished by the "LowPower" library by RocketScream. Thiis reduces the current of the board from tens of milliamps to a fraction of a milliamp -- which extends the battery from about 10 days of operation to several months, depending on the sleep/wake protocol implemented.

However, the 328 chip is not very good at keeping track of the time while in sleep mode, so it's important to use the Real Time Clock (RTC) to keep track of the time.

Additionally, the RTC has an 'alarm' functionality that, in combination with an 'interrupt' feature on the Atmel328, can wake the Riffle from sleep.  When the alarm is set, the RTC will pull an alarm pin to the high-voltage (HIGH) setting.  A special pin on the Riffle -- **D5** -- can be used as a hardware interrupt.  D5 can be programmed so that, even during sleep, it will 'listen' for this sudden change, and wake up the Riffle out of sleep mode.

<img src="pics/rtc_pin.png" width=500>

## Switching off Battery Measurement Circuit

The Riffle 0.1.8 has an on-board circuit to measure the current battery level, via analog pin **A3**. This is done via a simple voltage divider circuit between the battery and ground;  one issue regarding power loss is that a voltage divider will slowly leak power to ground.  To avoid this, the Riffle 0.1.8 has placed a MOSFET switch on this circuit, so that the measurement circuit can be turned "off" when the battery isn't being measured.  This functionality is controlled by pin **D4**.  

<img src="pics/battery_switch.png" width=400>

There is an example in the included code above, "low_power_operation.ino", that demonstrates turning the battery measurement circuit on / off.

## Switching off External Sensors

One typical application of the Riffle is to connect it to external sensors via the 2x7 pin header on one end of the board.  Usually, any such sensors will be powered via the "3.3V" or "3V3" pin. 

<img src="pics/riffle_pinout.png" width=500>

Even if the main microcontroller chip is put to sleep, however, connected sensors can still use power when not being used.  In order to avoid this effect, the Riffle 0.1.8 has a MOSFET switch, controlled by pin **D8**, that can "turn off" the "3V3" line. 

<img src="pics/external_switch.png"  width=500>

There is an example in the included code above, "low_power_operation.ino",  that demonstrates turning external power on/off.

## Switching off the microSD card

The Riffle is typically used to log data to a microSD card.  MicroSD cards are complex devices in their own right, and while some sleep at low currents, others have quite variable power consumption.  The RIffle 0.1.8 can cut off power to the microSD card using a MOSFET switch controlled by pin **D6**.

<img src="pics/microSD_switch.png"  width=500>

Code in the example above, "low_power_operation.ino", demonstrates turning the microSD on and off.  



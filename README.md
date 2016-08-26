# Using the RTC / Low-Power Operation

When using the Riffle to log data for extended periods, there are several techniques to extending battery life.  

**Sleep.** One of the most basic is to put the Atmel 328 chip into a "sleep" mode that consumes less power, during times that no active sensing is being done.  This is accomplished by the "LowPower" library by RocketScream. Thiis reduces the current of the board from tens of milliamps to a fraction of a milliamp -- which extends the battery from about 10 days of operation to several months, depending on the sleep/wake protocol implemented.

However, the 328 chip is not very good at keeping track of the time while in sleep mode, so it's important to use the Real Time Clock (RTC) to keep track of the time.

Additionally, the RTC has an 'alarm' functionality that, in combination with an 'interrupt' feature on the Atmel328, can wake the Riffle from sleep.  When the alarm is set, the RTC will pull an alarm pin to the high-voltage (HIGH) setting.  A special pin on the Riffle -- **D5** -- can be used as a hardware interrupt.  D5 can be programmed so that, even during sleep, it will 'listen' for this sudden change, and wake up the Riffle out of sleep mode.

<img src="pics/rtc_pin.png" width=500>

**Avoiding power loss through the battery measurement circuit**.

<img src="pics/battery_switch.png" width=500>

**Avoiding power loss through any external sensors**. 

<img src="pics/external_switch.png"  width=500>

**Avoiding power loss through the microSD card**.

<img src="pics/microSD_switch.png"  width=500>




# Shelly-Pro-1-ESPHome
The internals of the Shelly Pro 1 and pinout


There is a new Shelly on the market that now finally shipped. After buying and receiving it i immediately startet taking it apart. There where some things i noticed right at the beginning. 

## Multiple small board’s 
It has two switch inputs but only one of them gets utilized, also there is one more LED at the top of the device for the second relay that the Pro 2 version has, that is not being used. You can see that they build one PCB for four device versions. 
The PSU, the switch input board and the Relays board are all removable.


## Pinout
After some further digging i found out there where using SMSC’s LAN8720A chip for the LAN communication. The ESP there are using is an ESP32 DOWDQ6, wich i am not sure why there are not using the same as in the Shelly Plus 1 (ESP32-U4WDH) or even the ESP32 S3. But maybe there where some supply chain issues, so that they needed to change out the ESP to an older model. Because of that they may change the ESP to a different one in the future and with that the pinout may change.

ESP32 DOWDQ6| SN74HC595B | LAN8720A | Component
------------|------------|----------|----------
GPIO 4      |RCLK        |          |
GPIO 13     |SER         |          |
GPIO 14     |SRCLK       |          |
GPIO 17     |            |CLKIN     |
GPIO 18     |            |MDIO      |
GPIO 19     |            |TXD0      |
GPIO 21     |            |TXEN      |
GPIO 22     |            |TXD1      |
GPIO 23     |            |MDC       |
GPIO 25     |            |RXD0      |
GPIO 26     |            |RXD1      |
GPIO 27     |            |CRS_DV    |
GPIO 35     |            |          |Reset Button
GPIO 38     |            |          |Button input 1
GPIO 39     |            |          |Button input 2


## Shift register
At first I could not figure out what kind of IC there where using to control the LEDs and the relay but after some digging on the internet I found out that it is an ti SN74HC595B 8 channel shift register, wich is even included in the ESPHome components. The pinout of the shift register is the the following:

SN74HC595B| Component
----------|----------
QA        |Relay
QB        |Out 2LED
QC        |RGB Blue
QD        |RGB Green
QE        |RGB Red
QF        |nc
QG        |nc
QH        |nc


## Programming 

# Marlin2-Tronxy_P802M-Configuration
Marlin's Configuration files for Tronxy P802M 3D printer. 2 setup are available: STD and 12mm NPN capacitive bed level sensor (CPL).

For the STD one, quite sure that you will find a better version here : https://github.com/MarlinFirmware/Configurations/ and search for Zonestar/P802M (exactly the same as the Tronxy).


## Branch name : 
- release/x.x.x-STD : tested with firmware x.x.x for a standard out of the box Tronxy 802M printer
- release/x.x.x-CPL : tested with firmware x.x.x for a P802M with a 12mm Capacitive Sensor (LJ12A3-4-Z/BX) for bed leveling (need a metal bed to work properly).


# Install Marlin 2 on a Tronxy P802M (or a ZoneStar)
First, if you have a stock printer and you want to install Marlin 2, you might have a big problem: your card is not detected by Arduino IDE.
That's because there is no bootloader on this cheap board.

So, you have to install a bootloader on the printer. This is not easy, but this can be done.

you have 2 solutions:
  - using a Rasberry Pi as an AVR.
  - using a USBtinyISP AVR or similar.
  
Then you will be able to flash your printer.
  
## Hardware configuration

You might have a small, cheap board on your printer : The Melzi 2.0 (Mine is a 2.0 V5, but this should work for other versions)
At the bottom of the board, you may have (or not) a jumper
<p align="center"><img src="/images/JumperWrite.png" height="250" alt="Jumper Write" /></p>

Note the 6 pins connector on the left, you will use it to flash the board with the ISP.

it must be on to allow the write off the bootloader on the board.
If you don't have it, you can solder a jumper (recycled from and old board) or solder a cable.

Now, you can write on your board if you put the jumper on, and **you have to**

## Install a bootloader with an AVR

### with a raspberry
you'll find a lot of exemple using google like this one:
https://learn.adafruit.com/program-an-avr-or-arduino-using-raspberry-pi-gpio-pins/installation?view=all
Quite long but complete.

### with a USBtinyISP
same, a lot of examples, a good complete one:
https://www.makeuseof.com/how-to-install-an-arduino-bootloader/


## Install Marlin

Now, in Arduino IDE -> preferences add this bonard support:
https://raw.githubusercontent.com/Lauszus/Sanguino/master/package_lauszus_sanguino_index.json

then restart arduino IDE
and in tools -> type of card, choose Sanguino.
Then in tools -> processor, choose ATMEL 1284P 16Mhz.
Choose the serial port where you have your printer (depend of your OS and config)

then download the Marlin 2.0 firmware: (take the latest zip or the one corresponding to this branch)
https://github.com/MarlinFirmware/Marlin/tags

unzip it, go into Marlin2.1.2/Marlin and overwrite the configuration.h with the one of this project.
You can also take the official ZoneStar P802M config from if you have a stock printer:
https://github.com/MarlinFirmware/Configurations/

then open the project with arduino IDE (open the Marlin.ino file)

compile, upload, enjoy.

You may have an unstable temperature for your extruder. Sometimes, you need to autotune it. 

Send this command to your printer: (I do it with octoprint)

M303 E0 S205 C10 ; This will run autotune for extruder 1 (Extruder 1 is E0) at 205°C for a total of 10 iterations.

at the end, you will have a result showing the new values for Kp/Ki/Kd (this is the PID).
example:
#define DEFAULT_Kp  12.52
#define DEFAULT_Ki   0.45
#define DEFAULT_Kd  87.94

then edit the configuration.h, save, compile and upload again. your printer is now tuned.

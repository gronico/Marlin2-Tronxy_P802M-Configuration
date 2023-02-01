# Marlin2-Tronxy_P802M-Configuration
Marlin's Configuration files for Tronxy P802M 3D printer. 2 setup are available: STD and 12mm NPN capacitive bed level sensor (CPL).

For the STD one, quite sure that you will find a better version here : https://github.com/MarlinFirmware/Configurations/ and search for Zonestar/P802M (exactly the same as the Tronxy).


## Branch name : 
- release/x.x.x-STD : tested with firmware x.x.x for a standard out of the box Tronxy 802M printer
- release/x.x.x-CPL : tested with firmware x.x.x for a P802M with a 12mm Capacitive Sensor (LJ12A3-4-Z/BX) for bed leveling (need a metal bed to work properly).


# Install Marlin 2 on a Tronxy P802M (or a ZoneStar)
First, if you have a stock printer and you want to install Marlin 2, you have to install a bootloader on the printer. And this is not easy.
you have 2 solutions:
  - using a Rasberry Pi as an ISP.
  - using a USBtinyISP or similar.
  
Then you will be able to flash your printer.
  
## Hardware configuration

You might have a small, cheap board on your printer : The Melzi 2.0 (Mine is a 2.0 V5, but this should work for other versions)
At the bottom of the board, you may have (or not) a jumper
<p align="center"><img src="/images/JumperWrite.png" height="250" alt="MarlinFirmware's logo" /></p>

Note the 6 pins connector on the left, you will use it to flash the board.

it must be on to allow the write off the bootloader on the board.
If you don't have it, you can solder a jumper (recycled from and old board) or solder a cable.


Before using the library, you should key down the PWRKEY until the SIM800 is powerded on.

## Hardware
If you are using a Raspberry Pi Model 1 A+/B+, Model 2/3 B or Zero then this add-on board will connect directly to the 40-pin GPIO.
If you are using an Model 1 A/B with a 28-pin GPIO connector then you will have to connect the board to the Pi with ribbon cable
or dupont connectors as the composite video and audio connectors are in the way. Only the follow seven pins need to be connected:

| Pin | Function |
| --- | --- |
| 1   | 3.3V |
| 2 | 5V |
| 6 | GND |
| 8 | TXD |
| 10 | RXD |
| 11 | SIM800 Power |
| 12 | SIM800 Reset |

## Software
This library has been tested with Python 3.4.2 running on a Raspberry Pi Model B (Rev.2) with Raspbian Jessie Lite (2016-05-27).
It depends on PySerial and  Ben Croston's RPi.GPIO which can be installed (if not already) as follows:

```
$ sudo apt-get update
$ sudo apt-get install python3-rpi.gpio
$ sudo pip3 install pyserial
```

The file `sms.py` is both the library and a working example if read/executed:

```
$ sudo python3 sms.py
```


Support for Pi3
There is now a device tree file called pi3-miniuart-bt which makes the Raspberry Pi 3 disable the Bluetooth and map pl011 UART on pins 14 and 15 as before.

Step 1 - Install Raspbian Jessie onto a SD card and boot the Pi when connected to a network

Login via terminal or desktop and shell

Configure the system with:

sudo raspi-config

Expand filesystem and enable serial on advanced page, exit and reboot.

Update the system with:

sudo apt-get update
sudo apt-get upgrade

Step 2:  Device Tree settings as below:

Add device tree to /boot/config.txt to disable the Raspberry Pi 3 bluetooth.

sudo nano /boot/config.txt

Add at the end of the file

dtoverlay=pi3-miniuart-bt

Exit the editor saving your changes and then:

sudo reboot

Enabling the Serial Console Rasbian Jessie after 18th March 2016 release

To enable the serial console, you need to edit the /boot/cmdline.txt file

sudo nano /boot/cmdline.txt

Change the file to the following:

dwc_otg.lpm_enable=0 console=tty1 console=serial0,115200 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait

Exit and save your changes

sudo apt-get update
sudo apt-get install python3-rpi.gpio
sudo pip3 install pyserial

The file `sms.py` is both the library and a working example if read/executed:

 sudo python3 sms.py


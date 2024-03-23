## dbus_ubms
 CANBUS to dbus bridge for a Valence U-BMS to provide battery monitor service on Victronenergy Venus OS
 The idea here is to use a CAN-USB converter connected to the USB port of a Raspberry running VenusOS or Victron device directly.

 Note: I have personally used this on a Victron Cervo GX with a USB-Converter connected to a USB port.
 <img width="342" alt="image" src="https://github.com/aguerrejoaquin/dbus_ubms/assets/132913905/3ff1d289-ec77-4b8e-8e78-0eb32ecf9fd4">


 Use this code at your own risk.
## Installation

Depending if you are using a Raspi or a Victron device (ex: Cerbo GX) you will need to use different codes to install this library. 

## Installation on Raspi
```
with git:
 opkg install git
 git clone https://github.com/gimx/dbus_ubms.git
 cd dbus_ubms/ext
 git clone https://github.com/victronenergy/velib_python.git

or download the above projects as archives, copy and unzip to root home
```

## Install git on Victron

Install git
```
 /opt/victronenergy/swupdate-scripts/resize2fs.sh
 opkg update
 opkg install git
```

Clone library
```
 git clone https://github.com/aguerrejoaquin/dbus_ubms.git
 cd dbus_ubms/ext
 git clone https://github.com/victronenergy/velib_python.git
```

## Preparation on Raspi
```
 sudo apt-get install libgtk2.0-dev  libdbus-1-dev libgirepository1.0-dev python-gobject python-can
 sudo pip install dbus-python can pygobject
```

## Preparation on Victron
```
 cd
 dbus_ubms/prep_ubms.sh
```

## Run from command line
Check with the "ifconfig" for the CAN number port (ex: can0). You will need to know the CAN port that your USB converter is assigned. 

```
 python dbus_ubms.py -i can0 -v 29.0 -c 650
 or
 nohup python dbus_ubms.py -i can0 -v 29.0 -c 650 &
```

## Run as a service: 
```
 ln -s /home/root/dbus_ubms/service /service/dbus-ubms.can0
 cp rc.local /data/rc.local
 svc -u /service/dbus-ubms.can0
```


## Configuration of U-BMS
```
 set SOC calculation to minimum (not average)
 set voltage scaling factor to 1
 set VMU slave mode (error on timeout maybe on or off)
 configure C3 to single discharge/charge contactor, ie no separate charge path, no pre-charge, no on/off charge control
 connect C3 (and route battery + through it)
 connect battery voltage
 connect CAN and CAN 5V supply
 connect +12V for System and Ignition
 in a system with x modules in series and multiple in parallel, module numbers 1 to x have to be assigned to one string, pack voltage calculation depends on this 
``` 
   

## Credits
 - Majority of the protocol reverse engineering work was done by @cogito44 http://cogito44.free.fr
 - This code has been developed using information from the following (re-)sources
   - https://github.com/victronenergy/venus/wiki/howto-add-a-driver-to-Venus
   - https://github.com/victronenergy/venus/wiki/dbus#battery
   - https://github.com/victronenergy/velib_python
   - https://groups.google.com/forum/#!msg/victron-dev-venus/nCrpONiWYs0/-Z4wnkEJAAAJ;context-place=forum/victron-dev-venus
   - /opt/victronenergy/vrmlogger/datalist.py
   - https://groups.google.com/forum/#!searchin/victron-dev-venus/link$20to$20service%7Csort:date/victron-dev-venus/-AJzKTxk-3k/fOt707ZeAAAJ


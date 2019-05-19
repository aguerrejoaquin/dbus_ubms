##dbus_ubms
 CANBUS to dbus bridge for a Valence U-BMS to provide battery monitor service on Victronenergy Venus OS

 Use this code at your own risk.
## Installation
```
with git:
 opkg install git
 git clone https://github.com/gimx/dbus_ubms.git
 cd dbus_ubms/ext
 git clone https://github.com/victronenergy/velib_python.git

or download the above projects as archives, copy and unzip to root home
```

## Preparation on Raspi
```
 sudo apt-get install libgtk2.0-dev  libdbus-1-dev libgirepository1.0-dev python-gobject python-can
 sudo pip install dbus-python can pygobject
```

## Preparation on CCGX
```
 dbus_ubms/prep_ubms.sh
```

## Run from command line
```
 python dbus/dbus_ubms.py -i can0
 or
 nohup python dbus/dbus_ubms.py -i can0 &
```

## Run as a service: 
```
 opkg install custom-rc.d
 ln -s ./dbus_ubms/service /service/dbus-ubms.can0
 cp ./dbus_ubms/rc.local /data/rc.local
```

## Configuration of U-BMS
```
 set SOC calculation to minimum (not average)
 set voltage scaling factor to 1
 configure C3 to single discharge/charge contactor, ie no separate charge path, no pre-charge, no on/off charge control
 connect C3 (and route battery + through it)
 connect battery voltage
 connect CAN and CAN 5V supply
 connect +12V for System and Ignition
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


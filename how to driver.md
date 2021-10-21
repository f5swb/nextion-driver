HOW TO INSTALL THE NEXTION DRIVER

log in to your Pi-Star with SSH

RPI-RW



sudo rm /usr/lcoal/bin/NextionDriver

get the software
Then: cd /tmp

git clone https://github.com/on7lds/NextionDriverInstaller.git

go !

sudo NextionDriverInstaller/install.sh

Checking the installing (on Pi-Star)

You will notice that in the MMDVMHost beyond the Nextion part of that page, there are some additions regarding this Nextion Interface:
Check your software settings in Pi-Star:

Goto the Expert Page => MMDVMHost Editor (or mmdvmhost.ini file) to the Nextion part

    check/set in the Nextion part, the driver at /dev/ttyNextionDriver (USB adapter) or /dev/ttyAMA0 (connected to GPIO-RPi)
    check/set in the NextionDriver part
        Port: /dev/ttyUSB0 (for USB adapter) or /dev/ttyAMA0 (connected to the GPIO pins of RPi)****
        LogLevel: 2
        DataFilesPath: /usr/local/etc/
        GroupsFile: groups.txt
        DMRidFile: stripped.csv
  
  Sending commands from the display
Execute a linux command:

    2A F0 (linux command) FF FF FF

The 'linux command' is executed.
Execute a linux command: with feedback:

   2A F1 (linux command) FF FF FF
or
   2A F1 (number) (linux command) FF FF FF

The 'linux command' is executed and the FIRST line of the result is sent to the display variable 'msg'

After executing the linux command, status.val=24 is sent and S0.click is triggered. This allows the display to process the command result, if necessary.

If the third byte, (number) is present (with number 1..31), the result of the command will not be returned in msg.txt, but in the variable resultXX.txt where XX = the number that was given.

Example : 2A F1 05 date FF FF FF wil return the date/time in result05.txt

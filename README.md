# TFMini-Plus
#### Arduino Library for the Benewake TFMini-Plus Lidar sensor

The Benewake TFMini-Plus is a unique product and not merely an enhanced version of the TFMini. It has its own command and data structure. Therefore, this Arduino TFMini-Plus library is not compatible with the TFMini product.

The Plus features a UART serial communication interface. The serial baud rate is programmable.
<br />Only these rates are supported: 9600, 14400, 19200, 56000, 115200, 460800, and 921600.

Data output rates are programmable up to 10KHz, but the internal measuring frame rate is fixed at 4KHz.
<br />"Standard" output rates are: 1, 2, 5, 10, 20, 25, 50, 100, 125, 200, 250, 500, and 1000Hz.
<br />If the output rate is set to 0 (zero), single measurements can be triggered by command.

The default format for each frame of data consists of three measuremnets:
<br />&nbsp;&nbsp;&#9679;&nbsp;  Distance to target in centimeters. Range: 0 - 1200
<br />&nbsp;&nbsp;&#9679;&nbsp;  Strength of return signal in arbitrary units. Range: 0 - 65535
<br />&nbsp;&nbsp;&#9679;&nbsp;  Temperature of the device


The device is set by default to a 115200 baud rate and a 100Hz data frame rate.
Upon power-up it will immediately begin to send measurement data.
Use the library's 'getData( dist, flux, temp)' function to pass back measurement data and return system status.
Fewer errors will occur if the rate of data sampling roughly matches the output data frame rate.

Use the library's 'buildCommand( cmnd, param)' function to send a command and a parameter to the device.
The function returns a status or error code.  A command (cmnd) must be selected from the library's list
of twelve defined commands. A parameter (param) may be entered directly as an unsigned 32bit number,
but it is better to choose from the library's defined parameters because **an erroneous parameter can block communication and there is no external means of resetting the device to factory defaults.**

An example Arduino sketch "TFMP_example.ino" is included.

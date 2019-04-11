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

The 'begin()' function passes a serial stream to the library and returns a boolean value (TRUE/FALSE) whether serial data is available. The function also sets a public one byte status/error code. Status codes are defined within the library.

The 'getData( dist, flux, temp)' function passes back three measurement values.  It returns a boolean value and also sets the status byte.  If no serial data or no 'header' code are received within 1 second, the command returns an error.  Version 1.3.2 flushes the serial buffer before reading, which improves performance asynchronous code.

The 'sendCommand( cmnd, param)' function sends a 32bit command and a 32bit parameter to the device. It returns a boolean value and also sets the status byte.  A command (cmnd) must be selected from the library's list of twelve defined commands. A parameter (param) may be entered directly as an unsigned number, but it is better to choose from the Library's defined parameters because **an erroneous parameter can block communication and there is no external means of resetting the device to factory defaults.**

Any change of device settings (frame rate or baud rate) must be followed by a SAVE_SETTINGS command or the changed values will be lost when power is removed.  SYSTEM_RESET and RESTORE_FACTORY_SETTINGS do not require a SAVE_SETTINGS command.

Benewake is not forthcoming about the internals of the device, however they did share this.
>Some commands that modify internal parameters are processed within 1ms. Some commands require the MCU to communicate with other chips may take several ms. And some commands, such as saving configuration and restoring the factory need to erase the FLASH of the MCU, which may take several hundred ms.

An example Arduino sketch "TFMP_example.ino" is included.

# ZKLibrary
ZKLibrary is PHP library for reading and writing data to attendance device using UDP protocol. This library is useful to comunicate between web server and attendance device directly without any addition program.
This library is implemented in the form of class. So that you can create an object and use it functions.

## Example

<?php

include "zklibrary.php";

$zk = new ZKLibrary('192.168.1.102', 4370);

$zk->connect();

$zk->disableDevice();

$zk->testVoice();

$zk->enableDevice();

$zk->disconnect();

?>


---
# ZKLibrary
## Data Structrure
```php
Class ZKLibrary{
String ip;
Unsigned Short port;
Unsigned Long socket;
Unigned Long session_id;
String received_data;
String user_data[][];
String attendance_data[][];
Unsigned Long timeout_sec;
Unsigned Long timeout_usec;
}
```
## Functions
```php
__construct([$ip[, $port]])
```
Object constructor
### Parameter
$ip is ip address of device

$port is UDP port of device

```php
__destruct()
```
Object destructor

```php
connect([$ip[, $port]])
```
Function to make connection to the device. If ip address and port is not defined yet, this function must take it. Else, this function return FALSE and does not make any connection.
### Parameters
$ip is ip address of device

$port is UDP port of device

```php
disconnect()
```
Function to disconnect to the device. If ip address and port is not defined yet, this function must take it. Else, this function return FALSE and does not make any changes.
```php
setTimeout([$sec[, $usec]])
```
Set timeout for socket connection.
### Parameters

```php
reverseHex($input)
```
Reverse hexadecimal digits.
```php
encodeTime($time)
```
Encode time to binary data.
```php
decodeTime($data)
```
Decode binary data to time
```php
checkSum($p)
```
This function calculates the chksum of the packet to be sent to the time clock.
```php
createHeader($command, $chksum, $session_id, $reply_id, $command_string)
```
Create data headerto be sent to the device
### Parameters
```php
checkValid($reply)
```
Check wether reply is valid or not
```php
execCommand($command, $command_string = '', $offset_data = 8)
```
Send command and data packet to the device and receive some data if any.
```php
getSizeUser()
```
Get number of user.
```php
getSizeAttendance()
```
Get number of attendance log.
```php
restartDevice()
```
Restart the device.
```php
shutdownDevice()
```
Shutdown the device.
```php
sleepDevice()
```
Sleep the device.
```php
resumeDevice()
```
Resume the device.
```php
changeSpeed($speed = 0)
```
Change transfer speed of the device. 0 = slower. 1 = faster.
```php
writeLCD($rank, $text)
```
Write text on LCD.
### Parameters
```php
clearLCD()
```
Clear text from LCD.
```php
testVoice()
```
Test voice of the device.
```php
getVersion()
```
Get device version.
```php
getOSVersion($net = true)
```
Get OS version.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setOSVersion($osVersion)
```
Set OS version
### Parameters
$osVertion

Version of operating version
```php
getPlatform($net = true)
```
Get OS version.
### Parameters
$net
If net set to true, function will return netto data without parameter name.
```php
setPlatform($patform)
```
Set platform
### Parameters
$platform

Platform name.
```php
getFirmwareVersion($net = true)
```
Get firmware version.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setFirmwareVersion ($firmwareVersion)
```
Set firmware version.
### Parameters
$firmwareVersion

The version of firmware.
```php
getWorkCode($net = true)
```
Get work code.
### Parameters
$net
If net set to true, function will return netto data without parameter name.
```php
setWorkCode($workCode)
```
Set work code.
### Parameters
$workCode

Work code.

```php
getSSR($net = true)
```
Get SSR
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setSSR($ssr)
```
Set SSR.
### Parameters
$ssr

SSR.
```php
getPinWidth($net = true)
```
Get pin width.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setPinWidth($pinWidth)
```
Set pin width.
### Parameters
$pinWidth

Pin width
```php
getFaceFunctionOn($net = true)
```
Check wether face detection function is available or not.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setFaceFunctionOn ($faceFunction)
```
Set wether face detection function is available or not.
### Parameters
$faceFunction

Face function. 1 = available; 2 = not available.
```php
getSerialNumber($net = true)
```
get serial number of the device.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setSerialNumber($serialNumber)
```
Set serial number of the device.
### Parameters
$serialNumber

Serial number of the device.
```php
getDeviceName($net = true)
```
Get device name.
### Parameters
$net

If net set to true, function will return netto data without parameter name.
```php
setDeviceName($deviceName)
```
Set device name.
### Parameters
$deviceName
The device name.
```php
getTime()
```
Get time of device from real time clock (RTC). The time resolution is one minute.
### Return Value
getTime return time as string with format YYYY-MM-DD HH:II:SS.
```php
setTime($t)
```
Set time of the device.
### Parameters
Time to be set with format YYYY-MM-DD HH:II:SS.
```php
enableDevice()
```
Ensure the machine to be at in the normal work condition, generally when data communication shields the machine auxiliary equipment (keyboard, LCD, sensor), this order restores the auxiliary equipment to be at the normal work condition. 
```php
disableDevice()
```
Shield machine periphery keyboard, LCD, sensor, if perform successfully, there are showing “working” on LCD.
```php
enableClock()
```
Set the LCD dot (to glitter ‘:’) the packet data part transmit 0 to stop glittering, 1 start to glitter. After this order carries out successfully, the firmware will refresh LCD.
```php
getUser()
```
Retrive the user list from the device.
### Return Value
getUser return array 2 dimension. The key of array is serial number of user. The value of array is array containing: id, name, role, password.
setUser($uid, $userid, $name, $password, $role)
Write user to the device.
###Parameters
$uid

Serial number of user. This is the unsigned short number (2 bytes)

$userid

User ID used by the application. The maximum length of $userid is 8 characters containing numeric whithout zero on the beginning.

$name

User name. The maximum length of $name is 28 characters nontaining alpha numeic and some (not all) punctuation

$role

The role of user. The length of $role is 1 byte. Possible value of $role is:
```
0 = LEVEL_USER
2 = LEVEL_ENROLLER
12 = LEVEL_MANAGER
14 = LEVEL_SUPERMANAGER
```
```php
clearUser()
```
Delete all user from the device.
```php
deleteUser($uid)
```
Delete some user from the device.
#Parameters
$uid

Serial number of the user (2 bytes)
```php
deleteUserTemp($uid, $finger)
```
Delete finger template of the user.
###
Parameters
$uid

Serial number of the user (2 bytes)

$finger

The number of finger (0-9)
```php
clearAdmin()
```
Delete all admin from the device.
```php
getAttendance()
```
Retrieve the attendance log.
### Return Value
getAttendance return array 2 dimension. The value of array is array containing
```php
clearAttendance()
```
Delete all attendance log.

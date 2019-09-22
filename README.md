# Headless PiHole with LCD

## Prerequisites
Install xserver video drivers.  
```Bash
apt install xserver-xorg-video-fbturbo
```
## Enable LCD sleep after **x** seconds
Check the current setting
```Bash
cat /sys/module/kernel/parameters/consoleblank
```

Here, consoleblank is a kernel parameter. In order to be permanently set, it needs to be defined on the kernel command line.

```Bash
vi /boot/cmdline.txt
```
Add **consoleblank=0** to turn screen blanking off completely, or edit it to set the number of seconds of inactivity before the console will blank. Note the kernel command line must be a single line of text.
### White LCD
If the LCD stays white. Check if this error occurs
```Bash
dpkg: dependency problems prevent configuration of xserver-xorg-input-evdev:
 xserver-xorg-input-evdev depends on libevdev2 (>= 0.9.1); however:
  Package libevdev2 is not installed.
 xserver-xorg-input-evdev depends on libmtdev1 (>= 1.1.0); however:
  Package libmtdev1:armhf is not installed.

dpkg: error processing package xserver-xorg-input-evdev (--install):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 xserver-xorg-input-evdev
```
To fix this problem (TODO)

## Setup touch screen
Install touch screen driver
```Bash
apt install libts-bin
```

Create exports and start calibration
```Bash
export TSLIB_TSDEVICE=/dev/input/event0  
export TSLIB_FBDEVICE=/dev/fb1
ts_calibrate
```
### Wake up screen
via SSH
```Bash
echo -ne "\033[13]" > /dev/tty1
```

---
Sources:  
https://www.raspberrypi.org/documentation/configuration/screensaver.md

http://www.circuitbasics.com/raspberry-pi-touchscreen-calibration-screen-rotation/

https://github.com/jpmck/PADD
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
Add consoleblank=0 to turn screen blanking off completely, or edit it to set the number of seconds of inactivity before the console will blank. Note the kernel command line must be a single line of text.

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
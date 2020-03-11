# Headless PiHole with LCD

## Supplier Instructions
About the system of 3.5 touch screen
The screen can be used for Raspberry Pi 4/3B+/3B/2B 
The touch screen need to configure the driver to use , it is suitable for Raspbian/Ubuntu/Kali-linux , if you use for other system , you need to congigure by yourself.

We provide the configure method :

- Step 1：Download the Raspbian IMG
[https://www.raspberrypi.org/downloads/raspbian/]

- Step 2: Burn the system image
If you don't know how to do that,you can refer to the Raspberry Pi office tutorial

- Step 3: Open terminal(SSH) and install the driver on RaspberryPi
(tested on RaspberryPi 4B,3B+,3B,2B,2B+,1B,ZERO)

Run:
```
sudo rm -rf LCD-show

git clone https://github.com/goodtft/LCD-show.git

chmod -R 755 LCD-show

cd LCD-show/

sudo ./LCD35-show
```
Wait a few minutes, when the system reboot , it will work.

You can also download the system image which we already configured well by the end of this links :
[http://www.lcdwiki.com/3.5inch_RPi_Display]

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
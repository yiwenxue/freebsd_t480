# Run FreeBSD on ThinkPad T480
## Hardware Specs
The following is the hardware list of thinkpad t480.
* **Cpu**: Intel texttel core i5-8250
* **Gpu**: Intel UHD Graphics 620
* **Ram**: 32GB(16GBx2) DDR4 2400MHz (Kingston)
* **Storage**: 512GB SSD (Samsung 860 pro)
* **Wireless**: Intel Wireless-AC 8265
* **Ethernet**: Intel Corporation Ethernet Connection I219-V
* **Dock**: ThinkPad Thunderbolt Workstation Dock 2

  

| Hardware & Function | works? | need config? | description |
| :------------------ | ------ | ------------ | ----------- |
| Ethernet            | yes    | no           |             |
| Wifi                | yes    | no           |             |
| Bluethooth          | no     | ---          |             |
| Graphics            | yes    | yes          |             |
| Microphone          | yes    | unknown      |             |
| Sound               | yes    | no           |             |
| Webcam              | yes    | yes          |             |
| Suspend & Resume    | yes    | yes          |             |

And the Dock station:

 

| Hardware & Function | works? | need conf ? | description |
| ------------------- | ------ | ----------- | ----------- |
| VGA                 | yes    | no          |             |
| Ethernet            | yes    | no          |             |
| Usb                 | yes    | no          |             |

## Basic Setup

### Prepare install usb stick

FreeBSD has three type of versions:

* Current --- Not stable, but with new features.

* Release --- Stable

* Stable --- Stablest 

  I chose 12.1-RELEASE.  

1. Usb stick & download image.\
   You can download official install image [here](http://ftp.freebsd.org/pub/FreeBSD/snapshots/ISO-IMAGES/12.1/). Choose the amd64*memstick.img, but amd64*memstick.img.xz is better.

2. Burn with dd 

	```bash
	dd if=FreeBSD*amd64-memstick.img of=/dev/sda* bs=1M conv=sync
	```

### Bios Setup

1. Disable Secure Boot
* Security > Secure Boot
     * Secure Boot: Enabled -> Disabled
2. Disable TPM
* Security > Security Chip
     * Security Chip: Enabled -> Disabled
3. Disable Bluetooth
* Security > I/O Port Access
     * Bluetooth: Enabled -> Disabled

### Install Base system

1. Boot from usb

2. Then install FreeBSD base system.\

   That is easy, just follow the installer.

3. Reboot

## Further Configurations

### Network & Wireless

### Graphic & X system
A graphic desktop would be necessary for daily use. We have many options. We have two popular options: WM(window manager) and DE(desktop environment).
* DE:
	- Gnome: Not uptodate. Only 3.28.
	- KDE: Uptodate and beautiful, but not stable 😑️.
	- Xfce4 
* WM:
	- DWM: The most suckless wm, but you need cood, patches are annoying.
	- Xmonad: Many functions, but haskell programming needed.
	- i3WM: widely used, easy to config (just copy from github 😉️).
	- Awesome: Also has many functions, and easy to config.

If you use WM, a DM(Desktop manager) would be required.
* DM:
	- slim
	- SDDM
	- GDM
	- XDM

Install:
* Install graphic driver and load it.\
After this, the resolution of your tty should be larger. If so, modify rc.conf to load this module at startup. The changes will work at next boot.
	```bash
	pkg install drm-kmod # you can also install from ports.
	kldload i915-kmod.ko
	```
	```bash
	echo kld_list = '/boot/module/i915-kmod.ko'
	``` 
* Install the desktop

	```bash
	pkg install xorg xfce4 slim
	```
* Cerate ~/.xinitrc
	```bash
	exec startxfce4
	```
* Then test Xorg. If the system starts a xfce4 session, one can goto the next step.
	```bash 
	startx
	```
* Enable system servers
	```bash
	sysrc dbus_enable=YES
	sysrc hald_enable=YES
	sysrc slim_enable=YES

	service dbus start
	service hald start
	service slim start
	```


### Softwares
* Browser 
	- Chromium
	- Firefox
* Terminal
	- Urxvt
	- Termite
* GIMP
* ThunderBird
* Inkscape
* VIM || Emacs
* Rhythmbox 
* Vscode


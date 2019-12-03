# Run FreeBSD on ThinkPad T480

## Install Base System
* Usb stick & download image.

  You can download official install image [here](http://ftp.freebsd.org/pub/FreeBSD/snapshots/ISO-IMAGES/12.1/). Choose the amd64*memstick.img, but amd64*memstick.img.xz is better.

* Burn with dd

  > dd if=FreeBSD*amd64-memstick.img of=/dev/sda* bs=1M conv=sync
* boot from usb
## Network & Wireless
    You can config network with bsdconfig. It's a convinent tool.

## Graphic & X system
    You will need a kernel level driver(drm-fbsd-kmod)) and a user level driver(xf86-video-intel). 

 >  Don't put kld_list+="/boot/modules/i915kms.ko" into /etc/rc.conf before a necessery test. (Your computer will boot then shutdown -- dead-loop).(this driver in pkg repo will shutdown your computer once you load it.)
 
    pkg install drm-fbsd12.0-kmod 

 >   run this command instead
 
    cd /usr/ports/graphics/drm-kmod && make install clean 
 
    kldload /boot/modules/i915kms.ko \
    pkg install xorg xf86-video-intel openbox xdm 

 >  You can start the next step -- configuration. create /usr/local/etc/X11/xorg.conf.d/20-intel.conf

    Section "Device" 
        Identifier "Card0"
        Driver "intel"
        Option "DPMS"
        Option "AccelMethod" "uxa"
        Option "TearFree" "true" 
    EndSection

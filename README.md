# Run FreeBSD on ThinkPad T480

## Install Base System
* Usb stick & download image.
        You can download official install image [here](http://ftp.freebsd.org/pub/FreeBSD/snapshots/ISO-IMAGES/12.1/). Choose the amd64*memstick.img, but amd64*memstick.img.xz is better.
* Burn with dd 
    <bash>
    dd if=FreeBSD*amd64-memstick.img of=/dev/sda* bs=1M conv=sync
* boot from usb
## Network & Wireless

## Graphic & X system
* drm-fbsd-kmod

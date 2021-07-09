# raspberrypi-SPI
resources on SPI protocol and raspberry pi
* https://www.raspberrypi.org/documentation/hardware/raspberrypi/spi/README.md
* https://elinux.org/RPi_SPI

## initial configuration
in /boot/config.txt:
```
dtparam=spi=on
```
Reference on dtoverlay params in config.txt : https://github.com/raspberrypi/firmware/blob/master/boot/overlays/README

## use flashrom to read/write SPI flash

Command to dump flash:
```
/sbin/flashrom -V -f -c W25Q80.V -p buspirate_spi:dev=/dev/ttyUSB0,spispeed=1M -r test.bin
```
`-f -c W25Q80.V` is used to force a device type in case it is not autodetected by flashrom (ie BergMicro 25Q80)

## SPI-NOR flash direct support
http://events17.linuxfoundation.org/sites/events/files/slides/An%20Introduction%20to%20SPI-NOR%20Subsystem%20-%20v3_0.pdf
apparently direct support for SPI-nor flash (such as winbond 25QXX) via /dev/mtdX, /dev/mtdblockX, /proc/mtd.  
Add `dtoverlay=jedec-spi-nor,flash-spi0-0` to config.txt (https://raspberrypi.stackexchange.com/questions/22695/accessing-spi-flash-from-dev)

## boot from SPI flash?
https://www.raspberrypi.org/forums/viewtopic.php?t=288131

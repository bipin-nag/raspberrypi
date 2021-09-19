# Installation

1. Visit https://openwrt.org/toh/raspberry_pi_foundation/raspberry_pi

2. Download proper image for your Pi.

   - 3b/3b+: http://downloads.openwrt.org/releases/21.02.0/targets/bcm27xx/bcm2710/openwrt-21.02.0-bcm27xx-bcm2710-rpi-3-ext4-factory.img.gz

3. Download and install imager: https://www.raspberrypi.org/blog/raspberry-pi-imager-imaging-utility/

4. Flash USB drive with the extracted image file from step 2.

5. Mount the USB drive and edit cmdline.txt. Change the boot device from mmcblk0p2 to sda2.

6. Boot from USB drive to OpenWrt

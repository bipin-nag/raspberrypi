# Raspberry Pi 4 Model B

## [<span class="icon icon-link"></span>](#video-walkthrough)Video Walkthrough

To see a live demo of this writeup, see the video below:

<iframe width="560" height="315" src="https://www.youtube.com/embed/aHu1lFir7UU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen=""></iframe>

## [<span class="icon icon-link"></span>](#prerequisites)Prerequisites

You will need

*   `talosctl`
*   an SD card

Download the latest alpha `talosctl`.

    curl -Lo /usr/local/bin/talosctl https://github.com/talos-systems/talos/releases/latest/download/talosctl-$(uname -s | tr "[:upper:]" "[:lower:]")-amd64
    chmod +x /usr/local/bin/talosctl

## [<span class="icon icon-link"></span>](#updating-the-eeprom)Updating the EEPROM

At least version `v2020.09.03-138a1` of the bootloader (`rpi-eeprom`) is required. To update the bootloader we will need an SD card. Insert the SD card into your computer and use [Raspberry Pi Imager](https://www.raspberrypi.org/software/) to install the bootloader on it (select Operating System > Misc utility images > Bootloader > SD Card Boot). Alternatively, you can use the console on Linux or macOS. The path to your SD card can be found using `fdisk` on Linux or `diskutil` on macOS. In this example, we will assume `/dev/mmcblk0`.

    curl -Lo rpi-boot-eeprom-recovery.zip https://github.com/raspberrypi/rpi-eeprom/releases/download/v2021.04.29-138a1/rpi-boot-eeprom-recovery-2021-04-29-vl805-000138a1.zip
    sudo mkfs.fat -I /dev/mmcblk0
    sudo mount /dev/mmcblk0p1 /mnt
    sudo bsdtar rpi-boot-eeprom-recovery.zip -C /mnt

Remove the SD card from your local machine and insert it into the Raspberry Pi. Power the Raspberry Pi on, and wait at least 10 seconds. If successful, the green LED light will blink rapidly (forever), otherwise an error pattern will be displayed. If an HDMI display is attached to the port closest to the power/USB-C port, the screen will display green for success or red if a failure occurs. Power off the Raspberry Pi and remove the SD card from it.

> Note: Updating the bootloader only needs to be done once.

## [<span class="icon icon-link"></span>](#download-the-image)Download the Image

Download the image and decompress it:

    curl -LO https://github.com/talos-systems/talos/releases/latest/download/metal-rpi_4-arm64.img.xz
    xz -d metal-rpi_4-arm64.img.xz

## [<span class="icon icon-link"></span>](#writing-the-image)Writing the Image

Now `dd` the image to your SD card:

    sudo dd if=metal-rpi_4-arm64.img of=/dev/mmcblk0 conv=fsync bs=4M

## [<span class="icon icon-link"></span>](#bootstrapping-the-node)Bootstrapping the Node

Insert the SD card to your board, turn it on and wait for the console to show you the instructions for bootstrapping the node. Following the instructions in the console output to connect to the interactive installer:

    talosctl apply-config --insecure --interactive --nodes <node IP or DNS name>

Once the interactive installation is applied, the cluster will form and you can then use `kubectl`.

> Note: if you have an HDMI display attached and it shows only a rainbow splash, please use the other HDMI port, the one closest to the power/USB-C port.

## [<span class="icon icon-link"></span>](#retrieve-the-kubeconfig)Retrieve the `kubeconfig`

Retrieve the admin `kubeconfig` by running:

    talosctl kubeconfig

## [<span class="icon icon-link"></span>](#troubleshooting)Troubleshooting

The following table can be used to troubleshoot booting issues:

<table>

<thead>

<tr>

<th>Long Flashes</th>

<th align="center">Short Flashes</th>

<th align="right">Status</th>

</tr>

</thead>

<tbody>

<tr>

<td>0</td>

<td align="center">3</td>

<td align="right">Generic failure to boot</td>

</tr>

<tr>

<td>0</td>

<td align="center">4</td>

<td align="right">start*.elf not found</td>

</tr>

<tr>

<td>0</td>

<td align="center">7</td>

<td align="right">Kernel image not found</td>

</tr>

<tr>

<td>0</td>

<td align="center">8</td>

<td align="right">SDRAM failure</td>

</tr>

<tr>

<td>0</td>

<td align="center">9</td>

<td align="right">Insufficient SDRAM</td>

</tr>

<tr>

<td>0</td>

<td align="center">10</td>

<td align="right">In HALT state</td>

</tr>

<tr>

<td>2</td>

<td align="center">1</td>

<td align="right">Partition not FAT</td>

</tr>

<tr>

<td>2</td>

<td align="center">2</td>

<td align="right">Failed to read from partition</td>

</tr>

<tr>

<td>2</td>

<td align="center">3</td>

<td align="right">Extended partition not FAT</td>

</tr>

<tr>

<td>2</td>

<td align="center">4</td>

<td align="right">File signature/hash mismatch - Pi 4</td>

</tr>

<tr>

<td>4</td>

<td align="center">4</td>

<td align="right">Unsupported board type</td>

</tr>

<tr>

<td>4</td>

<td align="center">5</td>

<td align="right">Fatal firmware error</td>

</tr>

<tr>

<td>4</td>

<td align="center">6</td>

<td align="right">Power failure type A</td>

</tr>

<tr>

<td>4</td>

<td align="center">7</td>

<td align="right">Power failure type B</td>

</tr>

</tbody>

</table>
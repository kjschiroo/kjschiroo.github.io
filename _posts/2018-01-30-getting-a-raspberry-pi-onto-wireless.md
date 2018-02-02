---
layout: post
title: "Setting up wireless on a headless Raspberry Pi Zero W"
date: 2018-01-30
comments: true
---
# Flash the SD card #
You'll need an 8 GB or larger SD card to support Raspbian. Download a [Raspbian Light](https://www.raspberrypi.org/downloads/raspbian/) image. The Standard Raspbian with Desktop will also work, but since the whole point is to be headless the desktop doesn't really do much good and takes up extra space.

Once you have the image, download and run [Etcher](https://etcher.io/). It's the most convenient way that I've found so far to image an SD card. In the "Select image" dialog select the Raspbian zip file that you just downloaded. If you only have one SD/USB drive plugged in it should automatically select the drive to flash. Take a moment to confirm that it is the drive you're expecting, once you hit 'Flash!' anything on that drive is gone.

# Adding wifi credentials #
After the SD card has been successfully flashed open it in your system's file explorer. You should see two volumes `boot` and `rootfs`. Create a file named `wpa_supplicant.conf` in the root of the `boot` volume and add in the network details as shown below.
```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="Your_wifi_network_name"
    psk="wifi_password"
    id_str="arbitrary_id_that_you_pick"
}
```
If you want to setup wifi for multiple networks just assign multiple values to `network` and use a different value for `id_str`.

# Enabling ssh #
In the root of the `boot` volume create an empty file called `ssh`. This will enable ssh access. The default credentials for Raspian are username `pi` and password `raspberry`.

_Warning: There is a directory in the `rootfs` volume named `boot`, this is NOT what you want. You want the root of the `boot` volume_.

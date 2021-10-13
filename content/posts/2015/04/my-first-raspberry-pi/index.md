---
title: My First Raspberry Pi
post_id: 74
date: '2015-04-03T06:57:08+00:00'
taxonomy:
    migration-status: review
tags: [computer,english,raspberrypi,computer,english,raspberrypi]
categories:
  - English
---
Earlier this week my first [Raspberry Pi](http://raspberrypi.org/) arrived by mail. What a great little device. I intend to use it to replace my Mac Mini. That Mac is currently running an [openHAB](http://openhab.org/) server. Where the previous model B was said to be somewhat slow for larger openHAB installations, the hardware specs of this new [Raspberry Pi 2 model B](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/) have increased. I expect it to be faster and fast enough for  my purposes.

To get it up and running, I [downloaded the latest Raspbian](http://downloads.raspberrypi.org/raspbian_latest) and installed it on an SD card using the [command line installation instructions for Mac](http://www.raspberrypi.org/documentation/installation/installing-images/mac.md). I had to wait impatiently for the `dd` command to finish, since the disk image is 3GB in size.

After I inserted the SD-card I immediately plugged in the network cable and the power adapter and let the Pi boot. How satisfying those LEDs looked.

To complete the initial installation I SSH’ed to the Pi from a Terminal with command

 
    ssh pi@<ip-address>


to run the configration tool (where *\\<ip-address>* is the dynamically assigned IP4 address e.g. “x.x.x.x”)

 
    sudo raspi-config


In the tool I expanded the file system to all of my 16GB flash card, changed the default password for the ‘pi’ user and used the  internationalisation option to set the locale to ‘nl-UTF8’ en the timezone to ‘Europe/Amsterdam’.
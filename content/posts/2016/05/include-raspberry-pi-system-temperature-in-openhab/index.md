---
title: 'Include Raspberry Pi System Temperature in openHAB'
date: '2016-05-13 14:00:00'
tags:
    - domotica
    - openhab
    - raspberrypi
    - computer
    - english
syndicateto: 
    - 'https://github.com/openhab/openhab1-addons/wiki/Raspberry-Pi-System-Temperature'
categories:
    - English
---

*(This post is also contributed to the openHAB wiki)*

The [Systeminfo Binding](https://github.com/openhab/openhab/wiki/Systeminfo-Binding) enables you to read system information through [Sigar](http://sigar.hyperic.com/). The system information provided through this library can be extended with some additional important features. For example, reading system temperatures for your Raspberry Pi.

**CPU temperature**

The CPU temperature can be read with a terminal command:
 
 ```bash
$ cat /sys/class/thermal/thermal_zone0/temp
46540
```

This output can be captured using the Exec binding. The value returned represents millidegrees Celsius. (I’m not sure if another OS localization returns Fahrenheit). So the actual needed CPU temperature is computed through a Javascript transformation.

**GPU temperature**

The GPU temperature can be read with a terminal command:

 ```bash
$ /opt/vc/bin/vcgencmd measure_temp
temp=47.1'C
```

This output can also be captured using the Exec binding. The value returned is surrounded by text for readability that can be removed through a Regex transformation.

This example gets both temperatures in degrees Celsius every 60 seconds and persistently stores them for presenting in a graph. It assumes that all items containing system information (potentially including those for the Systeminfo Binding are in a `systems.items` file (any other items file will do).

## Example configuration

### Assumptions

- OpenHAB has been installed on Raspberry Pi
- The [Exec binding](https://github.com/openhab/openhab/wiki/Exec-Binding) has been installed
- [RRD4J persistence](https://github.com/openhab/openhab/wiki/RRD4J-persistence) has been installed

### Add openhab user to video group

The user `openhab` needs to be member of the `video` group to be able to run the `vcgencmd` command. Otherwise you will see a [VCHI initialization failed](http://raspberrypi.stackexchange.com/questions/7546/munin-node-plugins-vchi-initialization-failed) error message.

Group memberships are only updated after a reboot.

 
    $ sudo usermod -a -G video openhab
    $ sudo reboot now


### Create javascript transformation

Create a `milli.js` file (in transform folder) with this content:

 ```javascript
(function(i){ return i / 1000; })(input)
```

### Add new items

Add to `system.items` file:

 
    // System temperatures
    Group  System_Temperature_Chart (System, Charts)
    Number System_Temperature_Chart_Period "Periode" (System)
    Number System_Temperature_CPU "Temperature CPU [%.1f °C]" <temperature> (System_Temperature_Chart) { exec="<[cat /sys/class/thermal/thermal_zone0/temp:60000:JS(milli.js)]" }
    Number System_Temperature_GPU "Temperature GPU [%.1f °C]" <temperature> (System_Temperature_Chart) { exec="<[/opt/vc/bin/vcgencmd measure_temp:60000:REGEX(temp=(.*?)'C)]" }


### Add persistence for items

Add to `rrd4j.persist` file:

 
    System_Temperature_Chart* : strategy = everyChange, everyMinute, restoreOnStartup


### Update sitemap

Add to `default.sitemap` file:

 
    Text item=System_Temperature_CPU label="Temperature [%.1f °C]" {
        Frame {
            Text item=System_Temperature_CPU
            Text item=System_Temperature_GPU
        }
        Frame {
            Switch item=System_Temperature_Chart_Period mappings=[0="1h", 1="4h", 2="8h", 3="12h", 4="24h"]
            Chart  item=System_Temperature_Chart period=h   refresh=60000 visibility=[System_Temperature_Chart_Period==0, System_Temperature_Chart_Period=="Uninitialized"]
            Chart  item=System_Temperature_Chart period=4h  refresh=60000 visibility=[System_Temperature_Chart_Period==1]
            Chart  item=System_Temperature_Chart period=8h  refresh=60000 visibility=[System_Temperature_Chart_Period==2]
            Chart  item=System_Temperature_Chart period=12h refresh=60000 visibility=[System_Temperature_Chart_Period==3]
            Chart  item=System_Temperature_Chart period=D   refresh=60000 visibility=[System_Temperature_Chart_Period==4]
        }
    }


## Sources

- [OpenHAB Community Thread](https://community.openhab.org/t/4964)

This solution was developed for a [Raspberry Pi 2 model B]({% post\_url 2015-04-03-my-first-raspberry-pi %}) running [Raspbian](https://www.raspberrypi.org/downloads/raspbian/)) and an [apt-get installation](https://github.com/openhab/openhab/wiki/Linux-and-OS-X#apt-get) of openHAB.
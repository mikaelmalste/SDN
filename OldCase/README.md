# Case

Create SDN-network with three Raspberry Pi-switches and two Access-Points. This documentation is for inbound management connection to Access-Points. In order to create this setup case, follow these instructions below.

![Topology](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/topologia3.png)

### Devices

List of devices needed. You can find used versions from __[here](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/Random/versions.md).__

* [Cisco Catalyst 2950 Switch](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/Cisco/README.md)
* [PfSense Firewall](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/PfSense/final.md)
* [Puikkari SDN-controller](https://cybertrust.labranet.jamk.fi/cf2017/overflow/wikis/puikkari/installation)
* [3 Raspberry Pi Switches](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/RaspberrySwitches/README.md)
* [2 Raspberry Pi Access-Points](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/RaspberryAccessPoint/README.md)

## Puikkari installation

You can find Puikkari installation documentation from [here](https://cybertrust.labranet.jamk.fi/cf2017/overflow/wikis/puikkari/installation).

## PfSense installation

You can find PfSense installation documentation from [here](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/PfSense/summary.md).

## Raspberry-Pi switches installation

First you have to install NOOBS to your Raspberry Pi. [Here](https://www.raspberrypi.org/help/noobs-setup/2/) is simple instructions for install process.
You can find Raspberry-Pi switches installation documentation from [here](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/RaspberrySwitches/README.md).

## Raspberry-Pi Access-Points installation

First you have to install NOOBS to your Raspberry Pi. [Here](https://www.raspberrypi.org/help/noobs-setup/2/) is simple instructions for install process.
You can find Raspberry-Pi Access-Points installation documentation from [here](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/RaspberryAccessPoint/README.md).

### IP-Addresses

| Device | Address  |
|:-------------:|:-------------:|
| PfSense |192.168.1.1|
| Puikkari | 192.168.1.100 |
| Raspi1 | 192.168.1.11 |
| Raspi2 | 192.168.1.12 |
| Raspi3 | 192.168.1.13 |
| AP1 | DHCP |
| AP2 | DHCP |

### Usernames and passwords

|Device| Username | Password  |
|:-------------:|:-------------:|:-------------:|
|Cisco Switch|cisco|cisco|
|PfSense|admin|pfsense|
|Puikkari|puikkari|puikkari|
|Access-Points|pi|raspberry|
|Switches|pi|raspberry|

## Conclusions

After many weeks of troubleshooting, we decided to add second cable from AP2 to controller. We followed instructions from two theses and still our network didn't work. 
There were very strange problems where traffic didn't came back to AP2.
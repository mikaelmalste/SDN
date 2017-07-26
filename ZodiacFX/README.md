# First topology with four Zodiac-switches

## Case

Create SDN-network with four Zodiac FX-switches and two Raspberry Pi Access-Points. We create two subnets, one for Management traffic (MGNT) and the second for client traffic (Data). Management network uses 192.168.1.x subnet and Data network uses 10.0.0.x subnet.

## Issues

After building and configuring the physical network, host-devices (Access-Points) can't communicate with each other. 

### Devices

List of devices needed. You can find used versions from __[here](https://github.com/mikaelmalste/SDN/blob/master/Random/versions.md).__

* [Cisco Catalyst 2950 Switch](https://github.com/mikaelmalste/SDN/blob/master/Cisco/README.md)
* [PfSense Firewall](https://github.com/mikaelmalste/SDN/blob/master/PfSense/final.md)
* [Puikkari SDN-controller](https://cybertrust.labranet.jamk.fi/cf2017/overflow/wikis/puikkari/installation)
* [4 Zodiac FX switches](https://github.com/mikaelmalste/SDN/blob/master/ZodiacFX/Zodiac_conf.txt)
* [2 Raspberry Pi Access-Points](https://github.com/mikaelmalste/SDN/blob/master/RaspberryAccessPoint/final.md)

### IP-Addresses

| Device | Address  |
|:-------------:|:-------------:|
| PfSense |192.168.1.1|
| Puikkari | 192.168.1.100 |
| Zodiac ACM0 | 192.168.1.11 |
| Zodiac ACM1 | 192.168.1.12 |
| Zodiac ACM2 | 192.168.1.13 |
| Zodiac ACM3 | 192.168.1.14 |
| Raspi1 | DHCP |
| Raspi2 | DHCP |

### First topology:

PfSense's main function is to serve as Firewall, DHCP-server and routing point in our network. All switches have straight connection to SDN-controller throught Cisco Catalyst 2950-switch. Switches communicate with controller via OpenFlow-protocol. Every Zodiac FX-switch has dedicated port for Management-traffic (Port4).

![First topology](https://github.com/mikaelmalste/SDN/blob/master/pictures/topologia1.png?raw=true)

### Usernames and passwords
|Device| Username | Password  |
|:-------------:|:-------------:|:-------------:|
|Cisco Switch|cisco|cisco|
|PfSense|admin|pfsense|
|Puikkari|puikkari|puikkari|
|Access-Points|pi|raspberry|

## Conclusions

After many days of troubleshooting, we desided to simplify our network by using only two Zodiac FX-switches. After restarting controller and resetting the database, we didn't found any solutions for our problem.

# Second topology with two Zodiac-switches

## Case

Create SDN-network with two Zodiac FX-switches and one Raspberry Pi Access-Points. We create two subnets, one for Management traffic (MGNT) and the second for client traffic (Data). Management network uses 192.168.1.x subnet and Data network uses 10.0.0.x subnet.

## Issues

We decided to capture traffic from Puikkari controller and analyze the TCPDUMP-file in Wireshark.

### Devices

List of devices needed. You can find used versions from __[here](https://github.com/mikaelmalste/SDN/blob/master/Random/versions.md).__

* [Cisco Catalyst 2950 Switch](https://github.com/mikaelmalste/SDN/blob/master/Cisco/README.md)
* [PfSense Firewall](https://github.com/mikaelmalste/SDN/blob/master/PfSense/final.md)
* [Puikkari SDN-controller](https://cybertrust.labranet.jamk.fi/cf2017/overflow/wikis/puikkari/installation)
* [4 Zodiac FX switches](https://github.com/mikaelmalste/SDN/blob/master/ZodiacFX/Zodiac_conf.txt)
* [2 Raspberry Pi Access-Points](https://github.com/mikaelmalste/SDN/blob/master/RaspberryAccessPoint/final.md)

### IP-Addresses

| Device | Address  |
|:-------------:|:-------------:|
| PfSense |192.168.1.1|
| Puikkari | 192.168.1.100 |
| Zodiac ACM1 | 192.168.1.11 |
| Zodiac ACM2 | 192.168.1.12 |
| Raspi1 | DHCP |

### Second topology:

PfSense's main function is to serve as Firewall, DHCP-server and routing point in our network. All switches have straight connection to SDN-controller throught Cisco Catalyst 2950-switch. Switches communicate with controller via OpenFlow-protocol. Every Zodiac FX-switch has dedicated port for Management-traffic (Port4).
![Second topology](https://github.com/mikaelmalste/SDN/blob/master/pictures/topologia2.png?raw=true)

### Usernames and passwords

|Device| Username | Password  |
|:-------------:|:-------------:|:-------------:|
|Cisco Switch|cisco|cisco|
|PfSense|admin|pfsense|
|Puikkari|puikkari|puikkari|
|Access-Point|pi|raspberry|

## Conclusions

After hours of analyzing the traffic capture, we figure out that the Group Mod action was the cause of all our problems. Zodiac FX-switches don't have support for Group Mod action. We updated the firmware to latest version, but that didn't fix the issue. [Here](https://github.com/NorthboundNetworks/ZodiacFX/issues/81) is the link for our problem that is posted as an issue to Zodiac FX forum.

<img src="https://github.com/mikaelmalste/SDN/blob/master/pictures/grp_mod.png?raw=true" width="800" />

Screen capture of Group Mod error from Wireshark.

<img src="https://github.com/mikaelmalste/SDN/blob/master/pictures/grp_mod_error.png?raw=true" width="800" />

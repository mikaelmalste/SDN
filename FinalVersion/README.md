# Final topology

Final working solution was to separate Management and Data interfaces to their own physical network interfaces.
By doing this we were able to isolate issue caused by VLANs, and focus on WLAN implementation.

We also configured RADIUS authentication and Captive Portal- services running on PfSense.

![Topology](https://github.com/mikaelmalste/SDN/blob/master/pictures/topologia4.png?raw=true)

### Devices

List of devices needed. You can find used versions from __[here](https://github.com/mikaelmalste/SDN/blob/master/Random/versions.md).__

* [Cisco Catalyst 2950 Switch](https://github.com/mikaelmalste/SDN/blob/master/Cisco/README.md)
* [PfSense Firewall](https://github.com/mikaelmalste/SDN/blob/master/PfSense/final.md)
* [Puikkari SDN-controller](https://github.com/mikaelmalste/SDN/wiki/Puikkari-installation)
* [3 Raspberry Pi Switches](https://github.com/mikaelmalste/SDN/blob/master/RaspberrySwitches/README.md)
* [2 Raspberry Pi Access-Points](https://github.com/mikaelmalste/SDN/blob/master/RaspberryAccessPoint/final.md)

## Puikkari installation

You can find Puikkari installation documentation from [here](https://github.com/mikaelmalste/SDN/wiki/Puikkari-installation).

## PfSense installation

You can find PfSense installation documentation from [here](https://github.com/mikaelmalste/SDN/blob/master/PfSense/final.md).

## Raspberry-Pi switches installation

First you have to install NOOBS to your Raspberry Pi. [Here](https://www.raspberrypi.org/help/noobs-setup/2/) is simple instructions for install process. 
You can find Raspberry-Pi switch installation instructions [here](https://github.com/mikaelmalste/SDN/tree/master/RaspberrySwitches#raspberry-pi-switches-installation).

__New front-end (Puikkari) port configurations can be found below.__

## Puikkari front-end configurations

Open Puikkari front-end from your browser. Address is your network interfaces address. For example in this documentation the address is 192.168.51.133.

<img src="https://github.com/mikaelmalste/SDN/blob/master/pictures/interface_conf.png?raw=true" width="600" />

You can edit port configurations by double clicking the switch.

### Raspi1

|Port|Port State|Priority|Traffic Match|Port Configuration|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Eth1|Internal|1||{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth2|Internal|1||{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|

### Raspi2

|Port|Port State|Priority|Traffic Match|Port Configuration|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Eth1|Edge|1|||
|Eth2|Internal|1||{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth3|Internal|1||{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth4|Edge|1|{"vlan_vid":5}|{"retag_vlan":true,"untag_vlan":true,"vlan":100}|

### Raspi3

|Port|Port State|Priority|Traffic Match|Port Configuration|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Eth1|Internal|1||{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth2|Internal|1||{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth3|Internal|1||{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|

### Access-Point2 (Br2)

|Port|Port State|Priority|Traffic Match|Port Configuration|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Eth0|Internal|1||{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Wlan0|Edge|1||||

### Access-Point1 (Br0)

|Port|Port State|Priority|Traffic Match|Port Configuration|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Eth0|Internal|1||{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|vEth11|Edge|1||||

## Raspberry-Pi Access-Points installation

First you have to install NOOBS to your Raspberry Pi. [Here](https://www.raspberrypi.org/help/noobs-setup/2/) is simple instructions for install process.
You can find Raspberry-Pi Access-Points installation instructions [here](https://github.com/mikaelmalste/SDN/blob/master/RaspberryAccessPoint/final.md).

### IP-Addresses

| Device | Address  |
|:-------------:|:-------------:|
| PfSense |192.168.1.1|
| Puikkari | 192.168.1.100 |
| Raspi1 | 192.168.1.11 |
| Raspi2 | 192.168.1.12 |
| Raspi3 | 192.168.1.13 |
| AP1 | 192.168.1.14 |
| AP2 | 192.168.1.15 |

### Usernames and passwords

|Device| Username | Password  |
|:-------------:|:-------------:|:-------------:|
|Cisco Switch|cisco|cisco|
|PfSense|admin|pfsense|
|Puikkari|puikkari|puikkari|
|Access-Points|pi|raspberry|
|Switches|pi|raspberry|

# Video taken from login and testing network

You can watch the video [here](https://github.com/mikaelmalste/SDN/blob/master/pictures/Wlan_cp_connection).

__[Here](https://github.com/mikaelmalste/SDN/blob/master/pictures/final_optimization.ogv) you can watch how links are optimized between different traffic.__

![Final links](https://github.com/mikaelmalste/SDN/blob/master/pictures/final_links.png)

Colors indicate how much traffic is going through the links.

### Demo

Demo video can be viewed from YouTube.

[![Demo](https://img.youtube.com/vi/EUBPUdrJnrI/0.jpg)](https://www.youtube.com/watch?v=EUBPUdrJnrI "Puikkari Demo")


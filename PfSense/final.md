# Summary for PfSense installation

Here you can find summary for installation of PfSense. For installing PfSense [here](https://doc.pfsense.org/index.php/Installing_pfSense) is simple instructions for that.

## Interface configurations

Wan-interface is for internet connection, Management-interface is for control traffic, Data-interface is for end-customer traffic.

![Interfaces](https://github.com/mikaelmalste/SDN/blob/master/pictures/interfaces2.png?raw=true)

## DNS

DNS-addresses from your network.

![DNS](https://github.com/mikaelmalste/SDN/blob/master/pictures/dns.png?raw=true)

## DHCP

DHCP-server address-scope is from **192.168.2.20** to **192.168.2.254**

![DHCP](https://github.com/mikaelmalste/SDN/blob/master/pictures/dhcp.png?raw=true)

## Firewall rules

Traffic between Management and Data networks is blocked. See rule below.

![Firewall rules](https://github.com/mikaelmalste/SDN/blob/master/pictures/firewall_rules.png?raw=true)

## MTU

After some six weeks of testing, we found out that 1478 is the right number. This is because VLAN (802.1Q) frame takes 22 extra bytes, increasing MTU size to total of 1522, which we need to substract from 1500 (1478 = 1500 - (1522 - 1500)) totaling MTU size back to 1500 if VLAN tag is added.

![MTU](https://github.com/mikaelmalste/SDN/blob/master/pictures/mtu.png?raw=true)

## FreeRADIUS

Add a new user which can login to the WLAN.

![User](https://github.com/mikaelmalste/SDN/blob/master/pictures/radius_user.png?raw=true)

Add interface address for RADIUS. This should be same as your DATA-interface address.

![Interface](https://github.com/mikaelmalste/SDN/blob/master/pictures/radius_int.png?raw=true)

## NAT

Create NAT rule for outbound-traffic. Choose Automatic outbound NAT.

![NAT](https://raw.githubusercontent.com/mikaelmalste/SDN/master/pictures/nat.png)

## Captive Portal

Captive Portal configuration. You can download our login page [here](https://github.com/mikaelmalste/SDN/blob/master/Random/index.php).

Download login page and add it.

![Login page](https://raw.githubusercontent.com/mikaelmalste/SDN/master/pictures/login_page.png)

Use RADIUS authentication and CHAP-MD5 protocol. Add RADIUS-server IP-address, port and password.

![Captive Portal1](https://github.com/mikaelmalste/SDN/blob/master/pictures/captive1.png?raw=true)

After succesful connection, login page appears. Here is an example of our login page.

![Captive Portal2](https://github.com/mikaelmalste/SDN/blob/master/pictures/captive2.png?raw=true)



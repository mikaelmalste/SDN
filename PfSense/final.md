# Summary for PfSense installation

Here you can find summary for installation of PfSense. For installing PfSense [here](https://doc.pfsense.org/index.php/Installing_pfSense) is simple instructions for that.

## Interface configurations

Wan-interface is for internet connection, Management-interface is for control traffic, Data-interface is for end-customer traffic.

![Interfaces](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/interfaces2.png)

## DNS

DNS-addresses from your network.

![DNS](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/dns.png)

## DHCP

DHCP-server address-scope is from **192.168.2.20** to **192.168.2.254**

![DHCP](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/dhcp.png)

## Firewall rules

Traffic between Management and Data networks is blocked. See rule below.

![Firewall rules](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/firewall_rules.png)

## MTU

After some six weeks of testing, we found out that 1478 is the right number. This is because VLAN (802.1Q) frame takes 22 extra bytes, increasing MTU size to total of 1522, which we need to substract from 1500 (1478 = 1500 - (1522 - 1500)) totaling MTU size back to 1500 if VLAN tag is added.

![MTU](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/mtu.png)

## FreeRADIUS

Add a new user which can login to the WLAN.

![User](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/radius_user.png)

Add interface address for RADIUS. This should be same as your DATA-interface address.

![Interface](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/radius_int.png)

## NAT

Create NAT rule for outbound-traffic. Choose Automatic outbound NAT.

![NAT](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/nat.png)

## Captive Portal

Captive Portal configuration. You can download our login page [here](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/Random/index.php).

Download login page and add it.

![Login page](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/login_page.png)

Use RADIUS authentication and CHAP-MD5 protocol. Add RADIUS-server IP-address, port and password.

![Captive Portal1](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/captive1.png)

After succesful connection, login page appears. Here is an example of our login page.

![Captive Portal2](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/captive2.png)



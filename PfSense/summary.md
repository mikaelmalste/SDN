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
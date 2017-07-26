# Access-Point 2 configuration


__To issue these commands, you need to install [openvswitch](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/RaspberryAccessPoint/README.md#openvswitch-installation) and [hostapd](https://cybertrust.labranet.jamk.fi/cf2017/overflow/blob/master/RaspberryAccessPoint/README.md#hostapd-configuration) first.__

Create openvswitch bridge using commands below. Include interfaces eth1 and wlan0 to this bridge.

```
ovs-vsctl add-br br2
ovs-vsctl add-port br2 eth1
ovs-vsctl add-port br2 wlan0
ovs-vsctl set-controller br2 tcp:192.168.1.100:6633
```

Configure management interface eth0 to etc/network/interfaces file. 
```
auto eth0
iface eth0 inet static
address 192.168.1.15
netmask 255.255.255.0
gateway 192.168.1.1
```

Configure hostapd.conf file to look like this. __Do not include bridge=br2 to this configuration file__, because wlan0 is connected to bridge via add-port- command. For this reason wlan interface can not use password or radius authentication, instead users authenticate via captive portal which uses radius to authenticate users.

__Note: There propably will be update on hostapd in the future which allows bridging on ovs-bridge. Un-official patch for hostapd can be found [here](https://github.com/helmut-jacob/hostapd).__

Due to lack of time we didn't have time to test this solution.
```
auth_algs=1
interface=wlan0
driver=nl80211
ssid=SDN-testi
hw_mode=g
ieee80211n=1
channel=10
```

# Raspberry Pi 3 access point installation
Topology where access point is going to be created. These configurations are going to be implemented to two access points. 

![Topology](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/topologia3.png)

First of all update your blank Raspberry device.
```
sudo apt-get update
sudo apt-get upgrade
```
This command installs all needed software to Open vSwitch.
```
root@raspberrypi:/home/pi# sudo apt-get install -y autoconf libtool openssl pkg-config make gcc 
libssl-dev
```
Sparse is needed so install it by git-command. Notice that after installation pull back from /sparse directory.
```
root@raspberrypi:/home/pi# git clone git://git.kernel.org/pub/scm/devel/sparse/sparse.git
root@raspberrypi:/home/pi# cd sparse
root@raspberrypi:/home/pi/sparse# make
root@raspberrypi:/home/pi/sparse# make install
root@raspberrypi:/home/pi# cd ..
```
Clone Open vSwitch from git and run boot.sh script and define directory to configurations.
```
git clone https://github.com/openvswitch/ovs.git
cd ovs/
sudo apt-get install dh-autoreconf
sudo ./boot.sh
sudo ./configure --prefix=/usr --localstatedir=/var --sysconfdir=/etc
```
If Raspberry warns that python is missing module-six try running these commands.
```
apt-get install python-pip
pip install six
make –j3
make install
```
Finally copy openvswitch-switch template and start Open vSwitch.
```
root@raspberrypi:cp debian/openvswitch-switch.init /etc/init.d/openvswitch-switch
root@raspberrypi:/etc/init.d/openvswitch-switch start
```
If Open vSwitch doesnt start try to re-run commands.
#### Open vSwitch configuration
Now device is ready to create virtual interfaces witch are connected to virtual switches. Create bridge br1 and add interfaces to it. Also add access points controller with ip address and port.
```
ip link add veth00 type veth peer name veth11
ovs-vsctl add-br br1
ovs-vsctl add-port br1 eth0
ovs-vsctl add-port br1 veth11
ovs-vsctl set-controller br1 tcp:192.168.1.100:6633
```
#### Bridge-utils configuration
Install bridge-utils software and create second bridge to wlan and veth00 interfaces.
```
apt-get install bridge-utils
brctl addbr br0
brctl addif br0 wlan0
brctl addif br0 veth00
```
#### Hostapd configuration
Start by installing hostapd and creating hostapd.conf file to run with it.
```
sudo apt-get install hostapd
sudo nano /etc/hostapd/hostapd.conf
```
Add created hostapd.conf file to /etc/default/hostapd directory, see line below.
```
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```
Configure lines below to hostapd.conf file to create open Wlan.

![Hostapd file](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/hostapd.png)

Configure bridge interfaces to /etc/network/interfaces file.

![Interfaces configuration](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/interfaces.png)

Make sure that br1 gets ip address from DHCP-server.
```
sudo ip addr flush dev br1
sudo ifdown br1 
sudo ifup br1
start hostapd service.
```
Start hostapd service.
```
sudo /usr/sbin/hostapd /etc/hostapd/hostapd.conf
```

If all configurations are ok, then you should see something like below:

![AP-ENABLED](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/hostapd-start.png)
### Crontab
To start all these services when restarting Raspberry configure crontab to look like this.
![Crontab -e](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/crontab.png)

### RC.local

Also add these two lines to /etc/rc.local. These commands are run at the end of device starting process.

![RC.local](https://cybertrust.labranet.jamk.fi/cf2017/overflow/raw/master/pictures/rclocal.png)

### Create virtual interface with vlan-tag

```
ip link add link <interface> name <interface.x> type vlan id x
```

Verify your virtual interface using command below.

```
ip -d link show <interface>.x
```

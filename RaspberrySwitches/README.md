# Raspberry Pi switches installation

Here you can find documentation for Raspberry Pi switches.

#### Openvswitch installation guide

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

### Example configuration from Raspi1:

```
ovs-vsctl add-br br0
ovs-vsctl add-port br0 eth1
ovs-vsctl add-port br0 eth2
ovs-vsctl add-port br0 eth3
ovs-vsctl set-controller br0 tcp:192.168.1.100:6633
```

### Port configurations to Puikkari front-end
Configure these settings to the Puikkari front-end. Please notice: Check port numbers from every device using command: 
```
sudo ovs-ofctl show <your bridge name>
```

### Port configurations

Raspi1

|Port|Port State|Priority|Traffic Match|Port Configuration|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Eth1|Internal|1|    |{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth2|Internal|1|    |{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth3|Edge|1|   |{"vlan":100}|

Raspi2

|Port|Port State|Priority|Traffic Match|Port Configuration|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Eth1|Edge|1|    |    |
|Eth2|Internal|1|    |{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth3|Internal|1|    |{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth4|Edge|1|{"vlan_vid":5}|{"retag_vlan":true,"untag_vlan":true,"vlan":100}|
|vEth4|Internal|555|    |{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|

Raspi3

|Port|Port State|Priority|Traffic Match|Port Configuration|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Eth1|Disabled|    |    |    |
|Eth2|Internal|1|    |{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|Eth3|Internal|1|    |{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|

Access-Point

|Port|Port State|Priority|Traffic Match|Port Configuration|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Eth0|Internal|1|    |{"lldp_listen":true,"lldp_send":true,"lldp_send_interval":2}|
|vEth11|Edge|1|    |    |


### Useful commands

Use the command below. Command shows if your switch is in <b>in-band mode</b>. If you can find lines where `action=NORMAL`, your switch is at <b>in-band mode</b>.

```
ovs-appctl bridge/dump-flows <your bridge name>
```

Change all of your Raspi-switches to the <b>out-of-band</b> mode using command below.

```
ovs-vsctl set controller <your bridge name> connection-mode=out-of-band
```

If you want to monitor flows from your switches, use command below.
```
watch -n 0.5 'sudo ovs-ofctl dump-flows <your bridge name>'
```
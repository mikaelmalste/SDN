# Port configurations to Puikkari front-end
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
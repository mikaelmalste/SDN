
## Switches and Access-Points

Use these commands to verify versions used.

```
sudo ovs-vswitchd --version
sudo ovs-ofctl --version
sudo uname -romn
sudo lsb_release -a
```

|Device|Name|Openvswitch Version|Openflow version|OS-version|
|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|Raspberry1|Raspi1|2.7.90|0x1:0x4|Raspbian GNU/Linux 8.0 (jessie)|
|Raspberry2|Raspi2|2.7.90|0x1:0x4|Raspbian GNU/Linux 8.0 (jessie)|
|Raspberry3|Raspi3|2.7.90|0x1:0x4|Raspbian GNU/Linux 8.0 (jessie)|
|RaspberryAP1|AP1|2.7.90|0x1:0x4|Raspbian GNU/Linux 8.0 (jessie)|
|RaspberryAP2|AP2|2.7.90|0x1:0x4|Raspbian GNU/Linux 8.0 (jessie)|

## PfSense

|Device|Name|FreeRADIUS version|OS-version|
|:-------------:|:-------------:|:-------------:|:-------------:|
|PfSense|PfSense|1.7.9|2.3.4|

## Puikkari components

Use these commands to verify versions used.

```
ryu-manager --version
sudo psql -V
go version
python --version
python3 --version
npm --version
sudo docker --version
sudo nginx -v
redis-server --version
rabbitmqctl status
```

|Component name|Version|
|:-------------:|:-------------:|
|Ryu-manager|4.13|
|PostgreSQL|9.5.7|
|Go|1.7.4|
|Python|2.7.12|
|Python3|3.5.2|
|NPM|3.8.6|
|Docker|17.06.0-ce|
|Nginx|1.10.3|
|Redis|3.2.9|
|RabbitMQ|3.6.10|
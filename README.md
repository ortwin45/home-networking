# home-networking
Memory for home network settings

## SSH

To avoid entering your password each time you connect with SSH, yYou can send your public key to the ssh server using ``ssh-copy-id``.



## Networking

The hostname is stored under ``/etc/hostname``. It shouldn't include the domain name.

In your access point, you can let DHCP assign the same IPs based on the MAC of your NIC or on the hostname. This is stored in the file ``/etc/dnsmasq.conf``. 

````
interface=eth0
listen-address=192.168.128.1
bind-interfaces
server=8.8.8.8
server=8.8.4.4
domain-needed
bogus-priv
expand-hosts
domain=local.ojothepojo.be
dhcp-range=192.168.128.4,192.168.128.254,12h
dhcp-lease-max=25
dhcp-host=mobilityplus,192.168.128.100
dhcp-host=G5,192.168.128.50
dhcp-host=OJO-DELL,192.168.128.51
````


## TP-Link extender

When rebooting the TP-link extender, use the ad-hoc wifi and open the page on [http://192.168.0.254](http://192.168.0.254)


## Home network architecture

````
Internet <-> Proximus router ))  (( TP-link Wifi Extender )))  ((( RPI 3 Bridge <-> Ethernet <-> Ethernet Switch <-> Devices

<--------------------  192.168.1.0/24  -------------------------->              <-----------  192.168.128.4/24  ----------->
````

### RPI 3 Bridge

Follow the instructions [here](https://www.maketecheasier.com/turn-raspberry-pi-into-wi-fi-bridge).

The following is appended to ``/etc/dnsmasq.conf``
````
interface=eth0
listen-address=192.168.128.1
bind-interfaces
server=8.8.8.8
server=8.8.4.4
domain-needed
bogus-priv
expand-hosts
domain=local.ojothepojo.be
dhcp-range=192.168.128.4,192.168.128.254,12h
dhcp-lease-max=25
dhcp-host=mobilityplus,192.168.128.100
dhcp-host=G5,192.168.128.50
````

Also, you can add port forwarding to a server on the subnet. For example for Kibana: 

````shell
sudo iptables -A PREROUTING -t nat -i wlan0 -p tcp --dport 5601 -j DNAT --to 192.168.128.111:5601
````
You can see the complete iptables config using sudo iptables -v -t nat
````shell
sudo iptables -t nat -L -n -v
sudo iptables -L -n -v
````

### Disable wifi on the RPI
When the ethernet cable is connected, no need for wifi anymore. 
````
sudo ifconfig wlan0 down
````
This only disables it until reboot. 

## SD Cards


| Card Number   | OS                       | Hardware     | Size   | Hostname     | ip              | Remarks      | User    |
| ------------- | ------------------------ | ------------ | ------ | ------------ | --------------- | ------------ | ------- |
| 1             | Retropie                 | Rpi 4B       | 64 GB  | retropie     | 192.168.128.120 |              | pi      |
| 2             | Ubuntu 20.04 Server      | Rpi 4B       | 64 GB  | duvel        | 192.168.128.110 |              | ubuntu  |
| 3             | Ubuntu 20.04 Server      | Rpi 4B       | 64 GB  | vedett       | 192.168.128.111 |              | ubuntu  |
| 4             | Raspberry Pi OS (32 bit) | Rpi 3B       |  8 GB  | mobilityplus | 192.168.128.100 |              | pi      |
| 5             | Raspberry Pi OS (32 bit) | Rpi 3B       | 16 GB  | ap           | 192.168.128.1   | Access point | pi      |
| 6             | OpenWRT                  | Rpi 4B       | 64 GB  | openwrt      | 192.168.?????   | Access point | root    |


## RPI tips

### HDMI Hot plug

Update the ``/boot/config.txt`` with the following: 
````
hdmi_force_hotplug=1
hdmi_drive=2
````
This might also work on Ubuntu, though you have to create the file yourself. 

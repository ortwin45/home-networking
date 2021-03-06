# home-networking
Memory for home network settings

## SSH

To avoid entering your password each time you connect with SSH, yYou can send your public key to the ssh server using ``ssh-copy-id``.



## Networking

The hostname is stored under ``/etc/hostname``. It shouldn't include the domain name.

In your access point, you can let DHCP assign the same IPs based on the MAC of your NIC or on the hostname. This is stored in the file ``/etc/dnsmasq.conf``. 

````shell
...
dhcp-host=66:d5:95:a9:de:38,192.168.4.32 # RPI
dhcp-host=66:d5:95:de:e5:43,192.168.4.9 # Dell XPS Ubuntu
...
````

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

Another way is to map based on the hostname using the ``/etc/hosts`` file. 
````
127.0.0.1	localhost
::1		localhost ip6-localhost ip6-loopback
ff02::1		ip6-allnodes
ff02::2		ip6-allrouters
192.168.4.32	mobilityplus
192.168.4.40	vedett
192.168.4.41	duvel
````


## TP-Link extender

When rebooting the TP-link extender, use the ad-hoc wifi and open the page on [http://192.168.0.254](http://192.168.0.254)

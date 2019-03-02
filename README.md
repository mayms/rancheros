#Install
```bash
sudo ros install -c https://raw.githubusercontent.com/mayms/rancheros/master/cloud-config.yml -d /dev/sda
```

#Add host-only nic
##On host
'''
ipconfig

Windows-IP-Konfiguration

...

Ethernet-Adapter VirtualBox Host-Only Network #3:

  Verbindungsspezifisches DNS-Suffix:
  Verbindungslokale IPv6-Adresse  . : fe80::782a:ed82:31b3:baf%5
  IPv4-Adresse  . . . . . . . . . . : 192.168.56.1
  Subnetzmaske  . . . . . . . . . . : 255.255.255.0
  Standardgateway . . . . . . . . . :

...
'''
##On rancher
'''
sudo ros config set rancher.network.interfaces.eth1.address "172.19.8.101/24"
sudo ros config set rancher.network.interfaces.eth1.dhcp false
sudo system-docker restart network
'''

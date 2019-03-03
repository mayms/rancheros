# Install
```bash
sudo ros install -c https://raw.githubusercontent.com/mayms/rancheros/master/cloud-config.yml -d /dev/sda
```

# Add host-only nic
## On host
```
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
```
## On rancher
```
sudo ros config set rancher.network.interfaces.eth0.dhcp true

sudo ros config set rancher.network.interfaces.eth1.address "192.168.56.10/24"
sudo ros config set rancher.network.interfaces.eth1.dhcp false

sudo system-docker restart network
```

# ssh to rancher
## with port forwarding in vbox
```
ssh rancher@localhost -p 2222
```

## after host-only nic is added
```
ssh rancher@192.168.56.10
```

# Configure remote docker daemon on host
Add to .profile
```
export DOCKER_HOST=tcp://192.168.56.10:2375
```
# Setting a static ip


1. The first step toward setting up a static IP address is identifying the name of the ethernet interface you want to configure. To do so, use the `ip link` command.

2. Netplan configuration files are stored in the `/etc/netplan` directory. You’ll probably find one or more YAML files in this directory. The name of the file may differ from setup to setup. The content of this file should be something like:

```yml
network:
  version: 2
  ethernets:
    ens3:
      dhcp4: yes
```

Each Netplan Yaml file starts with the network key that has at least two required elements. The first required element is the version of the network configuration format, and the second one is the device type. The device type can be `ethernets`, `bonds`, `bridges`, or `vlans`.


Under the device’s type (ethernets), you can specify one or more network interfaces. In this example, we have only one interface ens3 that is configured to obtain IP addressing from a DHCP server dhcp4: yes.

To assign a static IP address to `ens3` interface, edit the file as follows:

* Set DHCP to `dhcp4: no`.
* Specify the static IP address. Under `addresses`: you can add one or more IPv4 or IPv6 IP addresses that will be assigned to the network interface.
* Specify the gateway.
* Under nameservers, set the IP addresses of the nameservers.


```yaml
network:
  version: 2
  ethernets:
    abc1:
      dhcp4: no
      addresses:
        - 192.168.1.233
      gateway4: 192.168.1.1 #router's ip
      nameservers:
          addresses: [8.8.8.8, 1.1.1.1]
```

3. Apply changes

```bash
sudo netplan apply
```

4. Check if it works:

```bash
ip addr show dev abc1
```
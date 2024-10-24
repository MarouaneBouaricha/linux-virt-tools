# linux-virt-tools
Linux Virtualization Scripts Tools


## Emulate separate network nodes (via network namespaces)
### Create a new network namespace (bridge1) with a bridge device (br1) in it
```shell
create_bridge bridge1 br1
```
or
```shell
create_end_host host1 eth1 '192.168.0.1/24' bridge1 br1
```
## Emulate network interfaces (via veth devices)
### Create two hosts connected to the br1 bridge
```shell
create_end_host host1 eth1 bridge1 br1
create_end_host host2 eth2 bridge1 br1
```
## Emulate network switches
### Create two disjoint network segments:
```shell
create_bridge bridge10 br10
create_bridge bridge20 br20
```
### Connect two bridges
```shell
connect_bridges bridge10 br10 bridge20 br20
```

## Send Arbitary Data
from host1 to all hosts
```shell
ethsend --net=/var/run/netns/host1 \
  ethsend eth1 ff:ff:ff:ff:ff:ff 'Hello all!'

```
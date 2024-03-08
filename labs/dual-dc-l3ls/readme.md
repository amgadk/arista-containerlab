## Dual DC L3LS Example

This example will create the Dual DC L3LS topology, the configuration for each device will need to manually added (for an automated ansible version of this example refer to the dual-dc-l3ls-ansible example).

## Lab topology

The diagram below shows that this lab topology has two data centers. 

<p align="center">
  <img src="/docs/imgs/dual-dc-l3ls.png" alt="Lab Topology" width="800"/>
</p>

## ATD topology device list

Out-of-band management IP allocation for DC1	172.16.1.0/24
Default gateway	172.16.1.1
dc1-spine1	172.16.1.11
dc1-spine2	172.16.1.12
dc1-leaf1a	172.16.1.101
dc1-leaf1b	172.16.1.102
dc1-leaf2a	172.16.1.103
dc1-leaf2b	172.16.1.104
dc1-leaf1c	172.16.1.151
dc1-leaf2c	172.16.1.152
dc2-spine1	172.16.1.21
dc2-spine2	172.16.1.22
dc2-leaf1a	172.16.1.111
dc2-leaf1b	172.16.1.112
dc2-leaf2a	172.16.1.113
dc2-leaf2b	172.16.1.114
dc2-leaf1c	172.16.1.161
dc2-leaf2c	172.16.1.162


| Device | IP Address |
| ------ | ------------ |
| dc1-spine1 |172.16.1.11 |
| dc1-spine2 |172.16.1.12 |
| dc1-leaf1a  |172.16.1.101 |
| s1-leaf2  |192.168.0.13 |
| s1-leaf3  |192.168.0.14 |
| s1-leaf4  |192.168.0.15 |
| s1-host1  |192.168.0.16 |
| s1-host2  |192.168.0.17 |
| s1-spine1 |192.168.0.10 |
| s1-spine2 |192.168.0.11 |
| s1-leaf1  |192.168.0.12 |
| s1-leaf2  |192.168.0.13 |
| s1-leaf3  |192.168.0.14 |
| s1-leaf4  |192.168.0.15 |
| s1-host1  |192.168.0.16 |
| s1-host2  |192.168.0.17 |

> Current repository is built with cEOS management interface (`Management0`). If you run a vEOS topology, please update `mgmt_interface` field to `Management1` in the [ATD_LAB](./atd-inventory/group_vars/ATD_LAB.yml) `group_vars`.



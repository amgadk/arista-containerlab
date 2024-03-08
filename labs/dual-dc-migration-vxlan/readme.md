## Dual DC Migration Example (With VXLAN)


This example will create the Dual DC L3LS topology, the configuration for each device will need to manually added (for an automated ansible version of this example refer to the dual-dc-l3ls-ansible example).

## Lab topology

The diagram below shows that this lab topology has two data centers. 

<p align="center">
  <img src="/docs/imgs/dualdctopology.png" alt="Lab Topology" width="600"/>
</p>

## cEOS topology device list

Out-of-band management IP allocation for DC1	172.16.1.0/24


| Device | IP Address |
| ------ | ------------ |
| dc1spine1 |172.16.1.11 |
| dc1spine2 |172.16.1.12 |
| dc1leaf1a  |172.16.1.111 |
| dc1leaf1b  |172.16.1.112 |
| hostb  |172.16.1.155 |
| hostc  |172.16.1.156 |
| dc2spine1 |172.16.1.21 |
| dc2spine2 |172.16.1.22 |
| dc2leaf1a  |172.16.1.121 |
| dc2leaf1b  |172.16.1.122 |
| hosta  |172.16.1.165 |




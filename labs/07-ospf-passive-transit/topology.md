# Topology

| Cable | Endpoint A | Endpoint B |
| --- | --- | --- |
| Transit | R1 GigabitEthernet0/0 | R2 GigabitEthernet0/0 |

| Node | Interface | IPv4 address | OSPF area |
| --- | --- | --- | --- |
| R1 | GigabitEthernet0/0 | 10.0.12.1/30 | 0 |
| R2 | GigabitEthernet0/0 | 10.0.12.2/30 | 0 |
| R1 | Loopback0 | 192.0.2.1/32 | 0 |
| R2 | Loopback0 | 198.51.100.2/32 | 0 |

OSPF process 10 on both routers; router IDs equal their respective loopback addresses. Transit network type is point-to-point on both ends. There is no ACL, authentication, redistribution or competing routing protocol in this scenario.

[Exercise](README.md)

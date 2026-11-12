# Topology

| Node | Template |
| --- | --- |
| R1 | IOSv / IOS XE router |
| R2 | IOSv / IOS XE router |
| R3 | IOSv / IOS XE router |

| Node A | Port A | Node B | Port B | Segment |
| --- | --- | --- | --- | --- |
| R1 | Gi0/0 | R2 | Gi0/0 | 10.0.12.0/30 primary |
| R1 | Gi0/1 | R3 | Gi0/0 | 10.0.13.0/30 backup |

Create only the links listed above. Leave unrelated interfaces disconnected. Read [setup](../../docs/setup.md) before loading configs.

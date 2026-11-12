# Topology

| Node | Template |
| --- | --- |
| SW1 | IOSvL2 switch |
| SW2 | IOSvL2 switch |
| PC1 | VPCS |
| PC2 | VPCS |

| Node A | Port A | Node B | Port B | Segment |
| --- | --- | --- | --- | --- |
| SW1 | Gi0/0 | SW2 | Gi0/0 | LACP member 1 |
| SW1 | Gi0/1 | SW2 | Gi0/1 | LACP member 2 |
| PC1 | eth0 | SW1 | Gi0/2 | access VLAN 20 |
| PC2 | eth0 | SW2 | Gi0/2 | access VLAN 20 |

Create only the links listed above. Leave unrelated interfaces disconnected. Read [setup](../../docs/setup.md) before loading configs.

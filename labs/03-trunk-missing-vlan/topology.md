# Topology

| Node | Template |
| --- | --- |
| SW1 | IOSvL2 switch |
| SW2 | IOSvL2 switch |
| PC1 | VPCS |
| PC2 | VPCS |

| Node A | Port A | Node B | Port B | Segment |
| --- | --- | --- | --- | --- |
| PC1 | eth0 | SW1 | Gi0/1 | access VLAN 20 |
| SW1 | Gi0/0 | SW2 | Gi0/0 | 802.1Q trunk |
| SW2 | Gi0/1 | PC2 | eth0 | access VLAN 20 |

Create only the links listed above. Leave unrelated interfaces disconnected. Read [setup](../../docs/setup.md) before loading configs.

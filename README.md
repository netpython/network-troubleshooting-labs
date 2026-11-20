# Network Troubleshooting Labs

**Seven Cisco IOS and IOS XE incidents to build diagnostic reasoning.**

Start with a broken network, gather evidence, make a minimal correction, and prove that forwarding or protocol state has recovered.

`7 incidents` · `PNETLab / EVE-NG` · `Initial and fixed configurations` · `Progressive hints`

## Choose an incident

| Lab | Problem | Skills | Time |
| --- | --- | --- | ---: |
| [01 · OSPF EXSTART](labs/01-ospf-exstart/README.md) | Connected peers never reach FULL | Adjacencies, MTU, RIB | 25 min |
| [02 · Missing BGP prefix](labs/02-bgp-missing-prefix/README.md) | The session is up but a subnet is absent | Origination, exact RIB match, advertisements | 25 min |
| [03 · Missing trunk VLAN](labs/03-trunk-missing-vlan/README.md) | Hosts lose connectivity after a trunk change | VLAN membership, MAC learning, STP | 20 min |
| [04 · LACP passive/passive](labs/04-lacp-passive-passive/README.md) | Physical links are up but the bundle never forms | LACP modes, member state, port channels | 25 min |
| [05 · Return traffic ACL](labs/05-return-traffic-acl/README.md) | The request leaves but its reply is dropped | ACL direction, ICMP types, counters | 30 min |
| [06 · Backup route preferred](labs/06-floating-static-route/README.md) | A healthy primary path loses to a broken standby | Administrative distance, RIB, CEF | 30 min |
| [07 · No OSPF neighbor on a working link](labs/07-ospf-passive-transit/README.md) | Transit pings succeed but no adjacency forms | Passive interfaces, Hellos, return path | 25 min |

Times are estimates. Labs 05 and 06 use a stateless IOS ACL and static routing to practice packet-path reasoning.

## Start here

1. Follow the [emulator setup guide](docs/setup.md).
2. Pick a lab and build its topology from the node and cabling tables.
3. Load the `initial-configs/` files onto clean nodes.
4. Generate the symptom and record evidence in the [incident worksheet](docs/incident-worksheet.md).
5. Use the progressive hints if needed, then inspect the solution.
6. Apply the correction, verify the success criteria, and reset the fault to repeat.

Each lab supplies a problem brief, topology table, initial configurations, three hints, diagnosis, verification commands, full corrected configurations, and a minimal reset delta.

## What has been validated

The repository has been checked offline for configuration consistency, topology interfaces, fault isolation and documentation links. Device execution is pending lab validation with your licensed Cisco images. Expected outputs are described as criteria, and no fabricated terminal captures are presented.

The switching scenarios require a Layer 2 capable image such as IOSvL2. Routing scenarios can use IOSv or a compatible IOS XE image after adapting interface names. See the setup guide for platform-specific details.

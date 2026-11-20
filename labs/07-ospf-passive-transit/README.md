# 07 · No OSPF neighbor on a working transit link

[Catalogue](../../README.md) · [Topology](topology.md) · [Hints](hints.md) · [Solution](solutions/README.md)

**Foundation · 25 minutes**

Two routers can ping each other's directly connected transit address. Their loopbacks remain unreachable and no OSPF neighbor appears after a configuration change. Your task is to find the smallest correction without restarting OSPF.

## Environment and initial state

Use two clean licensed IOSv or compatible IOS XE routers with OSPFv2, one routed Ethernet port each. Build the [topology](topology.md) in PNETLab, EVE-NG or GNS3 with an image template supported by your emulator. Read [setup](../../docs/setup.md); adapt interface names consistently. No images or imported projects are supplied, and execution on these emulators remains untested.

Load [R1](initial-configs/R1.cfg) and [R2](initial-configs/R2.cfg) onto isolated nodes. These files contain the broken state. Wait at least the configured OSPF dead interval before recording the symptom; older neighbor state can remain temporarily after introducing a fault.

## Investigate

1. Prove physical and IPv4 transit reachability.
2. Check OSPF participation, interface parameters and neighbor state.
3. Compare the configuration with the expected topology.
4. State a hypothesis with supporting evidence before changing anything.
5. Apply one minimal correction, then prove adjacency and bidirectional loopback reachability.
6. Record image/release, evidence and the correction in the [incident worksheet](../../docs/incident-worksheet.md).

Useful starting commands: `show ip interface brief`, `show ip ospf neighbor`, `show ip ospf interface GigabitEthernet0/0`, `show ip protocols`, `show running-config | section router ospf`.

Do not use `clear ip ospf process`, disable protections globally or add static routes to mask the fault. Read the hints progressively. The separate solution includes exact injection/reset instructions, corrected configs and acceptance checks.

All symptoms described here are expected lab behavior, not a real incident capture. Configuration consistency was reviewed offline; device validation is pending.

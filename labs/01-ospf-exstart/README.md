# OSPF neighbors stuck in EXSTART

**Intermediate · 25 minutes · Cisco IOS / IOS XE**

## Incident brief

The directly connected peers can ping each other. The OSPF adjacency does not reach FULL and remote loopbacks are absent from the routing table.

## Build the lab

1. Create the nodes and cable the interfaces in [topology.md](topology.md).
2. On clean nodes, load the files in [initial-configs](initial-configs/).
3. Wait for links and protocols to settle, then run the tests below.
4. Record your diagnosis in the [incident worksheet](../../docs/incident-worksheet.md) before opening the solution.

## Generate the symptom

On **R1**

```text
ping 10.0.12.2 repeat 5
ping 192.0.2.2 source 192.0.2.1 repeat 5
```

## Success criteria

- Both neighbors reach FULL.
- R1 learns 192.0.2.2/32 and R2 learns 192.0.2.1/32 through OSPF.
- Loopback-to-loopback ping succeeds after convergence.

[Progressive hints](hints.md) · [Solution and verification](solutions/README.md)

Expected behavior is described from the configurations. No captured device output is included.

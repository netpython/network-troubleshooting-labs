# A working host loses access after a trunk change

**Foundation · 20 minutes · Cisco IOS / IOS XE**

## Incident brief

PC1 and PC2 are in the same subnet and their access ports are up. Ping fails after a trunk allowed-list change.

## Build the lab

1. Create the nodes and cable the interfaces in [topology.md](topology.md).
2. On clean nodes, load the files in [initial-configs](initial-configs/).
3. Wait for links and protocols to settle, then run the tests below.
4. Record your diagnosis in the [incident worksheet](../../docs/incident-worksheet.md) before opening the solution.

## Generate the symptom

On **PC1**

```text
ping 192.0.2.20
```

## Success criteria

- VLAN 20 appears as allowed, active and forwarding on both ends of the trunk.
- Each switch learns the remote host MAC on the trunk after traffic is generated.
- PC1 can ping PC2 after ARP resolution.

[Progressive hints](hints.md) · [Solution and verification](solutions/README.md)

Expected behavior is described from the configurations. No captured device output is included.

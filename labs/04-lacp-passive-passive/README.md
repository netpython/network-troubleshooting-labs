# EtherChannel members never form a bundle

**Intermediate · 25 minutes · Cisco IOS / IOS XE**

## Incident brief

Both member links are physically up, but no LACP bundle forms. User traffic may fail or use an individual STP-controlled link, depending on image behavior.

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

- Port-channel1 is a Layer 2 bundle in use, commonly shown as SU.
- Both members show P for bundled in the port-channel.
- PC1 reaches PC2 with the healthy bundle.

[Progressive hints](hints.md) · [Solution and verification](solutions/README.md)

Expected behavior is described from the configurations. No captured device output is included.

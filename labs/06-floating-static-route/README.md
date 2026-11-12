# A backup static route wins over the primary

**Intermediate · 30 minutes · Cisco IOS / IOS XE**

## Incident brief

Both R1 next hops respond. The server loopback is available through the primary uplink, but R1 sends traffic toward the backup and the destination is unreachable.

## Build the lab

1. Create the nodes and cable the interfaces in [topology.md](topology.md).
2. On clean nodes, load the files in [initial-configs](initial-configs/).
3. Wait for links and protocols to settle, then run the tests below.
4. Record your diagnosis in the [incident worksheet](../../docs/incident-worksheet.md) before opening the solution.

## Generate the symptom

On **R1**

```text
ping 10.0.12.2 repeat 5
ping 10.0.13.2 repeat 5
ping 198.51.100.1 source 192.0.2.1 repeat 5
```

## Success criteria

- Initially, R1 selects the route through 10.0.13.2 with distance 10.
- After correction, R1 selects 10.0.12.2 with distance 1.
- The sourced ping to the server loopback succeeds.

[Progressive hints](hints.md) · [Solution and verification](solutions/README.md)

Expected behavior is described from the configurations. No captured device output is included.

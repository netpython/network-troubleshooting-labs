# BGP is established but a prefix is missing

**Intermediate · 25 minutes · Cisco IOS / IOS XE**

## Incident brief

The eBGP session establishes. R1 receives the server subnet from R2, but R2 does not receive the client subnet from R1.

## Build the lab

1. Create the nodes and cable the interfaces in [topology.md](topology.md).
2. On clean nodes, load the files in [initial-configs](initial-configs/).
3. Wait for links and protocols to settle, then run the tests below.
4. Record your diagnosis in the [incident worksheet](../../docs/incident-worksheet.md) before opening the solution.

## Generate the symptom

On **R1**

```text
ping 198.51.100.1 source 192.0.2.1 repeat 5
```

## Success criteria

- R2 installs a BGP route for 192.0.2.0/24 through 10.0.12.1.
- R1 advertises the /24 while the peer remains established.
- A sourced ping between the two loopback addresses succeeds.

[Progressive hints](hints.md) · [Solution and verification](solutions/README.md)

Expected behavior is described from the configurations. No captured device output is included.

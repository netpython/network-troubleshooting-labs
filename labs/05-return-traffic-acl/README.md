# The request is permitted but the reply is dropped

**Intermediate · 30 minutes · Cisco IOS / IOS XE**

## Incident brief

Routes to both loopbacks exist. A ping initiated by R1 fails, while a sourced ping initiated by R2 succeeds.

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

On **R2**

```text
ping 192.0.2.1 source 198.51.100.1 repeat 5
```

## Success criteria

- The deny counter increases during the initial R1-sourced test.
- After correction, the echo-reply permit counter increases with R1-sourced pings.
- Both sourced ping directions succeed.

[Progressive hints](hints.md) · [Solution and verification](solutions/README.md)

Expected behavior is described from the configurations. No captured device output is included.

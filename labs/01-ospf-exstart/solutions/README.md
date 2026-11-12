# Solution

R1 advertises an IP MTU of 1400 while R2 uses the default 1500. Database description exchange fails or repeats. The observed state may alternate between EXSTART and EXCHANGE depending on the image and timing. Restore matching IP MTUs, then wait for the adjacency to reconverge.

## Gather evidence

On **R1**

```text
show ip ospf neighbor
show ip ospf interface GigabitEthernet0/0
show ip interface GigabitEthernet0/0
show ip route ospf
```

On **R2**

```text
show ip ospf neighbor
show ip interface GigabitEthernet0/0
show ip route ospf
```

## Apply the correction

On **R1**, paste [the correction](fixes/R1.cfg) into privileged EXEC mode.

```text
configure terminal
interface GigabitEthernet0/0
 no ip mtu
end
```

## Verify the result

- Both neighbors reach FULL.
- R1 learns 192.0.2.2/32 and R2 learns 192.0.2.1/32 through OSPF.
- Loopback-to-loopback ping succeeds after convergence.

Rerun the incident tests after convergence. Compare the relevant route, neighbor, ACL or interface state before and after the change.

## Repeat the exercise

Paste [the reset delta](reset/R1.cfg) on R1 to restore the injected fault. The full [fixed configurations](fixed-configs/) are also supplied for rebuilding clean nodes.

## Reference

- https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/13684-12.html

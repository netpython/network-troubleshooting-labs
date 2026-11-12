# Solution

SW1 permits only VLAN 99 on its trunk. VLAN 20 exists on both switches but cannot traverse that link. Add VLAN 20 to the allowed list without replacing the other VLANs.

## Gather evidence

On **SW1**

```text
show interfaces trunk
show vlan brief
show mac address-table dynamic vlan 20
show spanning-tree vlan 20
```

On **SW2**

```text
show interfaces trunk
show mac address-table dynamic vlan 20
```

## Apply the correction

On **SW1**, paste [the correction](fixes/SW1.cfg) into privileged EXEC mode.

```text
configure terminal
interface GigabitEthernet0/0
 switchport trunk allowed vlan add 20
end
```

## Verify the result

- VLAN 20 appears as allowed, active and forwarding on both ends of the trunk.
- Each switch learns the remote host MAC on the trunk after traffic is generated.
- PC1 can ping PC2 after ARP resolution.

Rerun the incident tests after convergence. Compare the relevant route, neighbor, ACL or interface state before and after the change.

## Repeat the exercise

Paste [the reset delta](reset/SW1.cfg) on SW1 to restore the injected fault. The full [fixed configurations](fixed-configs/) are also supplied for rebuilding clean nodes.

## Reference

- https://www.cisco.com/c/en/us/support/switches/catalyst-2960-series-switches/products-command-reference-list.html

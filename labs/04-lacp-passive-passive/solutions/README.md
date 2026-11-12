# Solution

Both peers are configured as LACP passive, so neither initiates negotiation. Make SW1 active and leave SW2 passive. After negotiation, both physical members must be bundled rather than individual or suspended.

## Gather evidence

On **SW1**

```text
show etherchannel summary
show lacp neighbor
show running-config interface GigabitEthernet0/0
show spanning-tree vlan 20
```

On **SW2**

```text
show etherchannel summary
show lacp neighbor
```

## Apply the correction

On **SW1**, paste [the correction](fixes/SW1.cfg) into privileged EXEC mode.

```text
configure terminal
interface range GigabitEthernet0/0 - 1
 channel-group 1 mode active
end
```

## Verify the result

- Port-channel1 is a Layer 2 bundle in use, commonly shown as SU.
- Both members show P for bundled in the port-channel.
- PC1 reaches PC2 with the healthy bundle.

Rerun the incident tests after convergence. Compare the relevant route, neighbor, ACL or interface state before and after the change.

## Repeat the exercise

Paste [the reset delta](reset/SW1.cfg) on SW1 to restore the injected fault. The full [fixed configurations](fixed-configs/) are also supplied for rebuilding clean nodes.

## Reference

- https://www.cisco.com/c/en/us/support/switches/catalyst-2960-series-switches/products-command-reference-list.html

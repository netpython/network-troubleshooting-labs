# Solution

The inbound ACL on R1 permits echo requests from the server loopback, but R1-initiated pings return as echo-reply packets. Those replies hit the explicit deny. Add the narrow echo-reply permit before the deny. This IOS ACL is stateless and is used to teach return-path reasoning.

## Gather evidence

On **R1**

```text
show ip route 198.51.100.1
show ip interface GigabitEthernet0/0
show ip access-lists FROM-SERVER
```

On **R2**

```text
show ip route 192.0.2.1
```

## Apply the correction

On **R1**, paste [the correction](fixes/R1.cfg) into privileged EXEC mode.

```text
configure terminal
ip access-list extended FROM-SERVER
 30 permit icmp host 198.51.100.1 host 192.0.2.1 echo-reply
end
```

## Verify the result

- The deny counter increases during the initial R1-sourced test.
- After correction, the echo-reply permit counter increases with R1-sourced pings.
- Both sourced ping directions succeed.

Rerun the incident tests after convergence. Compare the relevant route, neighbor, ACL or interface state before and after the change.

## Repeat the exercise

Paste [the reset delta](reset/R1.cfg) on R1 to restore the injected fault. The full [fixed configurations](fixed-configs/) are also supplied for rebuilding clean nodes.

## Reference

- https://www.cisco.com/c/en/us/support/docs/security/ios-firewall/23602-confaccesslists.html

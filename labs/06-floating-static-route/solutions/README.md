# Solution

The primary route has distance 200 and the backup has distance 10. R1 therefore selects R3, whose server route deliberately points to Null0. Restore the primary distance to 1 so it wins over the backup distance 10. R3 models an impaired standby path. This exercise validates route preference and does not implement end-to-end failover monitoring.

## Gather evidence

On **R1**

```text
show ip route 198.51.100.1
show running-config | include ^ip route
show ip cef 198.51.100.1 detail
```

On **R2**

```text
show ip route 198.51.100.1
```

On **R3**

```text
show ip route 198.51.100.1
```

## Apply the correction

On **R1**, paste [the correction](fixes/R1.cfg) into privileged EXEC mode.

```text
configure terminal
no ip route 198.51.100.1 255.255.255.255 10.0.12.2 200
ip route 198.51.100.1 255.255.255.255 10.0.12.2 1
end
```

## Verify the result

- Initially, R1 selects the route through 10.0.13.2 with distance 10.
- After correction, R1 selects 10.0.12.2 with distance 1.
- The sourced ping to the server loopback succeeds.

Rerun the incident tests after convergence. Compare the relevant route, neighbor, ACL or interface state before and after the change.

## Repeat the exercise

Paste [the reset delta](reset/R1.cfg) on R1 to restore the injected fault. The full [fixed configurations](fixed-configs/) are also supplied for rebuilding clean nodes.

## Reference

- https://www.cisco.com/c/en/us/support/docs/ip/ip-routing/118263-technote-nexthop-00.html

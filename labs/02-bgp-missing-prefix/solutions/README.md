# Solution

R1 has a connected 192.0.2.0/24 route, while its BGP network statement names 192.0.2.0/25. No exact /25 route exists, so BGP does not originate that prefix. Correct the statement to /24. A session reset is unnecessary.

## Gather evidence

On **R1**

```text
show ip bgp summary
show ip route connected
show ip bgp
show ip bgp neighbors 10.0.12.2 advertised-routes
```

On **R2**

```text
show ip bgp summary
show ip bgp
show ip route bgp
```

## Apply the correction

On **R1**, paste [the correction](fixes/R1.cfg) into privileged EXEC mode.

```text
configure terminal
router bgp 65001
 no network 192.0.2.0 mask 255.255.255.128
 network 192.0.2.0 mask 255.255.255.0
end
```

## Verify the result

- R2 installs a BGP route for 192.0.2.0/24 through 10.0.12.1.
- R1 advertises the /24 while the peer remains established.
- A sourced ping between the two loopback addresses succeeds.

Rerun the incident tests after convergence. Compare the relevant route, neighbor, ACL or interface state before and after the change.

## Repeat the exercise

Paste [the reset delta](reset/R1.cfg) on R1 to restore the injected fault. The full [fixed configurations](fixed-configs/) are also supplied for rebuilding clean nodes.

## Reference

- https://www.cisco.com/c/en/us/support/docs/ip/border-gateway-protocol-bgp/26634-bgp-toc.html

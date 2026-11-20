# Diagnosis and correction

## Cause and evidence

R1 uses `passive-interface default` but omits the exception for its transit interface. OSPF Hellos are suppressed there. The interface still forwards IP traffic, so the directly connected ping works. R2 has the exception and cannot form a neighbor with R1 alone.

Confirm this in the actual `show ip ospf interface GigabitEthernet0/0` and router configuration output. Do not infer a passive-interface problem from every empty neighbor table: area, timers, authentication, filtering and topology can cause other failures. They are deliberately consistent in the supplied configurations.

## Minimal fix

Apply [R1 correction](fixes/R1.cfg). Keep the passive default; enable only the transit adjacency. R2 requires no change. Reference states: [R1](fixed-configs/R1.cfg), [R2](fixed-configs/R2.cfg).

This changes OSPF behavior on the transit link. Perform it only in the isolated lab; no process restart is required.

## Acceptance criteria

| Check | Expected result after correction |
| --- | --- |
| `show ip ospf neighbor` on both nodes | One FULL neighbor, often displayed FULL/- for this point-to-point network |
| `show ip route ospf` on R1 | 198.51.100.2/32 learned via 10.0.12.2 |
| `show ip route ospf` on R2 | 192.0.2.1/32 learned via 10.0.12.1 |
| R1: `ping 198.51.100.2 source Loopback0 repeat 5` | Five replies after convergence |
| R2: `ping 192.0.2.1 source Loopback0 repeat 5` | Five replies after convergence |
| Loopback OSPF behavior | Remains passive; no unintended adjacency surface added |

## Reproduce the fault and restore

Starting from the corrected state, apply [R1 reset](reset/R1.cfg). This explicitly makes the transit passive, reproducing the missing-adjacency behavior. Wait at least the configured dead interval and inspect both neighbors and learned routes. Confirm that the directly connected transit ping still works while sourced loopback reachability fails.

Reapply the minimal fix and repeat all acceptance checks. The reset delta is behaviorally equivalent to the initial missing exception; the running configuration rendering can differ by release. Do not save the fault unless intentionally preserving the exercise.

## Sources and validation

- [Cisco passive-interface behavior](https://www.cisco.com/c/en/us/td/docs/ios/iproute_pi/command/reference/iri_book/iri_pi1.html).
- [Cisco OSPF network-type command](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_ospf/command/iro-cr-book/m_ospf-i1.html).
- [Cisco OSPF neighbor troubleshooting](https://www.cisco.com/c/en/us/support/docs/ip/open-shortest-path-first-ospf/13699-29.html).

The scenario and configurations are original. Expected criteria are not recorded test results. Offline review does not replace testing on the selected image.

[Exercise](../README.md)

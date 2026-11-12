# Build a lab in PNETLab or EVE-NG

Use a separate, isolated topology for each incident. Supply your own licensed Cisco images.

## Templates and interfaces

| Role | Suggested template | Requirements |
| --- | --- | --- |
| R1, R2, R3 | IOSv router | GigabitEthernet0/0; lab 06 also requires GigabitEthernet0/1 on R1 |
| SW1, SW2 | IOSvL2 switch | Gi0/0 through Gi0/2 with VLAN, STP and LACP support |
| PC1, PC2 | VPCS | One Ethernet interface |

IOS XE routers can replace IOSv for routing labs if the selected image supports the required features. Map each interface in the topology table to its actual interface name and update the configuration before loading it. Catalyst IOS XE images require an appropriate switching emulation environment for the Layer 2 labs.

Allocate CPU and RAM according to your emulator template and image requirements. Start one lab at a time.

## Load the starting state

1. Create clean nodes from your emulator's templates.
2. Connect exactly the interfaces in the lab's topology table.
3. For Cisco nodes, finish or decline the initial setup dialog, enter privileged EXEC with `enable`, then enter `configure terminal`. Paste that node's `.cfg` file. The file ends with `end`.
4. For VPCS, paste the node's `.vpc` commands at its console.
5. Check every console for rejected commands and verify interface names before interpreting the incident.
6. Wait for interface and routing convergence before running the incident tests.

The IOSvL2 configurations explicitly select dot1q trunk encapsulation. On fixed-dot1q switch images that reject that command, omit only the `switchport trunk encapsulation dot1q` lines. Preserve the trunk mode and allowed VLAN commands.

VPCS hosts in the switching labs share a subnet and need no default gateway. A first ping can fail while ARP is being resolved. Retry before concluding that forwarding is broken.

## Apply a fix and repeat

The files in `solutions/fixes/` and `solutions/reset/` start with `configure terminal`. Paste them from privileged EXEC mode on the named device.

To repeat the same exercise, apply its reset delta. To rebuild, create clean nodes and load the initial configs. Pasting a full config into a running node merges settings and can leave existing commands behind.

The repository supplies configurations and cabling tables. Build the topology manually in your emulator. Native `.unl` project files and device images are not included.

## Validation status

Configurations, address plans, links, fault deltas and documentation links have been checked offline. Expected behaviors follow from these configurations and vendor references. The labs have not been booted on licensed Cisco images in this environment. Record your image version and observed results when validating a lab.

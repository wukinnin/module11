+++
title = 'Demo 5 - Mitigate STP Attacks'
date = 2024-10-30T16:04:26+08:00
+++

Add first one 2960 switch and rename to S1

![](/2ac9bd48-3401-48ba-bcf3-6c8bbbf30546.PNG)

Then access CLI, enable privileged EXEC, enter configuration mode, and change hostname to S1

```
Switch>
Switch>enable
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#
Switch(config)# hostname S1
S1(config)#
```

---

Implement PortFast and BPDU Guard for a switch based on the following topology and specified requirements

You are currently logged into S1. Complete the following steps to implement PortFast and BPDU Guard on all access ports:

- Enter interface configuration mode for fa0/1 – 24.
- Configure the ports for access mode.
- Return to global configuration mode.
- Enable PortFast by default for all access ports.
- Enable BPDU Guard by default for all access ports.

```
S1(config)#interface range fa0/1 - 24
S1(config-if-range)#switchport mode access
S1(config-if-range)#exit
S1(config)#spanning-tree portfast default
S1(config)#spanning-tree portfast bpduguard default
S1(config)# exit
```

Verify that PortFast and BPDU Guard is enabled by default by viewing STP summary information.

```
S1#show spanning-tree summary
Switch is in pvst mode
Root bridge for: none
Extended system ID           is enabled
Portfast Default             is enabled
PortFast BPDU Guard Default  is enabled
Portfast BPDU Filter Default is disabled
Loopguard Default            is disabled
EtherChannel misconfig guard is enabled
UplinkFast                   is disabled
BackboneFast                 is disabled
Configured Pathcost method used is short
(output omitted)
S1#
```

You have successfully configured and verified PortFast and BPDU Guard for the switch.
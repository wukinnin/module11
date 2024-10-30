+++
title = 'Demo 2 - Mitigate Vlan Attacks'
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

Mitigate VLAN hopping attacks on the switch based on the specified requirements.

You are currently logged into S1. The ports status of the ports are as follows:

- FastEthernet ports 0/1 through 0/4 are used for trunking with other switches.
- FastEthernet ports 0/5 through 0/10 are unused.
- FastEthernet ports 0/11 through 0/24 are active ports currently in use.

Use range fa0/1 – 4 to enter interface configuration mode for the trunks.

```
S1(config)#interface range fa0/1 - 0/4
```

Configure the interfaces as nonnegotiating trunks assigned to default VLAN 99.

```
S1(config-if-range)#switchport mode trunk
S1(config-if-range)#switchport nonegotiate
S1(config-if-range)#switchport trunk native vlan 99
S1(config-if-range)#exit
```

Use range fa0/5 – 10 to enter interface configuration mode for the trunks.

```
S1(config)#interface range fa0/5 - 10
```

Configure the unused ports as access ports, assign them to VLAN 86, and shutdown the ports.

```
S1(config-if-range)#switchport mode access
S1(config-if-range)#switchport access vlan 86
% Access VLAN does not exist. Creating vlan 86
S1(config-if-range)#shutdown
\*Mar  1 00:28:48.883: %LINK-5-CHANGED: Interface FastEthernet0/5, changed state to administratively down
\*Mar  1 00:28:48.900: %LINK-5-CHANGED: Interface FastEthernet0/6, changed state to administratively down
\*Mar  1 00:28:48.908: %LINK-5-CHANGED: Interface FastEthernet0/7, changed state to administratively down
\*Mar  1 00:28:48.917: %LINK-5-CHANGED: Interface FastEthernet0/8, changed state to administratively down
\*Mar  1 00:28:48.942: %LINK-5-CHANGED: Interface FastEthernet0/9, changed state to administratively down
\*Mar  1 00:28:48.950: %LINK-5-CHANGED: Interface FastEthernet0/10, changed state to administratively down
\*Mar  1 00:28:49.890: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/5, changed state to down
\*Mar  1 00:28:49.907: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/6, changed state to down
S1(config-if-range)# exit
```

Use range fa0/11 – 24 to enter interface configuration mode for the active ports and then configure them to prevent trunking.

```
S1(config)#interface range fa0/11 - 24
S1(config-if-range)#switchport mode access
S1(config-if-range)# end
S1#
```

You have successfully mitigated VLAN hopping attacks on this switch.
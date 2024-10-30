+++
title = 'Demo 3 - Mitigate DHCP Attacks'
date = 2024-10-30T16:04:26+08:00
+++

Add first one 2960 switch and rename to S1

![](/2ac9bd48-3401-48ba-bcf3-6c8bbbf30546.PNG)

Then access CLI and configure

---

Implement DHCP snooping for a switch based on the following topology and specified requirements.

You are currently logged into S1. Enable DHCP snooping globally for the switch.

```
S1(config)#ip dhcp snooping
```

Enter interface configuration mode for g0/1 – 2, trust the interfaces, and return to global configuration mode.

```
S1(config)#interface range g0/1 - 2
S1(config-if-range)#ip dhcp snooping trust
S1(config-if-range)#exit
```

Enter interface configuration mode for f0/1 – 24, limit the DHCP messages to no more than 10 per second, and return to global configuration mode.

```
S1(config)#interface range f0/1 - 24
S1(config-if-range)#ip dhcp snooping limit rate 10
S1(config-if-range)#exit
```

Enable DHCP snooping for VLANs 10,20,30-49.

```
S1(config)#ip dhcp snooping vlan 10,20,30-49
S1(config)# exit
```

Enter the command to verify DHCP snooping.

```
S1#show ip dhcp snooping
Switch DHCP snooping is enabled
DHCP snooping is configured on following VLANs:
10,20,30-49
DHCP snooping is operational on following VLANs:
none
DHCP snooping is configured on the following L3 Interfaces:
Insertion of option 82 is enabled
   circuit-id default format: vlan-mod-port
   remote-id: 0cd9.96d2.3f80 (MAC)
Option 82 on untrusted port is not allowed
Verification of hwaddr field is enabled
Verification of giaddr field is enabled
DHCP snooping trust/rate is configured on the following Interfaces:
Interface                  Trusted    Allow option    Rate limit (pps)
-----------------------    -------    ------------    ----------------   
GigabitEthernet0/1         yes        yes             unlimited
  Custom circuit-ids:
GigabitEthernet0/2         yes        yes             unlimited
  Custom circuit-ids:
FastEthernet0/1            no         no              10         
  Custom circuit-ids:
```

Enter the command to verify the current DHCP bindings logged by DHCP snooping

```
S1#show ip dhcp snooping binding
MacAddress         IpAddress       Lease(sec) Type          VLAN Interface
------------------ --------------- ---------- ------------- ---- --------------------
00:03:47:B5:9F:AD  10.0.0.10       193185     dhcp-snooping 5    FastEthernet0/1
S1#
```

You have successfully configured and verified DHCP snooping for the switch.
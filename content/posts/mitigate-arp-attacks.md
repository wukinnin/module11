+++
title = 'Demo 4 - Mitigate ARP Attacks'
date = 2024-10-30T16:04:26+08:00
+++

Add first one 2960 switch and rename to S1

![](/2ac9bd48-3401-48ba-bcf3-6c8bbbf30546.PNG)

Then access CLI and configure

---

Implement DAI for a switch based on the following topology and specified requirements.

You are currently logged into S1. Enable DHCP snooping globally for the switch.

```
S1(config)#ip dhcp snooping
```

Enter interface configuration mode for g0/1 – 2, trust the interfaces for both DHCP snooping and DAI, and then return to global configuration mode.

```
S1(config)#interface range g0/1 - 2
S1(config-if-range)#ip dhcp snooping trust
S1(config-if-range)#ip arp inspection trust
S1(config-if-range)#exit
```

Enable DHCP snooping and DAI for VLANs 10,20,30-49.

```
S1(config)#ip dhcp snooping vlan 10,20,30-49
S1(config)#ip arp inspection vlan 10,20,30-49
S1(config)#
```

You have successfully configured DAI for the switch.
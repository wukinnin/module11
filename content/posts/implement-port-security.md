+++
title = 'Demo 1 - Implement Port Security'
date = 2024-10-30T16:04:26+08:00
+++

Add first one 2960 switch and rename to S1

![](/2ac9bd48-3401-48ba-bcf3-6c8bbbf30546.PNG)

Then access CLI and configure

---

Implement port security for a switch interface based on the specified requirements

You are currently logged into S1. Configure FastEthernet 0/5 for port security by using the following requirements:

- Use the interface name fa0/5 to enter interface configuration mode.
- Enable the port for access mode.
- Enable port security.
- Set the maximum number of MAC address to 3.
- Statically configure the MAC address aaaa.bbbb.1234.
- Configure the port to dynamically learn additional MAC addresses and dynamically add them to the running configuration.
- Return to privileged EXEC mode.

```
Switch>enable
Switch#config t
Switch(config)#hostname S1
S1(config)#interface fa0/5
S1(config-if)#switchport mode access
S1(config-if)#switchport port-security
S1(config-if)#switchport port-security maximum 3
S1(config-if)#switchport port-security mac-address aaaa.bbbb.1234
S1(config-if)#switchport port-security mac-address sticky
S1(config-if)#end
```

*Optional:*

Enter the commands to verify port security.

```
S1#exit
S1#show port-security
S1#show port-security interface fa0/5
S1#show port-security address
```


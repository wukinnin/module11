+++
title = 'Demo 1 - Implement Port Security'
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

Implement port security for a switch interface based on the specified requirements

You are currently logged into S1. Configure FastEthernet 0/5 for port security by using the following requirements:

Use the interface name fa0/5 to enter interface configuration mode.
- Enable the port for access mode.
- Enable port security.
- Set the maximum number of MAC address to 3.
- Statically configure the MAC address aaaa.bbbb.1234.
- Configure the port to dynamically learn additional MAC addresses and dynamically add them to the running configuration.
- Return to privileged EXEC mode.

```
S1(config)#interface fa0/5
S1(config-if)#switchport mode access
S1(config-if)#switchport port-security
S1(config-if)#switchport port-security maximum 3
S1(config-if)#switchport port-security mac-address aaaa.bbbb.1234
S1(config-if)#switchport port-security mac-address sticky
S1(config-if)#end
```

Enter the command to verify port security for all interfaces.

```
S1#show port-security
Secure Port  MaxSecureAddr  CurrentAddr  SecurityViolation  Security Action
                (Count)       (Count)          (Count)
---------------------------------------------------------------------------
      Fa0/5              3            2                  0         Shutdown
---------------------------------------------------------------------------
Total Addresses in System (excluding one mac per port)     : 0
Max Addresses limit in System (excluding one mac per port) : 8192
```

Enter the command to verify port security on FastEthernet 0/5. Use fa0/5 for the interface name.

```
S1#show port-security interface fa0/5
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Aging Type                 : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 3
Total MAC Addresses        : 2
Configured MAC Addresses   : 1
Sticky MAC Addresses       : 1
Last Source Address:Vlan   : 0090.2135.6B8C:1
Security Violation Count   : 0
```

Enter the command that will display all of the addresses to verify that the manually configured and dynamically learned MAC addresses are in the running configuration.

```
S1#show port-security address
               Secure Mac Address Table
-----------------------------------------------------------------------------
Vlan    Mac Address       Type                          Ports   Remaining Age
                                                                   (mins)    
----    -----------       ----                          -----   -------------
   1    0090.2135.6b8c    SecureSticky                  Fa0/5        -
   1    aaaa.bbbb.1234    SecureConfigured              Fa0/5        -
-----------------------------------------------------------------------------
Total Addresses in System (excluding one mac per port)     : 0
Max Addresses limit in System (excluding one mac per port) : 8192
```

You have successfully configured and verified port security for the interface.
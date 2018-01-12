# Switch
<center>[Home](../index.html)</center>

[TOC]

## Configure an IP address and a subnet mask

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface vlan 1
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# description Link to VLAN 1
Switch(config-if)# no shutdown
```

## Configure a default gateway address

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# ip default-gateway 192.168.10.254
```

## Shutdown unused interfaces (FastEthernet and GigabitEthernet)

### Per interface

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface FastEthernet 0/3
Switch(config-if)# shutdown

%LINK-5-CHANGED: Interface FastEthernet0/3, changed state to administratively down
Switch(config-if)# exit
Switch(config)#
```

### Per range of interfaces

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface range FastEthernet 0/4 - FastEthernet 0/24
Switch(config)# !* interface range FastEthernet 0/4 - 24
Switch(config-if-range)#shutdown

%LINK-5-CHANGED: Interface FastEthernet0/4, changed state to administratively down

…

%LINK-5-CHANGED: Interface FastEthernet0/24, changed state to administratively down
Switch(config-if-range)# end
Switch#
```

## VLAN

### Create a VLAN

**Format**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# vlan ID
Switch(config-vlan)# name vlanName
Switch(config-vlan)# exit
```

**Example:**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# vlan 99
Switch(config-vlan)# name Management
Switch(config-vlan)# exit
```

### Assigning ports to a VLAN

**Format**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface interfaceID
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan ID
Switch(config-if)# exit
```

**Example:**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface Fa 0/5
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 99
Switch(config-if)# exit
```

### Delete a VLAN

 ⚠️**WARNING** ⚠️  
> _Before the deletion of the VLAN, the assigned ports have to be re-assigned to another VLAN._

**Format**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# no vlan ID
```

**Example:**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# no vlan 99
```

### Delete a port from a VLAN

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface Fa 0/5
Switch(config-if)# no switchport access vlan
```

### Activate a trunk link (to be configured on each end)

⚠️**WARNING** _Never use **VLAN 1** as native._  ⚠️
 
> - _The native VLAN has to be the same on each end_  
> - _By default, all VLANs are allowed. To filter the VLANs, use **allowed**._

**Format**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface interfaceID
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk native vlan ID
Switch(config-if)# switchport trunk allowed vlan ID1,ID2,ID3
Switch(config-if)# end
```

**Example:**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface Fa 0/5
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk native vlan 99
Switch(config-if)# end
```

### Configure the IP address of the management interface of the VLAN and activate it

**Format**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface vlan ID
Switch(config-if)# ip address IPAddress subnetMask
Switch(config-if)# no shutdown
Switch(config-if)# end
```

**Example:**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface vlan 99
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# end
```

### Show the different VLAN activated and the linked ports

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch#show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                                Fa0/7, Fa0/8, Fa0/9, Fa0/10
                                                Fa0/11, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/18
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/1, Gig0/2
99   Management                       active    Fa0/5, Fa0/6
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    
Switch#
```

## Activate the DHCP snooping

#### Set the FastEthernet 0/1 interface as trustworthy/reliable (for the VLAN ID1 et ID2)

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# ip dhcp snooping
Switch(config)# ip dhcp snooping vlan ID1,ID2
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# ip dhcp snooping trust
```

### Set the same settings plus limit the number of DHCP packets per second that an interface can receive.

_The range is **1 to 2048**. It's recommended to trust not more than **100** packets per second._  
_On the other hand, the limit should be increased if the port is a trunk port assigned to more than one VLAN on which DHCP snooping is enabled._

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# ip dhcp snooping
Switch(config)# ip dhcp snooping vlan ID1,ID2
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# ip dhcp snooping trust
Switch(config-if)# ip dhcp snooping limit rate 
```

## Display the MAC address table

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show mac-address-table 
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

  99    0060.3e71.9902    STATIC      Fa0/5
  99    0090.2b03.5b13    STATIC      Fa0/6
Switch#
```

## Port security

### Activate the port security

⚠️**WARNING** ⚠️   
> _Without the following command, none of this will work !!!_  
> **RQ:** _It sets the maximal number of MAC addresses to **1**  and the violation action type to **shutdown**._  


<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config-if)# switchport port-security
```

#### Choose the interface

_We choose the interface, shut it down and activate the port security on it._   

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface interfaceID
Switch(config-if)# shutdown
Switch(config-if)# switchport port-security
```

_Then we activate the security for the MAC address of the chosen interface  
(from [show interfaces interfaceID](Router and switch.html#shINT))._  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config-if)# switchport port-security mac-address macAddress
Switch(config-if)# no shutdown
Switch(config-if)# end
```

### Set the number of authorized MAC addresses

_The default value is **1** and the maximum number of addresses is **3072**._  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config-if)# switchport port-security maximum value
```

### Set the violation action type

_The default type is **shutdwon**  but there are three of them._ 

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config-if)# switchport port-security violation type
``` 

#### shutdown

In this mode, any port security violation immediately causes the deactivation of the interface errors recording as well as the port LED. The violation counter is incremented.

#### protect

When the secure MAC addresses number reaches the authorized limit on the port, packets with unknown source addresses are ignored until a sufficient number of secure MAC addresses are deleted or the maximum number of addresses to be authorized is increased. Using this mode produces no notification when a security violation has occurred.

#### restrict

When the secure MAC addresses number reaches the authorized limit on the port, packets with unknown source addresses are ignored until a sufficient number of secure MAC addresses are deleted or the maximum number of addresses to be authorized is increased. In this mode, a notification indicates that a security violation has occurred.


### Configure an interface to save the MAC addresses dynamically learned

#### Default

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface interfaceID
Switch(config-if)# switchport port-security mac-address sticky
```

#### The secure MAC addresses can be manually set

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface interfaceID
Switch(config-if)# switchport port-security mac-address sticky macAddress
```

### Delete the _**Error Disabled**_ of an interface

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# configure terminalSwitch(config)# interface FastEthernet 0/5
Switch(config-if)# shutdown
Switch(config-if)# no shutdown
```

### Verify the port security (display the secure MAC addresses)

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show port-security
Secure Port MaxSecureAddr CurrentAddr SecurityViolation Security Action
               (Count)       (Count)        (Count)
−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−
        Fa0/5        1          1                 0         Shutdown
        Fa0/6        1          1                 0         Shutdown
−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−
Switch#
```

### Display port security of an interface

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show port-security interface FastEthernet 0/5
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Aging Type                 : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 1
Total MAC Addresses        : 1
Configured MAC Addresses   : 1
Sticky MAC Addresses       : 0
Last Source Address:Vlan   : 0060.3E71.9902:99
Security Violation Count   : 0

Switch#
```

### Display the Secure MAC Address Table

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show port-security address 
			Secure Mac Address Table
−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−
Vlan	Mac Address			Type						  Ports		Remaining Age
												 					(mins)
−−−−	−−−−−−−−−−−			−−−−						  −−−−−		−−−−−−−−−−−−−
99		0060.3E71.9902		SecureConfigured	FastEthernet0/5		-
99		0090.2B03.5B13		SecureConfigured	FastEthernet0/6		-
−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−−
Total Addresses in System (excluding one mac per port)     : 0
Max Addresses limit in System (excluding one mac per port) : 1024
Switch#
```

## Additional source
* [pantz.org](http://www.pantz.org/software/ios/ioscommands.html)  
* [Cisco.com](http://www.cisco.com)


***

<center>ToolKit © <!--[if IE 8]>2017<![endif]--><!--[if !IE 8]> -->2017 <span id="currentYear"></span><!-- <![endif]--></center><center><a href="https://alexandre-ducobu.com/En">About</a> </center>


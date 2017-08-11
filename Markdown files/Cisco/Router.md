#Router
<center>[Home](../index.html)</center>

[TOC]

##Configure an IP address and a subnet mask on an interface

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# interface GigabitEthernet 0/1
Router(config-if)# ip address 192.168.10.254 255.255.255.0
Router(config-if)# no shutdown
```

##Configure a loopback interface

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# interface loopback 0
Router(config-if)# ip address 192.168.0.1 255.255.255.0
```

##Configure the clock rate on a serial interface (DCE)
> Configure on the source routeur (_the one near the clock image_)

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# interface S0/0/0
Router(config-if)# clock rate 128000
```

##Routing

###Static Route

**Format**  

- This one:  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# ip route <destinationIPAddress> <destinationSubnetMask> <forwardingRouterInterface>
```

- or  this one, **the favorite**:  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# ip route <destinationIPAddress> <destinationSubnetMask> <forwardingRouterAddress>
```

**Example:**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# ip route 172.16.0.96 255.255.255.0 192.168.11.1
Router(config)#
```

###Default route

**Format**

- This one:  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# ip route 0.0.0.0 0.0.0.0 <forwardingRouterInterface>
```

- or  this one, **the favorite**:  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# ip route 0.0.0.0 0.0.0.0 <forwardingRouterAddress>
```

**Example:**  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# ip route 0.0.0.0 0.0.0.0 FastEthernet 0/1
Router(config)#
```

##Change MAC address

###Set a new MAC address on an interface

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# interface GigabitEthernet 0/1
Router(config-if)# shutdown
Router(config-if)# mac-address aaaa.bbbb.cccc
Router(config-if)# no shutdown
```

###Reset the default MAC address of an interface

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Router(config)# interface GigabitEthernet 0/1
Router(config-if)# shutdown
Router(config-if)# no mac-address aaaa.bbbb.cccc
Router(config-if)# no shutdown
```

##Additional source
* [pantz.org](http://www.pantz.org/software/ios/ioscommands.html)  
* [Cisco.com](http://www.cisco.com)


***

<center>ToolKit © 2017</center><center><a href="http://alexandre-ducobu.esy.es/En">About</a> </center>


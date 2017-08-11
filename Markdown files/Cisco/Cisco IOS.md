#Cisco IOS
<center>[Home](../index.html)</center>

[TOC]

<!-- #Descriptions + IPv6 -->

##Execution modes

_To quit the current mode, use **exit**. You'll enter into the previous mode._

###User Mode
_Also known as **User EXEC Mode**_

- Default mode
- Limited access to the configuration
- Remote access  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch> 
```

###Privileged Mode
_Also known as **Privileged EXEC Mode**_

- Access through **enable**
- Device configuration
- Debugging and test  
**RQ:** _to access the User Mode, you can use the **disable** command_

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch> enable
Switch# 
Switch# disable
Switch> 
```

###Global Configuration Mode

- Access through **configure terminal** _(or **conf t**)_
- Access to the configuration
- Starting point for the other modes

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# configure terminal
Switch(config)#
Switch(config)# exit
Switch#
%SYS-5-CONFIG_I: Configured from console by console
Switch#
```

###Other Configuration Mode
_As **interface** or **subinterface** Configuration Mode_

- Depend on the requested mode
- Configuration of a service or a specific interface  
**RQ:** _to exit the current mode, use **exit**. To return to the privileged mode, use **end**._

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# exit
Switch(config)# line console 0
Switch(config-line)# end
Switch#
```

##General commands

###Get help
_Enter **?** into the CLI_

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch> ?
Exec commands:
	connect		Open a terminal connection
	disable		Turn off privileged commands
	disconnect	Disconnect an existing network connection
	enable		Turn on privileged commands
	exit		Exit from the EXEC
	logout		Exit from the EXEC
	ping		Send echo messages
	resume		Resume an active network connection
	show		Show running system information
	ssh			Open a secure shell client connection
	telnet		Open a telnet connection
	terminal	Set terminal line parameters
	traceroute	Trace route to destination
Switch>
```

###Restart the device
_For instance, to verify the new config_

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# reload
Proceed with reload? [confirm]
```

###Save config from running config (RAM) to starting config (NVRAM)

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# copy running-config starting-config
Destination filename [startup-config]? 
Building configuration...
[OK]
Switch#
```

###Reset the config

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# copy starting-config running-config
```

###Details the running configuration file (RAM)
_The same goes for the **starting-config**_

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show running-config
```

###Show history of executed commands

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show history
```

###Display the MAC address table

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show ip mac-addres-table
```

**or**

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show ip mac addres-table
```

###Execute configuration commands from the terminal

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# configure terminal
```

###Erase all the config files

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# write erase
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
[OK]
Erase of nvram: complete
%SYS-7-NV_BLOCK_INIT: Initialized the geometry of nvram
Switch# reload
```

###Get the current boot settings of IOS

**RQ:** _For IOS 15, the command is **show bootvar**._

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show boot
BOOT path-list      : c2960-lanbasek9-mz.150-2.SE4.bin
Config file         : flash:/config.text
Private Config file : flash:/private-config.text
Enable Break        : no
Manual Boot         : no
HELPER path-list    : 
Auto upgrade        : yes
NVRAM/Config file
      buffer size:   65536
```

###Copy and restoration

####Copy

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# copy flash: tftp:
Switch# !* Used to copy files from flash to tftp server
```
**Examples:**

#####Save the running configuration on a tftp.  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# copy run tftp:
Address or name of remote host []? 192.168.10.2
Destination filename [Switch-confg]? 

Writing running-config....!!
[OK - 623 bytes]

623 bytes copied in 3.001 secs (207 bytes/sec)
Switch#
```

#####Save the IOS _(file.bin)_ on a tftp.  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# copy flash: tftp: 
Source filename []? c2960-lanbase-mz.122-25.FX.bin
Address or name of remote host []? 192.168.10.2
Destination filename [c2960-lanbase-mz.122-25.FX.bin]? 

Writing c2960-lanbase
mz122-25.FX.bin....!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
[OK - 4414921 bytes]

4414921 bytes copied in 3.079 secs (38958 bytes/sec)
Switch#
```

####Restore

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# copy tftp: flash:
Switch# !* Used to restore file to flash from tftp server
Switch# copy tftp: run
```

**Example:**  

#####Download IOS from a server _(for an update or a reset)_  

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# copy tftp: flash: 
Address or name of remote host []? 192.168.10.2
Source filename []? c2960-lanbase-mz.122-25.FX.bin
Destination filename [c2960-lanbase-mz.122-25.FX.bin]? 
%Warning:There is a file already existing with this name
Do you want to over write? [confirm]

Accessing tftp://192.168.10.2/c2960-lanbase-mz.122-25.FX.bin...
Loading c2960-lanbase-mz.122-25.FX.bin from 192.168.10.2:
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!
[OK - 4414921 bytes]

4414921 bytes copied in 0.063 secs (1904027 bytes/sec)
Switch#
```

###Use another IOS file from the flash

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch(config)# boot system c2960-lanbase-mz.122-25.FX.bin
Switch(config)# exit
Switch# copy running-config starting-config
Switch# reload
```

###Show Cisco IOS version
**Also shows** _uptime of router, how the router started, where system was loaded from, the interfaces the POST found, and the configuration register._

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# show version
Cisco IOS Software, C2960 Software (C2960-LANBASE-M), Version 12.2(25)FX, RELEASE SOFTWARE (fc1)
Copyright (c) 1986-2005 by Cisco Systems, Inc.
Compiled Wed 12-Oct-05 22:05 by pt_team

ROM: C2960 Boot Loader (C2960-HBOOT-M) Version 12.2(25r)FX, RELEASE SOFTWARE (fc4)

System returned to ROM by power-on

Cisco WS-C2960-24TT (RC32300) processor (revision C0) with 21039K bytes of memory.


24 FastEthernet/IEEE 802.3 interface(s)
2 Gigabit Ethernet/IEEE 802.3 interface(s)

63488K bytes of flash-simulated non-volatile configuration memory.
Base ethernet MAC Address       : 0060.702A.D2EB
Motherboard assembly number     : 73-9832-06
Power supply part number        : 341-0097-02
Motherboard serial number       : FOC103248MJ
Power supply serial number      : DCA102133JA
Model revision number           : B0
Motherboard revision number     : C0
Model number                    : WS-C2960-24TT
System serial number            : FOC1033Z1EY
Top Assembly Part Number        : 800-26671-02
Top Assembly Revision Number    : B0
Version ID                      : V02
CLEI Code Number                : COM3K00BRA
Hardware Board Revision Number  : 0x01


Switch   Ports  Model              SW Version              SW Image
------   -----  -----              ----------              ----------
*    1   26     WS-C2960-24TT      12.2                    C2960-LANBASE-M

Configuration register is 0xF
```

- **Version d'IOS:** 12.2(25)FX
- **Modèle:** Cisco WS-C2960-24TT (RC32300)
- **Mémoire flash:** 63488K bytes _(flash-simulated non-volatile)_
- **Mémoire RAM:** 21039K bytes

###List the content of the flash (or a directory)

<div class="prism-show-language"><div class="prism-show-language-label">Cisco IOS</div></div>
```
Switch# dir flash:
Directory of flash:/

    1  -rw-     4414921          <no date>  c2960-lanbase-mz.122-25.FX.bin
    4  -rw-     4670455          <no date>  c2960-lanbasek9-mz.150-2.SE4.bin
    2  -rw-        1622          <no date>  config.text
    3  -rw-         616          <no date>  vlan.dat

64016384 bytes total (54928770 bytes free)
```

##Additional source
* [pantz.org](http://www.pantz.org/software/ios/ioscommands.html)  
* [Cisco.com](http://www.cisco.com)



***

<center>ToolKit © 2017</center><center><a href="http://alexandre-ducobu.esy.es/En">About</a> </center>

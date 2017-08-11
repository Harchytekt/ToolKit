#Switch and Router
<center>[Home](../index.html)</center>

[TOC]

##Configure hostname

```
Switch# configure terminal
Switch(config)# hostname S1
S1(config)# exit
```

##Set privileged mode password

```
Switch> enable
Switch# configure terminal
Switch(config)# enable password class
Switch(config)# exit
```

##Set encrypted privileged mode password

```
Switch> enable
Switch# configure terminal
Switch(config)# enable secret class
Switch(config)# exit
```

##Set password for console access
_Restricted access to the console port._

```
Switch(config)# line console 0
Switch(config-line)# password cisco
Switch(config-line)# logging synchronous
Switch(config-line)# !* Prevent console messages from aborting commands
Switch(config-line)# login !* Impose the use of the password
```

##Set password for virtual terminal (telnet) access
_Password must be set to access device through telnet._

```
Switch(config)# line vty 0 4 !* or 0 15
Switch(config-line)# password cisco
Switch(config-line)# logging synchronous
Switch(config-line)# !* Prevent console messages from aborting commands
Switch(config-line)# login !* Impose the use of the password
```

##Set encryption for plain text password such as enable and line

```
Switch(config)# service password-encryption
```

##Set a banner

```
Switch(config)# banner motd # Your message #
```

##Set date and time
**RQ:** _it **won't** be saved with the config !!!_

```
Switch# clock set 12:06:30 29 November 2016
Switch# show clock
12:6:33.623 UTC Tue Nov 29 2016
Switch#
```

##Prevent unwanted DNS lookups
_Disables the default behavior of the device of attempting to **resolve the invalid command into an IP address**._  

```
Switch(config)# no ip domain-lookup
```

##Configure SSH

To use SSH, IOS has to be a **'K9'** version. That means that the cryptography is taken over.  

###Checking SSH support:  

_This command is accessible from the **User** and **Privileged Modes**._

* SSH not supported

```
Switch> show ip ssh 
                ^
% Invalid input detected at '^' marker.
	
Switch>
```

* SSH disabled/not configured (but supported)

```
Switch> show ip ssh 
SSH Disabled - version 1.99
%Please create RSA keys (of atleast 768 bits size) to enable SSH v2.
Authentication timeout: 120 secs; Authentication retries: 3
Switch>
```

* SSH enabled  

```
Switch> show ip ssh
SSH Enabled - version 1.99
Authentication timeout: 75 secs; Authentication retries: 2
Switch>
```

###Configuration

####Configuration of the IP domain name

```
Switch(config)# ip domain-name myDomain
```

**Example:**  

```
Switch(config)# ip domain-name CCNA-Lab.com
```

####Creation of the username and the password for authentification

```
Switch(config)# username myName (privilege 0-15) secret myPass
```

**Example:**  

```
Switch(config)# username admin privilege 15 secret sshadmin
```

####SSH protocole activation on the VTY lines (required)

```
Switch(config)# line vty 0 15
Switch(config-line)# transport input ssh
Switch(config-line)# login local
```

####RSA Encryption Key generation

_Here we'll choose a modulus  of 1024 bits_

```
Switch(config)# crypto key generate rsa
The name for the keys will be: S1.CCNA-Lab.com
Choose the size of the key modulus in the range of 360 to 2048 for your
  General Purpose Keys. Choosing a key modulus greater than 512 may take
  a few minutes.

How many bits in the modulus [512]: 1024
% Generating 1024 bit RSA keys, keys will be non-exportable...[OK]

Switch(config)#
```

####To make sure that the SSH version 2 is used

```
Switch(config)# ip ssh version 2
```

####Change authentication timeout

```
Switch(config)# ip ssh time-out 75
```

####Change authentication retries

```
Switch(config)# ip ssh authentication-retries 2
```

###Display the SSH configuration

```
Switch# show ip ssh
SSH Enabled - version 2.0
Authentication timeout: 75 secs; Authentication retries: 2
```

###Verify the SSH conections towards the peripheral

```
Switch# show ssh
%No SSHv2 server connections running.
%No SSHv1 server connections running.
```

###Access the device from a PC through a SHH connection

**Format**  

```
SSH -l username IPAddress
```

**Example:**

_The used password is **sshadmin**._

```
C:\>SSH -l admin 172.16.99.11
Open
Password: 



S1>sh ip ssh
SSH Enabled - version 2.0
Authentication timeout: 75 secs; Authentication retries: 2
S1>exit

[Connection to 172.16.99.11 closed by foreign host]
C:\>
```

##Get a summary of the interfaces

```
Switch# show ip interface brief
```

##Activate the full duplex mode on interface

**Options:**  

* duplex {full | half | auto}
* no duplex

```
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# duplex full
Switch(config-if)# end
``` 

##Set the speed of an interface

**Options:**  

* 10 _(10 Mbps)_  
* 100 _(100 Mbps)_  
* 1000 _(1000 Mbps or 1 Gbps)_

```
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# speed 100
Switch(config-if)# !* the speed is 100 Mbps
Switch(config-if)# end
```

##Activate auto-MDIX

*RQ:* _To use this option, the speed and the duplex have to be **auto**._

```
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# duplex auto
Switch(config-if)# speed auto
Switch(config-if)# mdix auto
Switch(config-if)# end
```

<a name="shINT"></a>
##Get the informations of an interface (like its MAC address)

_The MAC address is **0060.3e71.9902**._

```
Switch# show interfaces GigabitEthernet 0/1
GigabitEthernet0/1 is up, line protocol is up (connected)
  Hardware is CN Gigabit Ethernet, address is 0060.3e71.9902 (bia 0060.3e71.9902)
  Internet address is 172.16.99.1/24
  MTU 1500 bytes, BW 1000000 Kbit, DLY 100 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full-duplex, 100Mb/s, media type is RJ45
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00, 
  Last input 00:00:08, output 00:00:05, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0 (size/max/drops); Total output drops: 0
  Queueing strategy: fifo
  Output queue :0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts, 0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 watchdog, 1017 multicast, 0 pause input
     0 input packets with dribble condition detected
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier
     0 output buffer failures, 0 output buffers swapped out

Switch#
```

##Additional source
* [pantz.org](http://www.pantz.org/software/ios/ioscommands.html)  
* [Cisco.com](http://www.cisco.com)


***

<center>ToolKit © 2017</center><center><a href="http://alexandre-ducobu.esy.es/En">About</a> </center>


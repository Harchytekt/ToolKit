# Windows Server
<center>[Home](../index.html)</center>

[TOC]

## DNS

_On **each** PC, go to **CMD** and type **ncpa.cpl**.  
Go to Propreties, IPv4 and choose an IPv4 address.  
For the primary zone, we choose **192.168.42.1** (Mask: 255.255.255.224 + Gateway: 192.168.42.30)  
Preferred DNS server: **192.168.42.1**, the second is for the secondary zone **192.168.42.2**._

### Primary Zone

**Machine name: _SRV164170_**

1.

- In DNS Manager, right click on **Forward Lookup Zones** > _New zone…_ > **Primary zone**
	- Choose a name for the zone, here: _ducobu.lan_
- Right click on **Reverse Lookup Zones** > _New zone…_ > **Primary zone**
	- Select _Primary zone_ > _IPv4_ > Network ID **192.168.42**

2.

- In the new primary zone, create a new host: **srv164170**; IP address: **192.168.42.1**
- For the **Lookup zone** as well as the **Reverse**:
	- Go to **SOA**, **Primary server** > _Browse_ and select the new host.
	- Go to **Name Servers** > Edit > FQDN: **srv164170.ducobu.lan.** and IP address: **192.168.42.1**  
	↳ OK (normal to have an error 😜)

_To verify if everything is correct: **CMD**:_

```
C:\Users\Administrator> nslookup
Default Server:  srv164170.ducobu.lan
Address:  192.168.42.1

> exit
C:\Users\Administrator>
```

3.

_If we want to create an alias (www) pointing on the principal server:_  

- In the new primary zone, **New alias (CNAME)**
- Name: **www**, FQDN: **srv164170.ducobu.lan.**

### Secondary Zone

**Machine name: _SRV164171_**

1.

**On SRV164170**

- We create a new host: **srv164171**; IP address: **192.168.42.2**
- For the **Lookup zone** as well as the **Reverse**:
	- Go to **Name Servers** > Edit > FQDN: **srv164171.ducobu.lan.** and IP address: **192.168.42.2**  
	↳ OK (normal to have an error 😜)

2.

**On SRV164171**

- In DNS Manager, right click on **Forward Lookup Zones** > _New zone…_ > **Secondary zone**
	- Zone name: _ducobu.lan_; IP address of the primary zone **192.168.42.1**
- Right click on **Reverse Lookup Zones** > _New zone…_ > **Secondary zone**
	- Select _Primary zone_ > _IPv4_ > Network ID **192.168.42**

In order to properly synchronize everything:  

- On **srv164170**, right click on the name _srv164170_ > _All tasks_ > _Restart_
- Likewise on **srv164171**
	- If you can't have access, refresh the two zones (Lookup et Reverse). First, on the primary server, then on the secondary server.

_To verify if everything is correct: **CMD**:_

```
C:\Users\Administrator>nslookup
Default Server:  srv164170.ducobu.lan
Address:  192.168.42.1

> www.ducobu.lan
Server:  srv164170.ducobu.lan
Address:  192.168.42.1

Name:    srv164170.ducobu.lan
Address:  192.168.42.1
Aliases:  www.ducobu.lan

> exit
C:\Users\Administrator>
```

3.

_Now that everythong is correct,we can verify, on the secondary server, if the zone transfertis functionnal:_  

```
C:\Users\Administrator>nslookup 192.168.42.1
Server:  srv164170.ducobu.lan
Address:  192.168.42.1

Name:    srv164170.ducobu.lan
Address:  192.168.42.1


C:\Users\Administrator>
```

_If it's okay, we can perform the zone transfert:_  

```
C:\Users\Administrator>nslookup
Default Server:  srv164170.ducobu.lan
Address:  192.168.42.1

> ls -d ducobu.lan
[srv164170.ducobu.lan]
 ducobu.lan.                    SOA    srv164170.ducobu.lan hostmaster. (7 900 600 86400 3600)
 ducobu.lan.                    NS     srv164170.ducobu.lan
 ducobu.lan.                    NS     srv164171.ducobu.lan
 srv164170                      A      192.168.42.1
 srv164171                      A      192.168.42.2
 www                            CNAME  srv164170.ducobu.lan
 ducobu.lan.                    SOA    srv164170.ducobu.lan hostmaster. (7 900 600 86400 3600)
> exit
C:\Users\Administrator>
```

_To do the same with the GUI, just do a right click on the **ducobu.lan** zone of the secondary server > **Transfert from Master**._

### Delegation zone

1.

We have to create a new primary zone on the secondary server (only in the _Forward Lookup Zones_).  
We'll call it **delegation.ducobu.lan**.

We create a new host: _srv164170_ & **IP Address**: _192.168.42.1_

Inside the **Properties** window:

- **Name Servers** > **FQDN**: _srv164170.ducobu.lan._ & **IP Address**: _192.168.42.1_

Now we have to create a new alias:   
We call it **www** and the **FQDN** is _srv164171.delegation.ducobu.lan._

2.

On the primary server, we have to create a **New delagation** > **Name**: _delegation_
> **Secondary server name**: srv164171.ducobu.lan

We can now verify if the delagation works. To do so, open the CMD on the primary server:

```
C:\Users\Administrator>nslookup
Default Server:  srv164170.ducobu.lan
Address:  192.168.42.1

> www.delegation.ducobu.lan
Server:  srv164170.ducobu.lan
Address:  192.168.42.1

Non-authoritative answer:
Non-authoritative answer:
Name:    www.delegation.ducobu.lan

> exit

C:\Users\Administrator>
```

## DHCP

_Todo_

## Active Directory

_Todo_


***

<center>ToolKit © 2017</center><center><a href="https://alexandre-ducobu.com/En">About</a> </center>


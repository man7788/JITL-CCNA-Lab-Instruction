# Part-6 - Network Services: DHCP, DNS, NTP, SNMP, Syslog, FTP, SSH, NAT

## Step 1

```
show ip dhcp binding
```

### R1

```
ip dhcp excluded-address 10.0.0.1 10.0.0.10
ip dhcp excluded-address 10.1.0.1 10.1.0.10
ip dhcp excluded-address 10.2.0.1 10.2.0.10
ip dhcp excluded-address 10.0.0.17 10.0.0.26
ip dhcp excluded-address 10.3.0.1 10.3.0.10
ip dhcp excluded-address 10.4.0.1 10.4.0.10
ip dhcp excluded-address 10.6.0.1 10.6.0.10
```

```
ip dhcp pool A-Mgmt
 network 10.0.0.0 255.255.255.240
 default-router 10.0.0.1
 dns-server 10.5.0.4
 domain-name jeremysitlab.com
 option 43 ip 10.0.0.7

ip dhcp pool A-PC
 network 10.1.0.0 255.255.255.0
 default-router 10.1.0.1
 dns-server 10.5.0.4
 domain-name jeremysitlab.com

ip dhcp pool A-Phone
 network 10.2.0.0 255.255.255.0
 default-router 10.2.0.1
 dns-server 10.5.0.4
 domain-name jeremysitlab.com

ip dhcp pool B-Mgmt
 network 10.0.0.16 255.255.255.240
 default-router 10.0.0.17
 dns-server 10.5.0.4
 domain-name jeremysitlab.com
 option 43 ip 10.0.0.7

ip dhcp pool B-PC
 network 10.3.0.0 255.255.255.0
 default-router 10.3.0.1
 dns-server 10.5.0.4
 domain-name jeremysitlab.com

ip dhcp pool B-Phone
 network 10.4.0.0 255.255.255.0
 default-router 10.4.0.1
 dns-server 10.5.0.4
 domain-name jeremysitlab.com

ip dhcp pool Wi-Fi
 network 10.6.0.0 255.255.255.0
 default-router 10.6.0.1
 dns-server 10.5.0.4
 domain-name jeremysitlab.com
```

## Step 2

### DSW-A1, DSW-A2

```
interface vlan 10
 ip helper-address 10.0.0.76

interface vlan 20
 ip helper-address 10.0.0.76

interface vlan 40
 ip helper-address 10.0.0.76

interface vlan 99
 ip helper-address 10.0.0.76
```

### DSW-B1, DSW-B2

```
interface vlan 10
 ip helper-address 10.0.0.76

interface vlan 20
 ip helper-address 10.0.0.76

interface vlan 30
 ip helper-address 10.0.0.76

interface vlan 99
 ip helper-address 10.0.0.76
```

### PC1

#### Desktop > Command Prompt

```
ipconfig /renew
ping 10.0.0.76
ping 203.0.113.2
ping 203.0.113.1
```

## Step 3

### SRV1

#### Services > DNS

- DNS Service: On

#### Services > DNS > Resource Records

- Name: google.com
- Type: A Record
- Address: 172.253.62.100

#

- Name: youtube.com
- Type: A Record
- Address: 152.250.31.93

#

- Name: jeremysitlab.com
- Type: A Record
- Address: 66.235.200.145

#

- Name: www.jeremysitlab.com
- Type: CNAME
- Host Name: jeremysitlab.com

### PC1

#### Desktop > Command Prompt

```
ping 10.5.0.4
ping google.com
ping jeremysitlab.com
ping www.jeremysitlab.com
```

## Step 4

### All Devices

```
ip domain name jeremysitlab.com
ip name-server 10.5.0.4
```

```
ping 10.5.0.4
ping google.com
```

## Step 5

### R1

```
ntp master 5
ntp server 216.239.35.0
```

## Step 6

### R1

```
ntp authentication-key 1 md5 ccna
ntp trusted-key 1
```

### All Switches

```
ntp authentication-key 1 md5 ccna
ntp trusted-key 1
ntp server 10.0.0.76 key 1
```

## Steps 7-8

```
show logging
```

### All Devices

```
snmp-server community SNMPSTRING ro

logging 10.5.0.4
logging trap debugging
logging buffered 8192
```

## Step 9

```
show flash
show version
```

### R1

```
ip ftp username cisco
ip ftp password cisco
```

### SRV1 > Services > FTP > File

- Copy file name `c2900-universalk9-mz.SPA.155-3.M4a.bin`

### R1

```
ping 10.5.0.4
```

```
copy ftp flash
 10.5.0.4
 c2900-universalk9-mz.SPA.155-3.M4a.bin
 c2900-universalk9-mz.SPA.155-3.M4a.bin
```

```
boot system flash:c2900-universalk9-mz.SPA.155-3.M4a.bin

write

reload

delete flash:c2900-universalk9-mz.SPA.151-4.M4a.bin
```

## Step 10

```
show ip ssh
```

### All Devices

```
crypto key generate rsa
 4096

ip ssh version 2

access-list 1 permit 10.1.0.0 0.0.0.255

line vty 0 15
 access-class 1 in
 transport input ssh
 login local
 logging synchronous
```

### PC1

#### Desktop > Command Prompt

```
ping 10.0.0.76
ssh -l cisco 10.0.0.76
```

### PC3

#### Desktop > Command Prompt

```
ipconfig /renew
ping 10.0.0.76
ssh -l cisco 10.0.0.76
```

## Step 11

### R1

```
ip nat inside source static 10.5.0.4 203.0.113.113

interface range g0/0/0,g0/1/0
 ip nat outside

interface range g0/0-1
 ip nat inside
```

### SRV1

#### Config > GLOBAL > Settings > Gateway/DNS IPv4 Static

- DNS Server: 10.5.0.4

#### Desktop > Command Prompt

```
ping google.com
```

## Step 12

```
show ip route
```

### R1

```
access-list 2 permit 10.1.0.0 0.0.0.255
access-list 2 permit 10.2.0.0 0.0.0.255
access-list 2 permit 10.3.0.0 0.0.0.255
access-list 2 permit 10.4.0.0 0.0.0.255
access-list 2 permit 10.6.0.0 0.0.0.255
```

```
ip nat pool POOL1 203.0.113.200 203.0.113.207 netmask 255.255.255.248
```

```
ip nat inside source list 2 pool POOL1 overload
```

### PC1

#### Desktop > Command Prompt

```
ping jeremysitlab.com
```

### R1

```
interface g0/0/0
 shutdown

router ospf 1
 no default-information originate
 default-information originate
```

### PC1

#### Desktop > Command Prompt

```
ping jeremysitlab.com
```

### R1

```
interface g0/0/0
 no shutdown

router ospf 1
 no default-information originate
 default-information originate
```

## Step 13

### R1, Core Switches, Distribution Switches

```
no cdp run
lldp run
```

```
write
```

### Access Switches

```
no cdp run
lldp run

interface f0/1
 no lldp transmit
```

```
write
```

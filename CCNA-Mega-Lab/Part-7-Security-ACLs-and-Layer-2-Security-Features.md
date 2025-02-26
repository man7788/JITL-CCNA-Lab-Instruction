# Part 7 - Security: ACLs and Layer-2 Security Features

## Step 1

### DSW-A1, DSW-A2

```
ip access-list extended OfficeA_to_OfficeB
 permit icmp 10.1.0.0 0.0.0.255 10.3.0.0 0.0.0.255
 deny ip 10.1.0.0 0.0.0.255 10.3.0.0 0.0.0.255
 permit ip any any

interface vlan 10
 ip access-group OfficeA_to_OfficeB in
```

```
write
```

## Step 2

### ASW-A1, ASW-B1, ASW-B3

```
interface f0/1
 switchport port-security
 switchport port-security mac-address sticky
 switchport port-security violation restrict
```

### ASW-A2, ASW-A3, ASW-B2

```
interface f0/1
 switchport port-security
 switchport port-security maximum 2
 switchport port-security mac-address sticky
 switchport port-security violation restrict
```

## Step 3

### ASW-A1

```
ip dhcp snooping
ip dhcp snooping vlan 10,20,40,99
no ip dhcp snooping information option

interface range g0/1-2
 ip dhcp snooping trust

interface f0/1
 ip dhcp snooping limit rate 15

interface f0/2
 ip dhcp snooping limit rate 100
```

### ASW-A2, ASW-A3

```
ip dhcp snooping
ip dhcp snooping vlan 10,20,40,99
no ip dhcp snooping information option

interface range g0/1-2
 ip dhcp snooping trust

interface f0/1
 ip dhcp snooping limit rate 15
```

### ASW-B1, ASW-B2, ASW-B3

```
ip dhcp snooping
ip dhcp snooping vlan 10,20,30,99
no ip dhcp snooping information option

interface range g0/1-2
 ip dhcp snooping trust

interface f0/1
 ip dhcp snooping limit rate 15
```

## Step 4

### ASW-A1, ASW-A2, ASW-A3

```
ip arp inspection vlan 10,20,40,99
ip arp inspection validate dst-mac src-mac ip

interface range g0/1-2
 ip arp inspection trust
```

```
write
```

### ASW-B1, ASW-B2, ASW-B3

```
ip arp inspection vlan 10,20,30,99
ip arp inspection validate dst-mac src-mac ip

interface range g0/1-2
 ip arp inspection trust
```

```
write
```

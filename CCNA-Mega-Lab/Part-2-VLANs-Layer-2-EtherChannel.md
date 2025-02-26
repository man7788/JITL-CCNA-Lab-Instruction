# Part 2 - VLANs, Layer-2 EtherChannel

## Step 1

```
show cdp neighbours
show etherchannel summary
```

### DSW-A1, DSW-A2

```
interface range g1/0/4-5
 channel-group 1 mode desirable
```

## Step 2

```
show etherchannel summary
```

### DSW-B1, DSW-B2

```
interface range g1/0/4-5
 channel-group 1 mode active
```

## Step 3

```
show cdp neighbours
```

### DSW-A1, DSW-A2

```
interface range g1/0/1-3
 switchport mode trunk
 switchport nonegotiate
 switchport trunk native vlan 1000
 switchport trunk allowed vlan 10,20,40,99

interface po1
 switchport mode trunk
 switchport nonegotiate
 switchport trunk native vlan 1000
 switchport trunk allowed vlan 10,20,40,99
```

### ASW-A1, ASW-A2, ASW-A3

```
interface range g0/1-2
 switchport mode trunk
 switchport nonegotiate
 switchport trunk native vlan 1000
 switchport trunk allowed vlan 10,20,40,99
```

### DSW-B1, DSW-B2

```
interface range g1/0/1-3
 switchport mode trunk
 switchport nonegotiate
 switchport trunk native vlan 1000
 switchport trunk allowed vlan 10,20,30,99

interface po1
 switchport mode trunk
 switchport nonegotiate
 switchport trunk native vlan 1000
 switchport trunk allowed vlan 10,20,30,99
```

### ASW-B1, ASW-B2, ASW-B3

```
interface range g0/1-2
 switchport mode trunk
 switchport nonegotiate
 switchport trunk native vlan 1000
 switchport trunk allowed vlan 10,20,30,99
```

## Step 4

```
show vtp status
```

### DSW-A1, DSW-B1

```
vtp domain JeremysITLab
vtp version 2
```

## ASW-A1, ASW-A2, ASW-A3, ASW-B1, ASW-B2, ASW-B3

```
vtp mode client
```

## Step 5

```
show vlan brief
```

### DSW-A1

```
vlan 10
 name PCs

vlan 20
 name Phones

vlan 40
 name Wi-Fi

vlan 99
 name Management
```

## Step 6

```
show vlan brief
```

### DSW-B1

```
vlan 10
 name PCs

vlan 20
 name Phones

vlan 30
 name Servers

vlan 99
 name Management
```

## Step 7

### ASW-A1, ASW-B1

```
interface f0/1
 switchport mode access
 switchport mode nonegotiate
 switchport access vlan 99
```

### ASW-A2, ASW-A3, ASW-B2

```
interface f0/1
 switchport mode access
 switchport nonegotiate
 switchport access vlan 10
 switchport voice vlan 20
```

### ASW-B3

```
interface f0/1
 switchport mode access
 switchport nonegotiate
 switchport access vlan 30
```

## Step 8

### ASW-A1

```
interface f0/2
 switchport mode trunk
 switchport trunk allowed vlan 40,99
 switchport trunk native vlan 99
 switchport nonegotiate
```

## Step 9

```
show interfaces status
```

### DSW-A1, DSW-A2, DSW-B1, DSW-B2

```
interface range g1/0/6-24,g1/1/3-4
 shutdown
```

```
write
```

### ASW-A1

```
interface range f0/3-24
 shutdown
```

```
write
```

### ASW-A2, ASW-A3, ASW-B1, ASW-B2, ASW-B3

```
interface range f0/2-24
 shutdown
```

```
write
```

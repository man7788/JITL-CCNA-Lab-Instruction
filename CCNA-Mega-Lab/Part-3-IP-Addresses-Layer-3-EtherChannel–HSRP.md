# Part 3 - IP Addresses, Layer-3 EtherChannel, HSRP

## Step 1

```
show ip interface brief
```

### R1

```
interface range g0/0/0,g0/1/0
 ip address dhcp
 no shutdown

interface g0/0
 ip address 10.0.0.33 255.255.255.252
 no shutdown

interface g0/1
 ip address 10.0.0.37 255.255.255.252
 no shutdown

interface loopback 0
 ip address 10.0.0.76 255.255.255.255
```

```
write
```

## Step 2

### CSW1, CSW2, DSW-A1, DSW-A2, DSW-B1, DSW-B2

```
ip routing
```

## Step 3

```
show cdp neighbors
show etherchannel summary
```

### CSW1

```
interface range g1/0/2-3
 no switchport
 channel-group 1 mode desirable

interface port-channel 1
 ip address 10.0.0.41 255.255.255.252
```

### CSW2

```
interface range g1/0/2-3
 no switchport
 channel-group 1 mode desirable

interface port-channel 1
 ip address 10.0.0.42 255.255.255.252
```

```
ping 10.0.0.41
```

## Step 4

### CSW1

```
interface g1/0/1
 no switchport
 ip address 10.0.0.34 255.255.255.252

interface g1/1/1
 no switchport
 ip address 10.0.0.45 255.255.255.252

interface g1/1/2
 no switchport
 ip address 10.0.0.49 255.255.255.252

interface g1/1/3
 no switchport
 ip address 10.0.0.53 255.255.255.252

interface g1/1/4
 no switchport
 ip address 10.0.0.57 255.255.255.252

interface loopback 0
 ip address 10.0.0.77 255.255.255.255

interface range g1/0/4-24
 shutdown
```

```
write
```

## Step 5

### CSW2

```
interface g1/0/1
 no switchport
 ip address 10.0.0.38 255.255.255.252

interface g1/1/1
 no switchport
 ip address 10.0.0.61 255.255.255.252

interface g1/1/2
 no switchport
 ip address 10.0.0.65 255.255.255.252

interface g1/1/3
 no switchport
 ip address 10.0.0.69 255.255.255.252

interface g1/1/4
 no switchport
 ip address 10.0.0.73 255.255.255.252

interface loopback 0
 ip address 10.0.0.78 255.255.255.255

interface range g1/0/4-24
 shutdown
```

```
write
```

## Step 6

### DSW-A1

```
interface g1/1/1
 no switchport
 ip address 10.0.0.46 255.255.255.252

interface g1/1/2
 no switchport
 ip address 10.0.0.62 255.255.255.252

interface loopback 0
 ip address 10.0.0.79 255.255.255.255
```

## Step 7

### DSW-A2

```
interface g1/1/1
 no switchport
 ip address 10.0.0.50 255.255.255.252

interface g1/1/2
 no switchport
 ip address 10.0.0.66 255.255.255.252

interface loopback 0
 ip address 10.0.0.80 255.255.255.255
```

## Step 8

### DSW-B1

```
interface g1/1/1
 no switchport
 ip address 10.0.0.54 255.255.255.252

interface g1/1/2
 no switchport
 ip address 10.0.0.70 255.255.255.252

interface loopback 0
 ip address 10.0.0.81 255.255.255.255
```

## Step 9

### DSW-B2

```
interface g1/1/1
 no switchport
 ip address 10.0.0.58 255.255.255.252

interface g1/1/2
 no switchport
 ip address 10.0.0.74 255.255.255.252

interface loopback 0
 ip address 10.0.0.82 255.255.255.255
```

## Step 10

### SRV1 > Config

#### GLOBAL > Settings > Gateway/DNS IPv4 Static

- Default Gateway: 10.5.0.1

#### INTERFACE > FastEthernet0 > IP Configuration Static

- IPv4 Address: 10.5.0.4
- Subnet Mask: 255.255.255.0

## Step 11

### ASW-A1

```
ip default-gateway 10.0.0.1

interface vlan 99
 ip address 10.0.0.4 255.255.255.240
```

```
write
```

### ASW-A2

```
ip default-gateway 10.0.0.1

interface vlan 99
 ip address 10.0.0.5 255.255.255.240
```

```
write
```

### ASW-A3

```
ip default-gateway 10.0.0.1

interface vlan 99
 ip address 10.0.0.6 255.255.255.240
```

```
write

```

### ASW-B1

```
ip default-gateway 10.0.0.17

interface vlan 99
 ip address 10.0.0.20 255.255.255.240
```

```
write
```

### ASW-B2

```
ip default-gateway 10.0.0.17

interface vlan 99
 ip address 10.0.0.21 255.255.255.240
```

```
write
```

### ASW-B3

```
ip default-gateway 10.0.0.17

interface vlan 99
 ip address 10.0.0.22 255.255.255.240
```

```
write
```

## Step 12

### DSW-A1

```
interface vlan 99
 ip address 10.0.0.2 255.255.255.240
 standby version 2
 standby 1 ip 10.0.0.1
 standby 1 priority 105
 standby 1 preempt
```

### DSW-A2

```
interface vlan 99
 ip address 10.0.0.3 255.255.255.240
 standby version 2
 standby 1 ip 10.0.0.1
```

## Step 13

### DSW-A1

```
interface vlan 10
 ip address 10.1.0.2 255.255.255.0
 standby version 2
 standby 2 ip 10.1.0.1
 standby 2 priority 105
 standby 2 preempt
```

### DSW-A2

```
interface vlan 10
 ip address 10.1.0.3 255.255.255.0
 standby version 2
 standby 2 ip 10.1.0.1
```

## Step 14

### DSW-A2

```
interface vlan 20
 ip address 10.2.0.3 255.255.255.0
 standby version 2
 standby 3 ip 10.2.0.1
 standby 3 priority 105
 standby 3 preempt
```

### DSW-A1

```
interface vlan 20
 ip address 10.2.0.2 255.255.255.0
 standby version 2
 standby 3 ip 10.2.0.1
```

## Step 15

### DSW-A2

```
interface vlan 40
 ip address 10.6.0.3 255.255.255.0
 standby version 2
 standby 4 ip 10.6.0.1
 standby 4 priority 105
 standby 4 preempt
```

```
write
```

### DSW-A1

```
interface vlan 40
 ip address 10.6.0.2 255.255.255.0
 standby version 2
 standby 4 ip 10.6.0.1
```

```
write
```

## Steps 16-19

### DSW-B1

```
interface vlan 99
 ip address 10.0.0.18 255.255.255.240
 standby version 2
 standby 1 ip 10.0.0.17
 standby 1 priority 105
 standby 1 preempt

interface vlan 10
 ip address 10.3.0.2 255.255.255.0
 standby version 2
 standby 2 ip 10.3.0.1
 standby 2 priority 105
 standby 2 preempt

interface vlan 20
 ip address 10.4.0.2 255.255.255.0
 standby version 2
 standby 3 ip 10.4.0.1

interface vlan 30
 ip address 10.5.0.2 255.255.255.0
 standby version 2
 standby 4 ip 10.5.0.1
```

```
write
```

### DSW-B2

```
interface vlan 99
 ip address 10.0.0.19 255.255.255.240
 standby version 2
 standby 1 ip 10.0.0.17

interface vlan 10
 ip address 10.3.0.3 255.255.255.0
 standby version 2
 standby 2 ip 10.3.0.1

interface vlan 20
 ip address 10.4.0.3 255.255.255.0
 standby version 2
 standby 3 ip 10.4.0.1
 standby 3 priority 105
 standby 3 preempt

interface vlan 30
 ip address 10.5.0.3 255.255.255.0
 standby version 2
 standby 4 ip 10.5.0.1
 standby 4 priority 105
 standby 4 preempt
```

```
write
```

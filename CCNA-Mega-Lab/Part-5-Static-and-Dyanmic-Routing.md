# Part 5 - Static and Dyanmic Routing

## Step 1

```
show ip interface brief | exclude unassigned
show ip ospf
show ip ospf neighbor
```

### R1

```
router ospf 1
 router-id 10.0.0.76
 passive-interface loopback 0

interface loopback 0
 ip ospf 1 area 0

interface range g0/0-1
 ip ospf 1 area 0
 ip ospf network point-to-point
```

### CSW1

```
router ospf 1
 router-id 10.0.0.77
 passive-interface loopback 0
 network 10.0.0.41 0.0.0.0 area 0
 network 10.0.0.34 0.0.0.0 area 0
 network 10.0.0.45 0.0.0.0 area 0
 network 10.0.0.49 0.0.0.0 area 0
 network 10.0.0.53 0.0.0.0 area 0
 network 10.0.0.57 0.0.0.0 area 0
 network 10.0.0.77 0.0.0.0 area 0

interface range g1/0/1,g1/1/1-4
 ip ospf network point-to-point
```

```
write
```

### CSW2

```
router ospf 1
 router-id 10.0.0.78
 passive-interface loopback 0
 network 10.0.0.42 0.0.0.0 area 0
 network 10.0.0.38 0.0.0.0 area 0
 network 10.0.0.61 0.0.0.0 area 0
 network 10.0.0.65 0.0.0.0 area 0
 network 10.0.0.69 0.0.0.0 area 0
 network 10.0.0.73 0.0.0.0 area 0
 network 10.0.0.78 0.0.0.0 area 0

interface range g1/0/1,g1/1/1-4
 ip ospf network point-to-point
```

```
write
```

### DSW-A1

```
router ospf 1
 router-id 10.0.0.79
 passive-interface loopback 0
 passive-interface vlan 10
 passive-interface vlan 20
 passive-interface vlan 40
 network 10.0.0.46 0.0.0.0 area 0
 network 10.0.0.62 0.0.0.0 area 0
 network 10.0.0.79 0.0.0.0 area 0
 network 10.1.0.2 0.0.0.0 area 0
 network 10.2.0.2 0.0.0.0 area 0
 network 10.0.0.2 0.0.0.0 area 0
 network 10.6.0.2 0.0.0.0 area 0

interface range g1/1/1-2
 ip ospf network point-to-point
```

```
write
```

### DSW-A2

```
router ospf 1
 router-id 10.0.0.80
 passive-interface loopback 0
 passive-interface vlan 10
 passive-interface vlan 20
 passive-interface vlan 40
 network 10.0.0.50 0.0.0.0 area 0
 network 10.0.0.66 0.0.0.0 area 0
 network 10.0.0.80 0.0.0.0 area 0
 network 10.1.0.3 0.0.0.0 area 0
 network 10.2.0.3 0.0.0.0 area 0
 network 10.0.0.3 0.0.0.0 area 0
 network 10.6.0.3 0.0.0.0 area 0

interface range g1/1/1-2
 ip ospf network point-to-point
```

```
write
```

### DSW-B1

```
router ospf 1
 router-id 10.0.0.81
 passive-interface loopback 0
 passive-interface vlan 10
 passive-interface vlan 20
 passive-interface vlan 30
 network 10.0.0.54 0.0.0.0 area 0
 network 10.0.0.70 0.0.0.0 area 0
 network 10.0.0.81 0.0.0.0 area 0
 network 10.3.0.2 0.0.0.0 area 0
 network 10.4.0.2 0.0.0.0 area 0
 network 10.5.0.2 0.0.0.0 area 0
 network 10.0.0.18 0.0.0.0 area 0

interface range g1/1/1-2
 ip ospf network point-to-point
```

```
write
```

### DSW-B2

```
router ospf 1
 router-id 10.0.0.82
 passive-interface loopback 0
 passive-interface vlan 10
 passive-interface vlan 20
 passive-interface vlan 30
 network 10.0.0.58 0.0.0.0 area 0
 network 10.0.0.74 0.0.0.0 area 0
 network 10.0.0.82 0.0.0.0 area 0
 network 10.3.0.3 0.0.0.0 area 0
 network 10.4.0.3 0.0.0.0 area 0
 network 10.5.0.3 0.0.0.0 area 0
 network 10.0.0.19 0.0.0.0 area 0

interface range g1/1/1-2
 ip ospf network point-to-point
```

```
write
```

## Step 2

```
show ip interface <interface>
show ip route
```

### R1

```
ping 203.0.113.1 (ISP's address)
ping 203.0.113.5 (ISP's address)
```

```
ip route 0.0.0.0 0.0.0.0 203.0.113.1
ip route 0.0.0.0 0.0.0.0 203.0.113.5 2

router ospf 1
 default-information originate
```

```
write
```

### DSW2-B2

```
ping 203.0.113.2
ping 203.0.113.1
```

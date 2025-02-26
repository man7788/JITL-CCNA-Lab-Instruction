# Part 8 - IPv6

## Step 1

```
show ipv6 interface brief
```

### R1

```
ipv6 unicast-routing

interface g0/0/0
 ipv6 address 2001:db8:a::2/64

interface g0/1/0
 ipv6 address 2001:db8:b::2/64

interface g0/0
 ipv6 address 2001:db8:a1::/64 eui-64

interface g0/1
 ipv6 address 2001:db8:a2::/64 eui-64
```

### CSW-1

```
ipv6 unicast-routing

interface g1/0/1
 ipv6 address 2001:db8:a1::/64 eui-64
```

### CSW-2

```
ipv6 unicast-routing

interface g1/0/1
  ipv6 address 2001:db8:a2::/64 eui-64
```

### CSW-1, CSW-2

```
interface port-channel 1
 ipv6 enable
```

```
write
```

## Step 2

### R1

```
ipv6 route ::/0 2001:db8:a::1
ipv6 route ::/0 g0/1/0 2001:db8:b::1 2
```

```
write
```

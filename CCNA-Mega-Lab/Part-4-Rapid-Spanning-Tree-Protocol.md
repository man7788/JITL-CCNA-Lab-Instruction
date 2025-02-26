# Part 4 - Rapid Spanning Tree Protocol

## Step 1

```
show spanning-tree <vlan>
```

#

### DSW-A1, DSW-A2, ASW-A1, ASW-A2, ASW-A3

### DSW-B1, DSW-B2, ASW-B1, ASW-B2, ASW-B3

```
spanning-tree mode rapid-pvst
```

### DSW-A1

```
spanning-tree vlan 10,99 priority 0
spanning-tree vlan 20,40 priority 4096
```

```
write
```

### DSW-A2

```
spanning-tree vlan 20,40 priority 0
spanning-tree vlan 10,99 priority 4096
```

```
write

```

### DSW-B1

```
spanning-tree vlan 10,99 priority 0
spanning-tree vlan 20,30 priority 4096
```

```
write
```

### DSW-B2

```
spanning-tree vlan 20,30 priority 0
spanning-tree vlan 10,99 priority 4096
```

```
write
```

## Step 2

### ASW-A1

```
interface f0/1
 spanning-tree portfast
 spanning-tree bpduguard enable

interface f0/2
 spanning-tree portfast trunk
 spanning-tree bpduguard enable
```

```
write
```

### ASW-A2, ASW-A3, ASW-B1, ASW-B2, ASW-B3

```
interface f0/1
 spanning-tree portfast
 spanning-tree bpduguard enable
```

```
write
```

# Part 1 - Initial Setup

## Step 1

```
hostname <hostname>
```

```
write
```

## Steps 2-4

### R1, Access switches

```
enable secret jeremysitlab
username cisco secret ccna

line console 0
 login local
 exec-timeout 30
 logging synchronous
```

```
write
```

### Core, Distribution switches

```
enable algorithm-type scrypt secret jeremysitlab
username cisco algorithm-type scrypt secret ccna

line console 0
 login local
 exec-timeout 30
 logging synchronous
```

```
write
```

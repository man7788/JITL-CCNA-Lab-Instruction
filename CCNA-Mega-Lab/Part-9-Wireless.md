# Part 9 - Wireless

## Step 1

### PC1 > Desktop > Command Prompt

```
ping 10.0.0.7
```

### PC1 > Desktop > Web Browser

- URL: https://10.0.0.7
- User Name: admin
- Password: adminPW12

## Step 2

### WLC1 GUI

#### CONTROLLER > Interfaces > New

- Interface Name: Wi-Fi
- VLAN Id: 40

#### CONTROLLER > Interfaces > Edit > Physical Information

- Port Number: 1

#### CONTROLLER > Interfaces > Edit > Interface Address

- VLAN Identifer: 40
- IP Address: 10.6.0.4
- Netmask: 255.255.255.0
- Gateway: 10.6.0.1

#### CONTROLLER > Interfaces > Edit > DHCP Information

- Primary DHCP Server: 10.0.0.76

## Step 3

### WLC1 GUI

#### WLANs > New

- Type: WLAN
- Profile Name: Wi-Fi
- SSID: Wi-Fi
- ID: 1

#### WLANs > Edit 'Wi-Fi' > General

- Status: ✔ Enabled
- Interface/Interface Group(G): Wi-Fi

#### WLANs > Edit 'Wi-Fi' > Security

- Layer 2 Security: WPA+WPA2

#### WLANs > Edit 'Wi-Fi' > Security > WPA+WPA2 Parameters

- WPA2 Policy: ✔
- WPA2 Encryption: ✔ AES

#### WLANs > Edit 'Wi-Fi' > Security > Authenication Key Management

- PSK: ✔
- PSK Format ASCII: cisco123

## Step 4

### Laptop 1 > Config > Wireless0

- SSID: Wi-Fi
- ✔ WPA2 PSK Pass Phrase: cisco123
- Encryption Type: AES

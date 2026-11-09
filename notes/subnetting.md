# Subnetting

## Method (for /25-/30)
1. Host bits = 32 - prefix
2. Block size = 2 to the power of host bits
3. Netmask = 255.255.255.(256 - block size)
4. Borders of block: I write out blocks using a step of 0, N, 2N, 3N, ... and determine between which two numbers the last octet of the address falls
5. Network = left border
6. Broadcast = next border - 1
7. HostMin = left border + 1
8. HostMax = broadcast - 1
9. Hosts = block size - 2

## Block sizes (/24-/30)

| Prefix | Netmask | Block size | Subnets in /24 | Hosts |
|---|---|---|---|---|
| /24 | 255.255.255.0 | 256 | 1 | 254 |
| /25 | 255.255.255.128 | 128 | 2 | 126 |
| /26 | 255.255.255.192 | 64 | 4 | 62 |
| /27 | 255.255.255.224 | 32 | 8 | 30 |
| /28 | 255.255.255.240 | 16 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 32 | 6 |
| /30 | 255.255.255.252 | 4 | 64 | 2 |

Special cases: /31 is used to connect 2 devices (without address of the network and broadcast), /32 is used to set the path to a specific IP

## How to determine if an IP address is public, private or special
- The addresses `10.x.x.x/8` are private
- The addresses `172.16.x.x/12` (`172.16.x.x` - `172.31.x.x`) are private
- The addresses `192.168.x.x/16` are private
- `127.x.x.x/8` are loopback IPs
- `169.254.x.x/16` are self-assigned fallback IPs (when host failed to get IP from DHCP)
- Most other addresses are public (a few reserved ranges exist, e.g. 100.64.0.0/10 and 224.0.0.0/4)

## Worked examples (/24/-30)
### 1. `172.16.33.200/25`
- Host bits: 7
- Block size: 128
- Borders: 0, 128, 256
- Network: `172.16.33.128/25`
- Broadcast: `172.16.33.255`
- HostMin: `172.16.33.129`
- HostMax: `172.16.33.254`
- Hosts: 126
- ipcalc check:
<img width="768" height="255" alt="image" src="https://github.com/user-attachments/assets/01f7bdcc-6459-4caa-b4c6-035e92a82e5f" />

### 2. `192.168.45.99/26`
- Host bits: 6
- Block size: 64
- Borders: 0, 64, 128, 192, 256
- Network: `192.168.45.64/26`
- Broadcast: `192.168.45.127`
- HostMin: `192.168.45.65`
- HostMax: `192.168.45.126`
- Hosts: 62
- ipcalc check:
<img width="820" height="259" alt="image" src="https://github.com/user-attachments/assets/18e58936-0c5d-4b6a-b16f-1ea97b2b2dda" />

### 3. `10.50.8.140/27`
- Host bits: 5
- Block size: 32
- Borders: 0, 32, 64, 96, 128, 160, 192, 224, 256
- Network: `10.50.8.128/27`
- Broadcast: `10.50.8.159`
- HostMin: `10.50.8.129`
- HostMax: `10.50.8.158`
- Hosts: 30
- ipcalc check:
<img width="820" height="259" alt="image" src="https://github.com/user-attachments/assets/3d225d81-592d-43e9-bb2f-8f79a0f75578" />

### 4. `192.168.200.83/28`
- Host bits: 4
- Block size: 16
- Borders: 0, 16, 32, 48, 64, 80, 96, 112, 128, 144, 160, 176, 192, 208, 224, 240, 256
- Network: `192.168.200.80/28`
- Broadcast: `192.168.200.95`
- HostMin: `192.168.200.81`
- HostMax: `192.168.200.94`
- Hosts: 14
- ipcalc check:
<img width="820" height="259" alt="image" src="https://github.com/user-attachments/assets/f4333050-297d-40d2-8d33-91ad91206217" />

### 5. `10.0.5.22/29`
- Host bits: 3
- Block size: 8
- Borders: 0, 8, 16, 24, 32, 40, 48, 56, 64, 72, 80, 88, 96, 104, 112, 120, 128, 136, 144, ...
- Network: `10.0.5.16/29`
- Broadcast: `10.0.5.23`
- HostMin: `10.0.5.17`
- HostMax: `10.0.5.22`
- Hosts: 6
- ipcalc check:
<img width="820" height="259" alt="image" src="https://github.com/user-attachments/assets/cecf5c67-8412-47c8-a53b-dbb29f369af2" />

### 6. `172.20.9.64/30`
- Host bits: 2
- Block size: 4
- Borders: 0, 4, 8, 12, 16, 20, 24, 28, 32, 36, 40, 44, 48, 52, 56, 60, 64, 68, 72, 76, 80, ...
- Network: `172.20.9.64/30`
- Broadcast: `172.20.9.67`
- HostMin: `172.20.9.65`
- HostMax: `172.20.9.66`
- Hosts: 2
- ! It can't be assigned to a host, bc this is an IP address of network
- ipcalc check:
<img width="820" height="259" alt="image" src="https://github.com/user-attachments/assets/9abfcc07-a1a9-4947-be00-424bef42149b" />

## Method for /16-/23
1. Block size is in the 3rd octet: 2 to the power of (24 - prefix)
2. Netmask = 255.255.(256 - block size).0
3. Block borders are also in the 3rd octet
4. Network = first two octets, left border, `.0`
5. Broadcast = first two octets, next border - 1, `.255`
6. HostMin = network + 1 (last octet `.1`)
7. HostMax = broadcast - 1 (last octet `.254`)
8. Hosts = block size * 256 - 2

Everything else is similar to /24-/30

## Block sizes (/16-/23)
| Prefix | Netmask | Block size (3rd octet) | Hosts |
|---|---|---|---|
| /16 | 255.255.0.0 | 256 (whole octet) | 65534 |
| /17 | 255.255.128.0 | 128 | 32766 |
| /18 | 255.255.192.0 | 64 | 16382 |
| /19 | 255.255.224.0 | 32 | 8190 |
| /20 | 255.255.240.0 | 16 | 4094 |
| /21 | 255.255.248.0 | 8 | 2046 |
| /22 | 255.255.252.0 | 4 | 1022 |
| /23 | 255.255.254.0 | 2 | 510 |

## Worked examples (/16-/23)
### 1. `10.77.150.20/22`
- Host bits: 10
- Block size: 4
- Borders: 0, 4, 8, 12, 16, 20, 24, 28, 32, 36, 40, 44, 48, 52, 56, 60, 64, 68, 72, 76, 80, 84, 88, 92, 96, 100, 104, 108, 112, 116, 120, 124, 128, 132, 136, 140, 144, 148, 152, 156, 160
- Network: 10.77.148.0/22
- Broadcast: 10.77.151.255
- HostMin: 10.77.148.1
- HostMax: 10.77.151.254
- Hosts: 1022
- ipcalc check:
<img width="775" height="275" alt="image" src="https://github.com/user-attachments/assets/0b8ffb8e-9538-41b2-b40d-dbf0fde514e1" />

### 2. `172.18.200.45/20`
- Host bits: 12
- Block size: 16
- Borders: 0, 16, 32, 48, 64, 80, 96, 112, 128, 144, 160, 176, 192, 208
- Network: 172.18.192.0/20
- Broadcast: 172.18.207.255
- HostMin: 172.18.192.1
- HostMax: 172.18.207.254
- Hosts: 4094
- ipcalc check:
<img width="775" height="275" alt="image" src="https://github.com/user-attachments/assets/3c662ad3-ea68-45fa-8be7-8fce1315b17b" />

### 3. `192.168.77.10/23`
- Host bits: 9
- Block size: 2
- Borders: 0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52, 54, 56, 58, 60, 62, 64, 66, 68, 70, 72, 74, 76, 78
- Network: 192.168.76.0/23
- Broadcast: 192.168.77.255
- HostMin: 192.168.76.1
- HostMax: 192.168.77.254
- Hosts: 510
- ipcalc check:
<img width="775" height="275" alt="image" src="https://github.com/user-attachments/assets/56037cc4-2ab5-4353-b469-8ed4533ad79e" />

### 4. `10.200.130.5/17`
- Host bits: 15
- Block size: 128
- Borders: 0, 128, 256
- Network: 10.200.128.0/17
- Broadcast: 10.200.255.255
- HostMin: 10.200.128.1
- HostMax: 10.200.255.254
- Hosts: 32766
- ipcalc check:
<img width="775" height="275" alt="image" src="https://github.com/user-attachments/assets/e91ce445-5729-499c-a49a-cc0c75c84fcd" />

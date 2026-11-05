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

## Block sizes

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
- The addresses `172.16.0.0/12` (`172.16.x.x` - `172.31.x.x`) are private
- The addresses `192.168.x.x/16` are private
- `127.x.x.x/8` is loopback address
- `169.254.x.x/16` is self-assigned fallback IPs (when host failed to get IP from DHCP)
- Most other addresses are public (a few reserved ranges exist, e.g. 100.64.0.0/10 and 224.0.0.0/4)

## Worked examples
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

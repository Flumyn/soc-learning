# ARP in Wireshark

## Goal
In this lab I want to see how ARP requests work using Wireshark

## Setup
- OS: Kali Linux 2026.3 (kernel 7.1.5+kali-amd64)
- Environment: physical machine
- Network: 192.168.10.0/24
- Gateway: 192.168.10.1
- Host: 192.168.10.123
- Interface: wlan0
- Tools used: Wireshark 4.6.6, `ip` and `ping`

## Steps
1. Firstly I started capturing traffic in Wireshark on wlan0 using the "arp" filter
 <img width="737" height="287" alt="image" src="https://github.com/user-attachments/assets/1fed22c2-c3c3-448a-8604-5c4ab93344ec" />

2. Then I flushed the ARP table on my host
 <img width="333" height="143" alt="image" src="https://github.com/user-attachments/assets/0b46de54-be33-4c51-ad84-d124d2edf7c0" />

3. Next I pinged the gateway and captured the ARP request from my host to broadcast
 <img width="1129" height="455" alt="image" src="https://github.com/user-attachments/assets/ab809f91-109f-45fe-929c-23b39e2713fd" />
 <img width="1000" height="359" alt="image" src="https://github.com/user-attachments/assets/3e167963-4217-4a6b-b467-e6ad0827a7c5" />
 <img width="1000" height="359" alt="image" src="https://github.com/user-attachments/assets/161e5459-192e-442f-9e3b-f9af65c54b39" />


4. We can see the MAC address of the gateway that appeared in the ARP table on my host
 <img width="649" height="117" alt="image" src="https://github.com/user-attachments/assets/7337e6bc-c076-4fe1-8ae0-31248230104c" />


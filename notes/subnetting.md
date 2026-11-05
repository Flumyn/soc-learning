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

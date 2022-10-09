---
description: Pre-Scanning Configuration
---

# Setup

## Target Designation

```
echo <IPv4> > ~/.kcp/TARGET
```

## Packet Capture

```
sudo tcpdump -i tun0 -w - -U | tee /home/kali/KCP/OSCP/pcaps/$(dtg).pcap | tcpdump -r -
```

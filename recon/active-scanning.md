# Active Scanning

## DNS Scanning

```shell
sudo nmap -sU -p 53 --open 192.168.X.0/24 -v -oG nameservers.txt
cat nameservers.txt | grep 53/open/ | cut -d ' ' -f2 > dnsservers.txt
for srv in $(cat dnsservers.txt); do echo "Asking $srv to lookup $TARGET:"; nslookup $TARGET $srv; done
```

### DNSRecon

`for srv in $(cat dnsservers.txt); do dnsrecon -n $srv -a -d <domain>; done`

```
dnsrecon -d <domain> -a
dnsrecon -d <domain> -t axfr
dnsrecon -d <domain> -D <namelist> -t brt
dnsrecon -d <startIP-endIP>
```

### Sublis3r

```
sublist3r -d <domain>
sublist3r -v -d <domain> -p 80,443
```

### OWASP AMASS

```
amass enum -d <domain>
amass intel -whois -d <domain>
amass intel -active 192.168.X.0/24 -p 80,443,8080,8443
amass intel -ipv4 -whois -d <domain>
```

## Network Scanning

### Pingsweep

#### Linux

`for i in {1..254} ;do (ping -c 1 172.21.10.$i | grep "bytes from" &) ;done`

#### Windows

`for /L %i in (1,1,255) do @ping -n 1 -w 200 172.21.10.%i > nul && echo 172.21.1.%i is up`

### ARP

`netdiscover -i tun0`

`netdiscover -r 192.168.X.0/24`

### nmap

`nmap -sn 192.168.X.0/24`

### nbtscan

`nbtscan -r 192.168.X.0/24`

## Host Scanning

```
autorecon $TARGET
```

To restore permissions:

```
sudo chown -R kali:kali /home/kali/KCP/OSCP/results/$TARGET
```

### TCP

`sudo nmap --privileged -O --fuzzy -Pn -sC -sV -p $(sudo nmap --privileged -Pn -p 1-65535 -sS --min-rate=1000 -T4 $target 2>/dev/null | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed 's/,$//') $TARGET -oX nmap-tcp-${TARGET}.xml`

#### Stealth

`nmap -sS -sC -sV $TARGET`

`nmap -sS -p- $TARGET`

### UDP

`sudo nmap --privileged -Pn -sC -sV -sU -p $(sudo nmap --privileged -Pn -p 1-65535 -sU --min-rate=1000 -T4 $target 2>/dev/null | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed 's/,$//') $TARGET -oX nmap-udp-${TARGET}.xml`

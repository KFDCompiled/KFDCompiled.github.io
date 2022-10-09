---
description: Web Service Enumeration
---

# HTTP(S)

## General Enumeration

### sitemap

```
curl http://${TARGET}:80/sitemap.xml -o /home/kali/KCP/OSCP/results/${TARGET}/scans/tcp80/sitemap.xml
```

### robots

```
curl http://${TARGET}:80/robots.txt -o /home/kali/KCP/OSCP/results/${TARGET}/scans/tcp80/robots.txt
```

### whatweb

```
whatweb --log-brief=/home/kali/KCP/OSCP/results/${TARGET}/scans/tcp80/tcp_80_http_whatweb.txt -v $TARGET
```

### nikto

```
nikto -ask=no -h http://${TARGET}:80 2>&1 | tee "/home/kali/KCP/OSCP/results/${TARGET}/scans/tcp80/tcp_80_http_nikto.txt"
```

### feroxbuster

```
feroxbuster -u http://${TARGET}:80 -t 50 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x "txt,html,php,asp,aspx,jsp" -v -k -n -e -o /home/kali/KCP/OSCP/results/${TARGET}/scans/tcp80/tcp_80_http_feroxbuster_dirbuster.txt
```

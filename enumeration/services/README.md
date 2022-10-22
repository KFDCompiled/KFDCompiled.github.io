---
description: Service Enumeration
---

# Services

## Active Directory

{% content-ref url="../active-directory/" %}
[active-directory](../active-directory/)
{% endcontent-ref %}

## FTP

```
$ ls -lh /usr/share/nmap/scripts/ | grep ftp
-rw-r--r-- 1 root root 4.5K Oct 12 09:29 ftp-anon.nse
-rw-r--r-- 1 root root 3.2K Oct 12 09:29 ftp-bounce.nse
-rw-r--r-- 1 root root 3.1K Oct 12 09:29 ftp-brute.nse
-rw-r--r-- 1 root root 3.2K Oct 12 09:29 ftp-libopie.nse
-rw-r--r-- 1 root root 3.3K Oct 12 09:29 ftp-proftpd-backdoor.nse
-rw-r--r-- 1 root root 3.7K Oct 12 09:29 ftp-syst.nse
-rw-r--r-- 1 root root 5.9K Oct 12 09:29 ftp-vsftpd-backdoor.nse
-rw-r--r-- 1 root root 5.8K Oct 12 09:29 ftp-vuln-cve2010-4221.nse
-rw-r--r-- 1 root root 5.7K Oct 12 09:29 tftp-enum.nse
```

## HTTP(S)

{% content-ref url="http-s.md" %}
[http-s.md](http-s.md)
{% endcontent-ref %}

## MAIL

### SMTP \[25,465,587]

[https://book.hacktricks.xyz/network-services-pentesting/pentesting-smtp](https://book.hacktricks.xyz/network-services-pentesting/pentesting-smtp)

### IMAP \[143,993]

[https://book.hacktricks.xyz/network-services-pentesting/pentesting-imap](https://book.hacktricks.xyz/network-services-pentesting/pentesting-imap)

### POP3 \[110,995]

[https://book.hacktricks.xyz/network-services-pentesting/pentesting-pop](https://book.hacktricks.xyz/network-services-pentesting/pentesting-pop)

## NetBIOS

```
nbtscan $TARGET
nmap --script nbstat.nse $TARGET
nmap --script smb-os-discovery $TARGET
nmblookup -A $TARGET
enum4linux -a $TARGET
```

## (MS)RPC

```
rpcinfo $TARGET -p
rpcinfo $TARGET -s
rpcclient -U "" -N $TARGET

#Dump user information
/usr/share/doc/python3-impacket/examples/samrdump.py -port 139 [[domain/]username[:password]@]<targetName or address>
/usr/share/doc/python3-impacket/examples/samrdump.py -port 445 [[domain/]username[:password]@]<targetName or address>

#Map possible RPC endpoints
/usr/share/doc/python3-impacket/examples/rpcdump.py -port 135 [[domain/]username[:password]@]<targetName or address>
/usr/share/doc/python3-impacket/examples/rpcdump.py -port 139 [[domain/]username[:password]@]<targetName or address>
/usr/share/doc/python3-impacket/examples/rpcdump.py -port 445 [[domain/]username[:password]@]<targetName or address>

#connect with username & hash
rpcclient //machine.htb -U domain.local/USERNAME%754d87d42adabcca32bdb34a876cbffb  --pw-nt-hash

#authenticate against kerberos
rpcclient -k ws01win10.domain.com

#while connected to rpcclient
List domains: enumdomains
Get SID: lsaquery
Domain info: querydominfo
List users: querydispinfo and enumdomusers
Get user details: queryuser <0xrid>
Get user groups: queryusergroups <0xrid>
GET SID of a user: lookupnames <username>
Get users aliases: queryuseraliases [builtin|domain] <sid>
List groups: enumdomgroups
Get group details: querygroup <0xrid>
Get group members: querygroupmem <0xrid>
Find SIDs by name: lookupnames <username>
Find more SIDs: lsaenumsid
RID cycling (check more SIDs): lookupsids <sid>
List alias: enumalsgroups <builtin|domain>
Get members: queryaliasmem builtin|domain <0xrid>
```

## RDP

{% content-ref url="rdp.md" %}
[rdp.md](rdp.md)
{% endcontent-ref %}

## SNMP

{% content-ref url="snmp.md" %}
[snmp.md](snmp.md)
{% endcontent-ref %}

## SMB

{% content-ref url="smb-139-445.md" %}
[smb-139-445.md](smb-139-445.md)
{% endcontent-ref %}

## (my/ms)SQL

[https://www.mysqltutorial.org/mysql-cheat-sheet.aspx](https://www.mysqltutorial.org/mysql-cheat-sheet.aspx)

### m\*sql

```
mysql -u<USER> -p<PASS> -e '<CMD>;'

sqsh -S<config> -D<database> -U <domain>\\<user> -P <password / hash>
```

```
sudo nmap -sV -p 3306 --script mysql-audit,mysql-databases,mysql-dump-hashes,mysql-empty-password,mysql-enum,mysql-info,mysql-query,mysql-users,mysql-variables,mysql-vuln-cve2012-2122 $TARGET -oX scans/xml/nmapsqlscripts.xml | tee scans/tcp3306/nmapsqlscripts.txt
```

### `noSQL`

``[`https://github.com/codingo/NoSQLMap`](https://github.com/codingo/NoSQLMap)``

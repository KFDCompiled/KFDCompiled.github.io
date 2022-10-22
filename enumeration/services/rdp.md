---
description: Remote Desktop Protocol Enumeration
---

# RDP

## stickykeys

[https://book.hacktricks.xyz/network-services-pentesting/pentesting-smtp](https://book.hacktricks.xyz/network-services-pentesting/pentesting-smtp)

## nmap (checks encryption & ntlm)

```
nmap --script "rdp-enum-encryption or rdp-vuln-ms12-020 or rdp-ntlm-info" -p 3389 -T4 $TARGET
```

## rdp\_check (test credentials)

```
rdp_check <domain>/<name>:<password>@$TARGET
```

## rdesktop (connect)

```
rdesktop -u <username> [-p <password>] [-d <domain>] $TARGET
```

## Once Connected:

### runas (another user)

```
runas /netonly /user:<DOMAIN>\<NAME> "cmd.exe" #The password will be prompted
```

### Session stealing

```
query user #check open sessions
tscon <ID> /dest:<SESSIONNAME> #access selected session
```

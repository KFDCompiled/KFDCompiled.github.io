# Devices

## Authenticated

```
ldapsearch -H ldap://<DCIP> -x -LLL -W -D "<user>@<domain>.<tld>" -b "dc=<domain>,dc=<tld>" "(objectclass=computer)" "DNSHostName" "OperatingSystem"
```

## Unauthenticated

```
nbtscan 192.168.X.0/24
ntlm-info smb 192.168.X.Y
crackmapexec smb $target
```

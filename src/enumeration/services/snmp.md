# SNMP

## snmpwalk

```
snmpwalk -c public -v1 $TARGET 1
snmpwalk -c private -v1 $TARGET 1
snmpwalk -c manager -v1 $TARGET 1
```

## nmap

nmap -Pn -sU -p 161 $TARGET --script=

```
/usr/share/nmap/scripts/snmp-brute.nse
/usr/share/nmap/scripts/snmp-hh3c-logins.nse
/usr/share/nmap/scripts/snmp-info.nse
/usr/share/nmap/scripts/snmp-interfaces.nse
/usr/share/nmap/scripts/snmp-ios-config.nse
/usr/share/nmap/scripts/snmp-netstat.nse
/usr/share/nmap/scripts/snmp-processes.nse
/usr/share/nmap/scripts/snmp-sysdescr.nse
/usr/share/nmap/scripts/snmp-win32-services.nse
/usr/share/nmap/scripts/snmp-win32-shares.nse
/usr/share/nmap/scripts/snmp-win32-software.nse
/usr/share/nmap/scripts/snmp-win32-users.nse
```

## snmp-check

```
snmp-check $TARGET -c public
```

## onesixtyone

```
onesixtyone -c /usr/share/doc/onesixtyone/dict.txt
```

## impacket

```
impacket-samdump SNMP $TARGET
```

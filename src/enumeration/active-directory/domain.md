# Domain

## Current User Domain from Powershell

```
$env:USERDNSDOMAIN
```

```
(Get-ADDomain).DNSRoot
```

## Current Device Domain from Powershell

```
(Get-WmiObject Win32_ComputerSystem).Domain
```

## Domain SID from Powershell

```powershell
Get-ADDomain | select DNSRoot,NetBIOSName,DomainSID
```

## nltest

```
nltest /domain_trusts
```

```
nltest /dclist:<domain>
```

```
nslookup <DC01.domain.tld>
```

---
description: Web Application Enumeration
---

# WebApp

## Credentials

### Bruteforce

```
hydra -L <username list> -P <password list> <Target IPv4/Domain> <method> "<auth area>:<parameters>:<fail message>[:H=COOKIES: security=low; <cookiename>=<cookievalue>]"
# <parameters> takes form of "username=^USER^&password=^PASS^&login=login"
```

### Bypass

#### SQLi

?id=1 union select \* from \<tablename>;

[SQLi](https://app.gitbook.com/o/0TOzzjcrYPbcpGxxpf2l/s/vkiHJ7wzKS1d2YnfoJ4m/\~/changes/kyfU1kkWEwd5E3hQ6qD2/enumeration/webapp/sqli)

{% content-ref url="sqli.md" %}
[sqli.md](sqli.md)
{% endcontent-ref %}

## URLs

### Bruteforce Directories

```
feroxbuster -A -w /usr/share/wordlists/dirb/common.txt -u http://$TARGET
```

## Page Content

### Displayed



### Source Code



## Response Headers

```
nikto -host http://$TARGET:80/ -Format txt -output $TARGET.nikto
```

## Sitemaps

```
curl -LO http://$TARGET/robots.txt && curl -LO http://$TARGET/sitemap.xml
```

## Administrative Consoles


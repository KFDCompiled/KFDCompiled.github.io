# Wordpress

## Wordpress

```
wpscan --update
wpscan --url http://${TARGET}:80/ --no-update -e vp,vt,tt,cb,dbe,u,m --plugins-detection aggressive --plugins-version-detection aggressive -f cli-no-color 2>&1 | tee "/home/kali/KCP/OSCP/results/${TARGET}/scans/tcp80/tcp_80_http_wpscan.txt"
```

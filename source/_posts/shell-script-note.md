title: shell筆記區
date: 2015-08-20 06:21:30
tags:
---
<!-- toc -->

# bash
## 搜尋.bash_history下過的command
`Ctrl + R`

## 查版本
`uname -a`
`lsb_release -a`

## 找DNS IP
```bash
$ scutil --dns
DNS configuration

resolver #1
  nameserver[0] : 192.168.43.1
  if_index : 5 (en1)
  flags    : Request A records
  reach    : Reachable,Directly Reachable Address
```

## 讀取java位置
```bash
[ec2-user@ip-172-31-22-146 opt]$ readlink -f $(which java)
/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.45-30.b13.el7_1.x86_64/jre/bin/java
/*redhat版本*/
[ec2-user@ip-172-31-22-146 ~]$ cat /etc/redhat-release
Red Hat Enterprise Linux Server release 7.1 (Maipo)
```
## 設定redirect 80 到 8080 (-A)
```bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
/* 移除設定 (-D)*?
iptables -t nat -D PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
```


# PowerShell
`Start-Process hexo s` or `start hexo s`

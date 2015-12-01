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


## 查詢檔案類型

```
# file /bin/grep
/bin/grep: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=0x2695c3bf69db3cd5a6ea3f71ce1d0658e53ba354, stripped
```

## 設定redirect 80 到 8080 (-A)

```bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
/* 移除設定 (-D)*?
iptables -t nat -D PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
```

## CentOS 7 open port 8080 on firewall

1.ensure `firewalld` is active.

```bash
# systemctl status firewalld.service
firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled)
   Active: active (running) since 三 2015-11-25 09:11:43 CST; 5h 4min ago
 Main PID: 654 (firewalld)
   CGroup: /system.slice/firewalld.service
           └─654 /usr/bin/python -Es /usr/sbin/firewalld --nofork --nopid

11月 25 09:11:42 f6s systemd[1]: Starting firewalld - dynamic firewall daemon...
11月 25 09:11:43 f6s systemd[1]: Started firewalld - dynamic firewall daemon...
```


2.pre-check firewall rule.

```bash
[root@f6s sysconfig]# firewall-cmd --zone=public --list-all
public (default, active)
  interfaces: ens32
  sources:
  services: dhcpv6-client ssh
  ports:
  masquerade: no
  forward-ports:
  icmp-blocks:
  rich rules:
```

3.add rule.

```bash
[root@f6s sysconfig]# firewall-cmd --zone=public --add-port=8080/tcp --permanent
success
```

4.rule not applied

```bash
[root@f6s sysconfig]# firewall-cmd --zone=public --list-all
public (default, active)
  interfaces: ens32
  sources:
  services: dhcpv6-client ssh
  ports:
  masquerade: no
  forward-ports:
  icmp-blocks:
  rich rules:
```

5.reload firewalld

```bash
[root@f6s sysconfig]# firewall-cmd --reload
success
```

6.rule applied

```bash
[root@f6s sysconfig]# firewall-cmd --zone=public --list-all
public (default, active)
  interfaces: ens32
  sources:
  services: dhcpv6-client ssh
  ports: 8080/tcp
  masquerade: no
  forward-ports:
  icmp-blocks:
  rich rules:
```

Remove it as needed:

```bash
[root@f6s sysconfig]# firewall-cmd --zone=public --remove-port=8080/tcp --permanent
success
[root@f6s sysconfig]# firewall-cmd --reload
success
[root@f6s sysconfig]# firewall-cmd --zone=public --list-all
public (default, active)
  interfaces: ens32
  sources:
  services: dhcpv6-client ssh
  ports:
  masquerade: no
  forward-ports:
  icmp-blocks:
  rich rules:
```

## reference

[CentOS 7 / RHEL 7 – Open ports](https://www.evernote.com/shard/s75/sh/6409d14a-1b0c-4cfc-bbe3-19b0470833b9/abc3172d799d27285096c6e7c7a61798)

# PowerShell
`Start-Process hexo s` or `start hexo s`
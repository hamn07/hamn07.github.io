title: 資料庫筆記區
date: 2015-08-20 05:55:47
tags:
---
<!-- toc -->
# MySQL

## MariaDB install on OSX
[官網教學](https://mariadb.com/kb/en/mariadb/building-mariadb-on-mac-os-x-using-homebrew/)

1. `brew install mariadb`
```bash
04:55 $ brew install mariadb
==> Installing mariadb dependency: openssl
==> Downloading https://homebrew.bintray.com/bottles/openssl-1.0.2d_1.yosemite.bottle.tar.gz
######################################################################## 100.0%
==> Pouring openssl-1.0.2d_1.yosemite.bottle.tar.gz
==> Caveats
A CA file has been bootstrapped using certificates from the system
keychain. To add additional certificates, place .pem files in
  /usr/local/etc/openssl/certs

and run
  /usr/local/opt/openssl/bin/c_rehash

This formula is keg-only, which means it was not symlinked into /usr/local.

Apple has deprecated use of OpenSSL in favor of its own TLS and crypto libraries

Generally there are no consequences of this for you. If you build your
own software and it requires this formula, you'll need to add to your
build variables:

    LDFLAGS:  -L/usr/local/opt/openssl/lib
    CPPFLAGS: -I/usr/local/opt/openssl/include

==> Summary
🍺  /usr/local/Cellar/openssl/1.0.2d_1: 464 files, 18M
==> Installing mariadb
==> Downloading https://homebrew.bintray.com/bottles/mariadb-10.0.21.yosemite.bottle.tar.gz
######################################################################## 100.0%
==> Pouring mariadb-10.0.21.yosemite.bottle.tar.gz
==> /usr/local/Cellar/mariadb/10.0.21/bin/mysql_install_db --verbose --user=HamnLee --basedir=/usr/lo
==> Caveats
A "/etc/my.cnf" from another install may interfere with a Homebrew-built
server starting up correctly.

To connect:
    mysql -uroot

To have launchd start mariadb at login:
  ln -sfv /usr/local/opt/mariadb/*.plist ~/Library/LaunchAgents
Then to load mariadb now:
  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mariadb.plist
Or, if you don't want/need launchctl, you can just run:
  mysql.server start
==> Summary
🍺  /usr/local/Cellar/mariadb/10.0.21: 530 files, 130M
```
2. `unset TMPDIR`
```bash
$ echo $TMPDIR
/var/folders/jw/6rpyrtd14g156cll7p2fx_vc0000gn/T/
$ unset TMPDIR
```
3. `mysql_install_db`
```bash
$ mysql_install_db
Installing MariaDB/MySQL system tables in '/usr/local/var/mysql' ...
150820  5:02:59 [Note] /usr/local/Cellar/mariadb/10.0.21/bin/mysqld (mysqld 10.0.21-MariaDB) starting as process 6132 ...
150820  5:02:59 [Note] InnoDB: Using mutexes to ref count buffer pool pages
150820  5:02:59 [Note] InnoDB: The InnoDB memory heap is disabled
150820  5:02:59 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
150820  5:02:59 [Note] InnoDB: Memory barrier is not used
150820  5:02:59 [Note] InnoDB: Compressed tables use zlib 1.2.5
150820  5:02:59 [Note] InnoDB: Using CPU crc32 instructions
150820  5:02:59 [Note] InnoDB: Initializing buffer pool, size = 128.0M
150820  5:02:59 [Note] InnoDB: Completed initialization of buffer pool
150820  5:02:59 [Note] InnoDB: Highest supported file format is Barracuda.
150820  5:02:59 [Note] InnoDB: 128 rollback segment(s) are active.
150820  5:02:59 [Note] InnoDB: Waiting for purge to start
150820  5:02:59 [Note] InnoDB:  Percona XtraDB (http://www.percona.com) 5.6.25-73.1 started; log sequence number 1616707
150820  5:03:06 [Note] InnoDB: FTS optimize thread exiting.
150820  5:03:06 [Note] InnoDB: Starting shutdown...
150820  5:03:08 [Note] InnoDB: Shutdown completed; log sequence number 1616717
OK
Filling help tables...
150820  5:03:09 [Note] /usr/local/Cellar/mariadb/10.0.21/bin/mysqld (mysqld 10.0.21-MariaDB) starting as process 6136 ...
150820  5:03:09 [Note] InnoDB: Using mutexes to ref count buffer pool pages
150820  5:03:09 [Note] InnoDB: The InnoDB memory heap is disabled
150820  5:03:09 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
150820  5:03:09 [Note] InnoDB: Memory barrier is not used
150820  5:03:09 [Note] InnoDB: Compressed tables use zlib 1.2.5
150820  5:03:09 [Note] InnoDB: Using CPU crc32 instructions
150820  5:03:09 [Note] InnoDB: Initializing buffer pool, size = 128.0M
150820  5:03:09 [Note] InnoDB: Completed initialization of buffer pool
150820  5:03:09 [Note] InnoDB: Highest supported file format is Barracuda.
150820  5:03:09 [Note] InnoDB: 128 rollback segment(s) are active.
150820  5:03:09 [Note] InnoDB: Waiting for purge to start
150820  5:03:09 [Note] InnoDB:  Percona XtraDB (http://www.percona.com) 5.6.25-73.1 started; log sequence number 1616717
150820  5:03:09 [Note] InnoDB: FTS optimize thread exiting.
150820  5:03:09 [Note] InnoDB: Starting shutdown...
150820  5:03:11 [Note] InnoDB: Shutdown completed; log sequence number 1616727
OK

To start mysqld at boot time you have to copy
support-files/mysql.server to the right place for your system

PLEASE REMEMBER TO SET A PASSWORD FOR THE MariaDB root USER !
To do so, start the server, then issue the following commands:

'/usr/local/Cellar/mariadb/10.0.21/bin/mysqladmin' -u root password 'new-password'
'/usr/local/Cellar/mariadb/10.0.21/bin/mysqladmin' -u root -h Leeteki-MacBook-Pro.local password 'new-password'

Alternatively you can run:
'/usr/local/Cellar/mariadb/10.0.21/bin/mysql_secure_installation'

which will also give you the option of removing the test
databases and anonymous user created by default.  This is
strongly recommended for production servers.

See the MariaDB Knowledgebase at http://mariadb.com/kb or the
MySQL manual for more instructions.

You can start the MariaDB daemon with:
cd '/usr/local/Cellar/mariadb/10.0.21' ; /usr/local/Cellar/mariadb/10.0.21/bin/mysqld_safe --datadir='/usr/local/var/mysql'

You can test the MariaDB daemon with mysql-test-run.pl
cd '/usr/local/Cellar/mariadb/10.0.21/mysql-test' ; perl mysql-test-run.pl

Please report any problems at http://mariadb.org/jira

The latest information about MariaDB is available at http://mariadb.org/.
You can find additional information about the MySQL part at:
http://dev.mysql.com
Support MariaDB development by buying support/new features from MariaDB
Corporation Ab. You can contact us about this at sales@mariadb.com.
Alternatively consider joining our community based development effort:
http://mariadb.com/kb/en/contributing-to-the-mariadb-project/
```
4. `mysql.server start`
```bash
$ mysql.server start
Starting MySQL
. SUCCESS!
```

5. `mysqladmin -u root password '密碼'`

6. `mysql -uroot -p`
```bash
$ mysql -uroot -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 4
Server version: 10.0.21-MariaDB Homebrew

Copyright (c) 2000, 2015, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| test               |
+--------------------+
4 rows in set (0.01 sec)
```


## 查此session是用那個帳號登入

> Actually, you need to use two functions
>
> `SELECT USER(),CURRENT_USER();`
> USER() reports how you attempted to authenticate in MySQL
>
> CURRENT_USER() reports how you were allowed to authenticate in MySQL
>
> Sometimes, they are different

## 啟動MySQL
OSX
`mysql.server {start|status|stop}`
Linux
`systemctl {start|status|stop} mariadb`

## Trouble Shooting
### add primary key時，出現key was too long的錯誤訊息

```sql
mysql> ALTER TABLE post
    ->   ADD PRIMARY KEY (timestamp,member_id);
ERROR 1071 (42000): Specified key was too long; max key length is 767 bytes
```
> id 長度設定為VARCHAR(256)，db編碼採用utf8，要佔掉256x3=768 bytes，再加上timestamp佔掉4個bytes，已超過限制，因此將id長度改成254

## Reference
[Server Error Codes and Messages](https://dev.mysql.com/doc/refman/5.7/en/error-messages-server.html)

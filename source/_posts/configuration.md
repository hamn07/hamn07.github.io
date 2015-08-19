title: 備忘 - Configuration of Server, IDE
date: 2015-07-22 07:45:21
tags:
---
<!-- toc -->



# OSX
## 設定apache
[Setting up a local web server on OS ](https://discussions.apple.com/docs/DOC-3083)
`sudo vi /etc/apache2/httpd.conf`
`sudo launchctl load -w /System/Library/LaunchDaemons/org.apache.httpd.plist`
`sudo /usr/sbin/apachectl restart`
## CyberDuck
![](CyberDuck.png)
## MenuMeter
![](MenuMeter.png)
## Keka
[官網](http://www.kekaosx.com/zh-tw/)
## ec2
$ chmod 400 ~/.ssh/dvp.pem
alias sshec2='ssh -i ~/.ssh/dvp.pem ec2-user@52.26.138.212'
## 嘸蝦米輸入法
直接安裝bin檔
## homebrew - The missing package manager for OS X
安裝套件都放在`/usr/local/Cellar`底下
## MariaDB
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

# Heroku
## deploy
1. Download `Heroku Toolbelt`
2. `$ heroku login`
3. `$ heroku git:clone -a stark-everglades-8527`
4. `$ git push heroku master`






# Git
## 設定`.gitignore_global`
> git config --global core.excludesfile ~/.gitignore_global

```bash
10:39 $ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.idea/
	lab-android-studio.iml
	pichannelur/pichannelur.iml
	pichannelvr/pichannelvr.iml

nothing added to commit but untracked files present (use "git add" to track)
✔ ~/Workspace/lab-android-studio [master|…11]
```
```bash
10:43 $ git config --global -l
fatal: unable to read config file '/Users/Hamn/.gitconfig': No such file or directory
✘-128 ~/Workspace/lab-android-studio [master|…11]
```
```bash
10:43 $ git config --global core.excludesfile ~/.gitignore_global
✔ ~/Workspace/lab-android-studio [master|✔]
```
```bash
10:44 $ git config --global -l
core.excludesfile=/Users/Hamn/.gitignore_global
✔ ~/Workspace/lab-android-studio [master|✔]
```
```bash
10:44 $ git status
On branch master
Your branch is up-to-date with 'origin/master'.

nothing to commit, working directory clean
✔ ~/Workspace/lab-android-studio [master|✔]
```

## 將現有專案push上gihub.com
1. 於github.com建立repository
2. 於專案目錄下:
  1. git init
  2. git add -A
  3. git commit -m "init"
  4. git remote add origin `{github.com上repository的HTTPS clone URL}`
  5. git push -u origin master
```
$ git push -u origin master
Counting objects: 421, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (387/387), done.
Writing objects: 100% (421/421), 31.74 MiB | 190.00 KiB/s, done.
Total 421 (delta 42), reused 0 (delta 0)
To git@github.com:hamn07/pichannel.web.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```
  6. git status
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

nothing to commit, working directory clean
```
3. github.com的repository有檔案，Done.


## git diff 比較兩個commit的差異
```bash
>
>
D:\dvp\workspace\hamn07.github.io [master]> git show --pretty=fuller
commit ad92f1e68a0c2b10f9d72307b7ab4299c475c1d3
Merge: 3c038a1 8865490
Author:     hamn07 <hamn07@gmail.com>
AuthorDate: Tue Jul 21 13:58:09 2015 +0800
Commit:     hamn07 <hamn07@gmail.com>
CommitDate: Tue Jul 21 13:58:09 2015 +0800

    Merge branch 'master' of github.com:hamn07/src.hamn07.github.io
>
>
D:\dvp\workspace\hamn07.github.io [master]> git diff 3c038a1 8865490
diff --git a/_config.yml b/_config.yml
index 626a0bb..a092632 100644
--- a/_config.yml
+++ b/_config.yml
@@ -63,6 +63,7 @@ pagination_dir: page
 # Extensions
 ## Plugins: http://hexo.io/plugins/
 ## Themes: http://hexo.io/themes/
+#theme: landscape
 #theme: phase
 theme: tranquilpeak
```




# Apache httpd
## win7建置

1. 目錄預設檔案
```
<IfModule dir_module>
    DirectoryIndex index.php
</IfModule>
```
2. apache安裝目錄
`Define SRVROOT "D:\dvp\dev-tool\httpd-2.4.16-x64-vc11\Apache24"`

3. 網頁根目錄
`DocumentRoot "D:\dvp\workspace\classroom2001\project"`
`<Directory "D:\dvp\workspace\classroom2001\project">`

4. 介紹apache認識php
```
LoadModule php5_module "D:\dvp\dev-tool\php-5.6.11-Win32-VC11-x64\php5apache2_4.dll"
AddType application/x-httpd-php .php
PHPIniDir "D:\dvp\dev-tool\php-5.6.11-Win32-VC11-x64"
```
5. 網頁重導設定
`LoadModule rewrite_module modules/mod_rewrite.so`
```
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
#RewriteRule api/v1/(.*)$ phpinfo.php?request=$1 [QSA,NC,L]
RewriteRule api/(.*)$ /api/controller.php?request=$1 [QSA,NC,L]
</IfModule>
```
6. 環境變數$PATH加入`D:\dvp\dev-tool\httpd-2.4.16-x64-vc11\Apache24\bin`

7. 防止diretory listing (Production)
```
#Options Indexes FollowSymLinks
Options FollowSymLinks
```
8. Cross-Origin Resource Sharing (Optional)，於DocumentRoot的Diretory裡設定
`LoadModule headers_module modules/mod_headers.so`
```
    <IfModule mod_headers.c>
      Header set Access-Control-Allow-Origin "*"
    </IfModule>
```

9. 註冊到service後，可使用Apache Monitor管理
`httpd.exe -k install [-n MyServiceName]`

>※使用service開啟httpd無法載入curl，原因是apache認不到curl在PHP目錄裡的依賴包libssh2.dll
>`PHP Fatal error:  Call to undefined function curl_init()`
>解法: 將libssh2.dll複製一份到apache/bin再重啟


# PHP
## win7建置
1. 顯示錯誤
`display_errors = On`

2. 設置extension目錄
`extension_dir = "D:\dvp\dev-tool\php-5.6.11-Win32-VC11-x64\ext"`

3. enable extenstions
`extension=php_bz2.dll`
`extension=php_curl.dll`
`extension=php_gd2.dll`
`extension=php_mbstring.dll`
`extension=php_exif.dll`
`extension=php_mysql.dll`
`extension=php_mysqli.dll`
`extension=php_pdo_mysql.dll`

4. 時區
`date.timezone = Asia/Taipei`

5. 環境變數$PATH加入`D:\dvp\dev-tool\php-5.6.11-Win32-VC11-x64`

6. 設置最大post size - Production
post_max_size = 1M

## Linux建置
上傳檔案時報錯`PHP Warning:  mkdir(): Permission denied`
Workaround: [參考](http://stackoverflow.com/questions/13908722/php-unable-to-create-a-directory-with-mkdir)
```
$ ls -lZ img-repo/
drwxrwxr-x. ec2-user ec2-user unconfined_u:object_r:httpd_sys_content_t:s0 img-repo
$ chcon -R -t httpd_sys_content_rw_t img-repo/
```
```
vi /etc/httpd/conf/httpd.conf

user ec2-user
group ec2-user
```


# hexo
`npm install hexo-toc --save`
`npm install hexo-deployer-git --save`

```bash
$ hexo d
INFO  Deploying: git
INFO  Clearing .deploy folder...
INFO  Copying files from public folder...
On branch master
nothing to commit, working directory clean
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
FATAL Something wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Error: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

    at ChildProcess.<anonymous> (/Users/Hamn/Workspace/src.hamn07.github.io/node_modules/hexo-deployer-git/node_modules/hexo-util/lib/spawn.js:42:17)
    at ChildProcess.emit (events.js:110:17)
    at maybeClose (child_process.js:1015:16)
    at Process.ChildProcess._handle.onexit (child_process.js:1087:5)
```
Workaround: [add SSH keys to GitHub.com](https://help.github.com/articles/generating-ssh-keys/)
## Reference
[lukang介紹Hexo系列文章](http://lukang.me/categories/Hexo/)

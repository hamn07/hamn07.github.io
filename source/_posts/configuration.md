title: 備忘 - Configuration of Server, IDE
date: 2015-07-22 07:45:21
tags:
---
<!-- toc -->

# Kaazing
```bash
✔ /usr/local/kaazing-gateway-community-5.0.0/bin [master L|✔]
06:01 $ ./gateway.start
INFO  Kaazing Gateway (5.0.0.15)
INFO  Configuration file: /usr/local/kaazing-gateway-community-5.0.0/conf/gateway-config-minimal.xml
INFO  Starting server
INFO  Starting services
INFO    http://localhost:8000/
INFO    http://localhost:8000/commandcenter
INFO    ws://localhost:8000/echo
INFO    ws://localhost:8000/snmp
INFO  Started services
INFO  Started server successfully in 2.391 secs at 2015-10-03 06:02:06

```


# OSX


## CentOS bootable USB

```bash
$ diskutil list
/dev/disk0
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.1 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:                  Apple_HFS Macintosh HD            419.0 GB   disk0s2
   3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
   4:       Microsoft Basic Data                         80.2 GB    disk0s4
/dev/disk1
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *8.1 GB     disk1
   1:                 DOS_FAT_32 NO NAME                 8.1 GB     disk1s1
$ diskutil unmountDisk /dev/disk1
Unmount of all volumes on disk1 was successful
$ sudo dd if=CentOS-7-x86_64-DVD-1503-01.iso of=/dev/disk1
8419328+0 records in
8419328+0 records out
4310695936 bytes transferred in 11507.233801 secs (374607 bytes/sec)
```
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
## XtraFinder - 補強Finder功能
## MPlayerX
## Sublime
[Sublime Text 3 新手上路：必要的安裝、設定與基本使用教學](https://www.evernote.com/shard/s75/sh/a1cd7790-c07f-41f6-9031-951c3988b457/5dd08a112d111e9e60c15bdc203466a9)

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

# Eclipse
- [CDT](http://www.eclipse.org/cdt/downloads.php)
- [Arduino plugin nightly-osx](http://www.baeyens.it/eclipse/nightly-osx.html)
- Log Viewer
- SQL Development Tool
- Eclipse Color Theme
- Eclipse Moonrise UI Theme
- Gradle IDE package 3.6.x

# Chrome
Insomnia
postman
better google tasks


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

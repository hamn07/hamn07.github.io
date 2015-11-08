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
`sudo launchctl load -w /System/Library/LaunchDaemons/org.apache.httpd.plist`
`sudo /usr/sbin/apachectl restart`
```bash
$ grep DocumentRoot /etc/apache2/httpd.conf
# DocumentRoot: The directory out of which you will serve your
DocumentRoot "/Library/WebServer/Documents"
```
```bash
$ pwd
$ grep ErrorLog /etc/apache2/httpd.conf
# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive w
-rw-r--r--  1 root  wheel  903123088 10 25 20:39 access_log
-rw-r--r--  1 root  wheel    3208194 10 25 20:38 error_log
```
## Software
- CyberDuck
![](CyberDuck.png)
- MenuMeter
![](MenuMeter.png)
- Keka
[官網](http://www.kekaosx.com/zh-tw/)
- ec2
$ chmod 400 ~/.ssh/dvp.pem
alias sshec2='ssh -i ~/.ssh/dvp.pem ec2-user@52.26.138.212'
- 嘸蝦米輸入法
直接安裝bin檔
- homebrew - The missing package manager for OS X
安裝套件都放在`/usr/local/Cellar`底下
- [Homebrew Cask](http://caskroom.io/) extends Homebrew and brings its elegance, simplicity, and speed to OS X applications and large binaries alike. It only takes 1 line in your shell to reach 2835 Casks maintained by 434 contributors.
- XtraFinder - 補強Finder功能
- [QLMarkdown](https://github.com/toland/qlmarkdown) is a simple QuickLook generator for Markdown files.
- MPlayerX
- Sublime
- PhotoScape X
[Sublime Text 3 新手上路：必要的安裝、設定與基本使用教學](https://www.evernote.com/shard/s75/sh/a1cd7790-c07f-41f6-9031-951c3988b457/5dd08a112d111e9e60c15bdc203466a9)

# Heroku
## deploy
1. Download `Heroku Toolbelt`
2. `$ heroku login`
3. `$ heroku git:clone -a stark-everglades-8527`
4. `$ git push heroku master`





# Git
[git help連結](https://help.github.com/)

A successful Git branching model
![A successful Git branching model](http://backlogtool.com/git-guide/tw/img/post/stepup/capture_stepup1_5_6.png)
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
> 若是要把remote端的repo覆蓋掉，使用`git push origin --mirror`

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
## git pull 後, 回復到前版次
```bash
$ git reflog
4afe7c0 HEAD@{0}: pull: Fast-forward
1bcd64b HEAD@{1}: pull: Fast-forward
65ce0d2 HEAD@{2}: clone: from https://github.com/iissnan/hexo-theme-next
$ git reset --hard 65ce0d2
HEAD is now at 65ce0d2 Merge pull request #418 from Acris/master
```
# Maven
```bash
$ cat ~/.bash_profile | grep maven
export PATH="/Users/tomin.henrylee/Applications/apache-maven-3.3.3/bin:$PATH"
```
```bash
$ mvn -v
Apache Maven 3.3.3 (7994120775791599e205a5524ec3e0dfe41d4a06; 2015-04-22T19:57:37+08:00)
Maven home: /Users/tomin.henrylee/Applications/apache-maven-3.3.3
Java version: 1.8.0_45, vendor: Oracle Corporation
Java home: /Library/Java/JavaVirtualMachines/jdk1.8.0_45.jdk/Contents/Home/jre
Default locale: zh_TW, platform encoding: UTF-8
OS name: "mac os x", version: "10.11", arch: "x86_64", family: "mac"
```
```bash
$ mvn archetype:generate -DgroupId=com.henry.webapp -DartifactId=maven-test -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] >>> maven-archetype-plugin:2.4:generate (default-cli) > generate-sources @ standalone-pom >>>
[INFO]
[INFO] <<< maven-archetype-plugin:2.4:generate (default-cli) < generate-sources @ standalone-pom <<<
[INFO]
[INFO] --- maven-archetype-plugin:2.4:generate (default-cli) @ standalone-pom ---
[INFO] Generating project in Batch mode
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Old (1.x) Archetype: maven-archetype-quickstart:1.0
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: basedir, Value: /Users/tomin.henrylee/Workspace/temp
[INFO] Parameter: package, Value: com.henry.webapp
[INFO] Parameter: groupId, Value: com.henry.webapp
[INFO] Parameter: artifactId, Value: maven-test
[INFO] Parameter: packageName, Value: com.henry.webapp
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] project created from Old (1.x) Archetype in dir: /Users/tomin.henrylee/Workspace/temp/maven-test
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 3.268 s
[INFO] Finished at: 2015-10-23T14:00:05+08:00
```
```bash
$ tree maven-test/
maven-test/
├── pom.xml
└── src
    ├── main
    │   └── java
    │       └── com
    │           └── henry
    │               └── webapp
    │                   └── App.java
    └── test
        └── java
            └── com
                └── henry
                    └── webapp
                        └── AppTest.java

11 directories, 3 files
```
```bash
$ cd maven-test/
$ cat pom.xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.henry.webapp</groupId>
  <artifactId>maven-test</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>maven-test</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
</project>
```
```bash
$ mvn package
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building maven-test 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ maven-test ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/tomin.henrylee/Workspace/temp/maven-test/src/main/resources
[INFO]
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ maven-test ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ maven-test ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/tomin.henrylee/Workspace/temp/maven-test/src/test/resources
[INFO]
[INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ maven-test ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ maven-test ---
[INFO] Surefire report directory: /Users/tomin.henrylee/Workspace/temp/maven-test/target/surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running com.henry.webapp.AppTest
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.004 sec

Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO]
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ maven-test ---
[INFO] Building jar: /Users/tomin.henrylee/Workspace/temp/maven-test/target/maven-test-1.0-SNAPSHOT.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.147 s
[INFO] Finished at: 2015-10-23T14:20:40+08:00
[INFO] Final Memory: 11M/220M
[INFO] ------------------------------------------------------------------------
```
```bash
$ tree .
.
├── pom.xml
├── src
│   ├── main
│   │   └── java
│   │       └── com
│   │           └── henry
│   │               └── webapp
│   │                   └── App.java
│   └── test
│       └── java
│           └── com
│               └── henry
│                   └── webapp
│                       └── AppTest.java
└── target
    ├── classes
    │   └── com
    │       └── henry
    │           └── webapp
    │               └── App.class
    ├── maven-archiver
    │   └── pom.properties
    ├── maven-status
    │   └── maven-compiler-plugin
    │       ├── compile
    │       │   └── default-compile
    │       │       ├── createdFiles.lst
    │       │       └── inputFiles.lst
    │       └── testCompile
    │           └── default-testCompile
    │               ├── createdFiles.lst
    │               └── inputFiles.lst
    ├── maven-test-1.0-SNAPSHOT.jar
    ├── surefire-reports
    │   ├── TEST-com.henry.webapp.AppTest.xml
    │   └── com.henry.webapp.AppTest.txt
    └── test-classes
        └── com
            └── henry
                └── webapp
                    └── AppTest.class

28 directories, 13 files
```
[Maven by Example](http://books.sonatype.com/mvnex-book/reference/index.html)
[How to enable index downloads in Eclipse for Maven search?](https://www.evernote.com/shard/s75/sh/20369e9b-278a-4782-b42c-9f4e820aced6/2fd59b98812bfd5a45e9bd6763ba63b8)
[Maven – Maven in 5 Minutes](https://www.evernote.com/shard/s75/sh/af016fc0-1205-4c35-b663-6ba2b7ecf41e/073450b9e72f07636e8e7329885e102c)
[How do I prevent "[WARNING] Using platform encoding (Cp1252 actually) to copy filtered resources, i.e. build is platform dependent!"](https://www.evernote.com/shard/s75/sh/309517cb-d15f-4f31-b3e2-79d2c0b41101/a47793422368965fa44fe1a7cfabb823)
# Atom
- Seti
-


# Eclipse
- [CDT](http://www.eclipse.org/cdt/downloads.php)
- [Arduino plugin nightly-osx](http://www.baeyens.it/eclipse/nightly-osx.html)
- Log Viewer
- SQL Development Tool
- Eclipse Color Theme
- Eclipse Moonrise UI Theme
![](eclipse-color-theme-1.png)
![](eclipse-color-theme-2.png)
- Gradle IDE package 3.6.x



# Chrome
Insomnia
postman
better google tasks


# hexo

## 報錯[Error: Module version mismatch. Expected 14, got 46.]

```bash
✔ ~/Workspace/src.hamn07.github.io [master|✔]
13:08 $ hexo --version
[Error: Module version mismatch. Expected 14, got 46.]
{ [Error: Cannot find module './build/default/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/Debug/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
hexo: 3.1.1
os: Darwin 15.0.0 darwin x64
http_parser: 2.3
node: 0.12.7
v8: 3.28.71.19
uv: 1.6.1
zlib: 1.2.8
modules: 14
openssl: 1.0.1p
```

**Workaround**
```bash
13:08 $ npm install hexo --no-optional
hexo@3.1.1 node_modules/hexo
├── hexo-front-matter@0.2.2
├── pretty-hrtime@1.0.1
├── abbrev@1.0.7
├── archy@1.0.0
├── titlecase@1.0.2
├── text-table@0.2.0
├── tildify@1.1.2 (os-homedir@1.0.1)
├── strip-indent@1.0.1 (get-stdin@4.0.1)
├── hexo-i18n@0.2.1 (sprintf-js@1.0.3)
├── chalk@1.1.1 (escape-string-regexp@1.0.3, supports-color@2.0.0, ansi-styles@2.1.0, has-ansi@2.0.0, strip-ansi@3.0.0)
├── minimatch@2.0.10 (brace-expansion@1.1.1)
├── bunyan@1.5.1
├── through2@1.1.1 (xtend@4.0.0, readable-stream@1.1.13)
├── swig-extras@0.0.1 (markdown@0.5.0)
├── bluebird@2.10.2
├── js-yaml@3.4.3 (esprima@2.6.0, argparse@1.0.2)
├── cheerio@0.19.0 (entities@1.1.1, dom-serializer@0.1.0, css-select@1.0.0, htmlparser2@3.8.3)
├── warehouse@1.0.3 (graceful-fs@4.1.2, cuid@1.2.5, JSONStream@1.0.6)
├── nunjucks@1.3.4 (optimist@0.6.1, chokidar@0.12.6)
├── hexo-cli@0.1.8 (minimist@1.2.0)
├── hexo-fs@0.1.4 (escape-string-regexp@1.0.3, graceful-fs@4.1.2, chokidar@1.2.0)
├── hexo-util@0.1.7 (ent@2.2.0, highlight.js@8.8.0)
├── moment-timezone@0.3.1
├── lodash@3.10.1
├── moment@2.10.6
└── swig@1.4.2 (optimist@0.6.1, uglify-js@2.4.24)

13:09 $ hexo server &
[1] 3911
✔ ~/Workspace/src.hamn07.github.io [master|✔]
13:09 $ INFO  Hexo is running at http://0.0.0.0:4000/. Press Ctrl+C to stop.

13:14 $ ps
  PID TTY           TIME CMD
  596 ttys000    0:01.23 -bash
 3911 ttys000    0:24.76 hexo

13:14 $ kill 3911
[1]+  Terminated: 15          hexo server
```

## npm install卡在node-gyp rebuild
Workaround:
1.安裝nvm
`wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.28.0/install.sh | bash`

2.更新npm

```bash
08:58 $ nvm list
->       system
node -> stable (-> N/A) (default)
iojs -> N/A (default)
✔ ~
08:58 $ nvm install stable
######################################################################## 100.0%
WARNING: checksums are currently disabled for node.js v4.0 and later
Now using node v4.1.2 (npm v2.14.4)
✔ ~
09:00 $ nvm ls
->       v4.1.2
         system
node -> stable (-> v4.1.2) (default)
stable -> 4.1 (-> v4.1.2) (default)
iojs -> N/A (default)
```

## deploy前置設定
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

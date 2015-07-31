title: 備忘 - Configuration of Server, IDE
date: 2015-07-22 07:45:21
tags:
---
<!-- toc -->
# Git
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
## Reference
[lukang介紹Hexo系列文章](http://lukang.me/categories/Hexo/)

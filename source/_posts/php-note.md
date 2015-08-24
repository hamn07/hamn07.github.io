title: Web筆記區
date: 2015-08-07 06:44:51
tags:
---
<!-- toc -->
[How to process PUT requests with PHP](http://phpave.com/how-to-process-put-requests-with-php/)

# Trouble Shooting
## PDO連線報錯no such file
[Setting up PHP & MySQL on OS X Yosemite](https://dzone.com/articles/setting-php-mysql-os-x)
![](pdo-error-msg.png)
![](pdo-error-phpinfo.png)
![](pdo-error-phpini.png)
![](pdo-error-mysql-sock.png)

## OSX上傳檔案時報錯`PHP Warning:  mkdir(): Permission denied`
```bash
[Fri Aug 21 06:46:19.036740 2015] [:error] [pid 4098] [client ::1:52036] PHP Warning:  mkdir(): Permission denied in /Users/Hamn/Workspace/pichannel.web/api/MyAPI.class.php on line 77
[Fri Aug 21 06:46:19.037019 2015] [:error] [pid 4098] [client ::1:52036] PHP Warning:  file_put_contents(/Users/Hamn/Workspace/pichannel.web/img-repo/fd/94400820857e1f415555cda791b279af6d72e8.jpg): failed to open stream: No such file or dir
```
Workaround:
```bash
$ mkdir img-repo
$ sudo chown img-repo _www
```
## Redhat上傳檔案時報錯`PHP Warning:  mkdir(): Permission denied`
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

## 上傳檔案時無法取得原始拍攝日期
```bash
[Sat Aug 22 18:12:45.538546 2015] [:error] [pid 833] [client ::1:49587] PHP Notice:  Undefined index: DateTimeOriginal in /Users/Hamn/Workspace/pichannel.web/api/MyAPI.class.php on line 89
```

# Apache httpd建置
## win7

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

## OSX
[Setting up a local web server on OS X](https://discussions.apple.com/docs/DOC-3083)

# PHP
## win7
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

## OSX (extra)
### 開啟xdebug
`zend_extension = "xdebug.so"`
### Composer
`curl -sS https://getcomposer.org/installer | php`
`mv composer.phar /usr/local/bin/composer`

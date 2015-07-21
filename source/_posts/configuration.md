title: 備忘 - Configuration of Server, IDE
date: 2015-07-22 07:45:21
tags:
---
<!-- toc -->

# Apache httpd
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

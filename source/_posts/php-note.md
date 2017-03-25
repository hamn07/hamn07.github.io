title: Web筆記區
date: 2015-08-07 06:44:51
tags:
---
<!-- toc -->

# html
``` html
<!-- 瀏覽器會根據伺服器送過來的 header 或是用其他方法來判定 HTML文件的編碼-->
<!-- 但是判定不一定會是正確，所以我們會在 <head> 告訴瀏覽器，這一份HTML文件的編碼是什麼 -->
<meta charset="UTF-8">
<!-- 為了手機瀏覽器設定的一個標籤 viewport (p17-12)-->
<meta name="viewport" content="width=device-width, user-scalable=no">

```

HTML data-* Attributes-->自定義tag屬性
[w3c](http://www.w3schools.com/tags/att_global_data.asp)
``` html
<ul>
  <li data-animal-type="bird">Owl</li>
  <li data-animal-type="fish">Salmon</li>
  <li data-animal-type="spider">Tarantula</li>
</ul>
```
# css

文字段落太長超過div後會有  ...  的效果

``` css
div {
        border-width: 5px;
        border-color: #000000;
        border-style: solid;
        width: 400px;
        height: 100px;

        /*這三組屬性必須同時存在*/
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
    }
```

# jQuery

[w3c參考網頁](http://www.w3schools.com/jquerymobile/)

[官網demo](http://demos.jquerymobile.com/1.4.5/grids/)

[Data Arributes](http://api.jquerymobile.com/data-attribute/)

[Classes](http://api.jquerymobile.com/classes/)

[jQuery Selectors](http://www.w3schools.com/jquery/jquery_selectors.asp)

[圖片slide的demo](http://www.anowave.com/factory/anoslide/demo.html)

[PhotoSwipe](http://photoswipe.com/)

[Glide](http://glide.jedrzejchalubek.com/)

[HTML5 Drag and Drop Upload and File API Tutorial](http://www.thebuzzmedia.com/html5-drag-and-drop-and-file-api-tutorial/)





# Security

## HTTPS - HTTP over SSL
工作原理:
1. 使用非對稱式加密演算法來對通訊雙方做身分認證
2. 並交換對稱金鑰為Session Key
3. 使用Session Key來加密C/S間的通訊內容

缺點:
1. 通訊內容加量，因此傳輸時間變長
2. 加解密需消耗額外機器資源 (可由SSL acceleration加速之)

IETF - Internet Engineering Task Force
SSL - Secure Socket Layer
TLS - Transport Layer Secure


SSL acceleration




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


## 定界符對應之結束符的前一個位元需為換行符號

以下會報錯`Parse error: syntax error, unexpected $end in xxx.php on line 64 `
```php
function insertImage($sha1,$timestamp){

  $sql = <<<sqlText
    INSERT INTO image VALUES (?,?)
  sqlText;
```

以下正解
```php
function insertImage($sha1,$timestamp){

  $sql = <<<sqlText
    INSERT INTO image VALUES (?,?)
sqlText;
```



## 使用exif_read_date需於php.ini做以下設定
以下報錯`Fatal error: Call to undefined function exif_read_data() xxx.php on line 2 `
```php
extension=php_exif.dll
extension=php_mbstring.dll
```
以下正解
```php
extension=php_mbstring.dll
extension=php_exif.dll
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

## 網站目錄權限設定

[官網說明文件 » File and Directory Ownership and Permissions for Web Content](https://wiki.apache.org/httpd/FileSystemPermissions)

# PHP

## curl使用POST打JSON搭Basic Authentication

##### /pichannel.web/test/curl-json.php


```php

$url = 'http://10.0.1.149:8080/SimpleTalk/test/henry/notify-sync';
$ch = curl_init( $url );
# Setup request to send json via POST.
$payload = json_encode( array( "member_id"=> "Samma" , "sync_type" => "A" , "timestampe" => "123456789") );
curl_setopt( $ch, CURLOPT_POSTFIELDS, $payload );
# Setup content-type as JSON
curl_setopt( $ch, CURLOPT_HTTPHEADER, array('Content-Type:application/json'));
# Return response instead of printing.
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
# Basic Authentication
$username = "api";
$password = "api";
curl_setopt( $ch, CURLOPT_USERPWD, $username . ":" . $password );
# Send request.
$response = curl_exec( $ch );
# Close Resource
curl_close( $ch );
# Parse to Array
$result = json_decode( $response, true );
# Print response.
echo var_dump($result);

```

[How to POST JSON Data With PHP cURL?](http://stackoverflow.com/questions/11079135/how-to-post-json-data-with-php-curl)


[How to process PUT requests with PHP](http://phpave.com/how-to-process-put-requests-with-php/)


## 資策會課程

[教材](http://sdrv.ms/178960Y)

MAMP: Mac Apache MySQL PHP

錢達智老師 [wolfgang.chien@gmail.com](mailto:wolfgang.chien@gmail.com)

RWD可參考 HTML5App_0309

``` php
//定界符號
$sSQL=<<<sqlText
SELECT id,name
  FROM employee
sqlText
```

```php
//string
$str1 = $str1." ".Str2
//string裡可放變數
echo "result=$sSum";
```

- include, require: 3-40
- include_once, **require_once**: 3-43
- define: 常數, 3-11

```php
//當檔案讀取到最後一行後會傳回false
while ($line = readline()){

}
```

```php
//global使用全域變數
$a = 20;
function myFunc($b){
	$a = 10;
	echo $a;
	global $a;
	echo $a;
}
```

```php
// 陣列
$weekArr [] = "Monday";
$weekArr [] = "Tuesday";
echo $weekArr [0];

$myArr ['myName'] = 'Henry';
$myArr ['myHeight'] = 183;
echo $myArr ['myName'];
echo "Hello!{$myArr['myName']}"

$weekArr = array('Mondy','Thuesday');

$myArr = array('myName'=>'Henry','myHeight'=>183);

foreach ($weekArr as $value){
	echo $value;
}
foreach ($weekArr as $key => $value){
	echo $key . ":" . $value . "<br>";
}
```

```php
//排序func
$myArr = array (
		'img1',
		'img3',
		'img5',
		'img2',
		'img11'
);
sort($myArr);
var_dump ( $myArr );
natsort($myArr);
var_dump ( $myArr );

// usort => 使用者自訂
usort($myArr, "cmp");

function cmp($a, $b){
	if ($a == $b){
		return 0
	};
	return ($a < $b) ? -1 : 1;
}
```

```php
// Session操作
start_session();
if (isset($_POST["btnWriteSession"])){
	$_SESSION["userName"]=$_POST["txt1"];
}
if (isset($_POST["btnWriteCookie"])){
	setcookie("userid", $_POST["txt2"]);
	setcookie("userid", $_POST["txt2"], time() + 60*60*24*7);
}
```

```php
//另一種if else寫法，可用來區分js的if else，提高可讀性
<?php if ($sUserName=="") : ?>
	<td align="center" valign="Wbaseline"><a href="login.php">登入</a> | <a href="secret.php">會員專用頁</a></td>
<?php else : ?>
	<td align="center" valign="Wbaseline"><a href="login.php?signout=1">登出</a> | <a href="secret.php">會員專用頁</a></td>
<?php endif ?>
```

```js
$('#letter').change(function(){
    //jQuery的$.get(url,func)即為AJAX機制存取資料
	$.get('getLetterNumber.php?letter='+$('#letter option:selected').text(),
			function(htmlData){
				$('#letterNumber').html(htmlData);
			});
});
```

Async的範例可參考0702的Lab_AsyncPost

```php
sprintf("<option value='%s'>%s%s</option>",$i, $x, $i+1);
```

##存取DB

```php
//連db(加上@是發生錯誤不show錯誤資訊)
$db_link = @mysql_connect($db_host, $db_username, $db_password);
//指定要操作那一個db
$seldb = @mysql_select_db("class");
//撈資訊
$sql_query = "SELECT * FROM `students`";
$result = mysql_query($sql_query);
//滾資料
//mysql_fetch_assoc => $item為欄位名 (associative array)
//mysql_fetch_row   => $item為array序號 (enumerated array)
//mysql_fetch_array => $both，所以會有兩筆
while($row_result=mysql_fetch_assoc($result)){
	foreach($row_result as $item=>$value){
		echo $item."=".$value."<br />";
	}
	echo "<hr />";
}
//取得資料筆數
$total_records = mysql_num_rows($result);
```
以下程式碼為建立連線存取資料的標準寫法
/LabPhp/php/0626/Lab_MySQL_basic_1_start.php
```php
<?php
header("content-type:text/html; charset=utf-8");

// 0. 請先建立 Class 資料庫 （執行 class.sql）

// 1. 連接資料庫伺服器
$link = mysql_connect("localhost", "root", "root") or die(mysql_error());
$result = mysql_query("set names utf8", $link);
mysql_selectdb("class", $link);

// 2. 執行 SQL 敘述
$commandText = "select * from students";
$result = mysql_query($commandText, $link);

// 3. 處理查詢結果
while ($row = mysql_fetch_assoc($result))
{
  echo "ID：{$row['cID']}<br>";
  echo "Name：{$row['cName']}<br>";
  echo "<HR>";
}
mysql_free_result($result);


// 4. 結束連線
mysql_close($link);

echo "<br />-- Done --";
?>
```
> PDO (PHP Data Object): 參考0702 Demo_PDO_xxxxx



6.29上午
file i/o
網站路徑(實體,虛擬)
檔名/目錄名/路徑的操作
檔案操作: 開/讀/關
目錄操作: 開/讀/關
form檔案上傳
```php
//目錄操作: 開/讀/關
	$fileDir = dirname(realpath("."));
	$fileResource = opendir($fileDir);
	echo "<table border='1' width='100%'><tr><td width='20%' valign='top'>資料夾：</td><td>";
	while($fileList = readdir($fileResource)){
		if(is_dir($fileDir.'/'.$fileList))	echo $fileList."<br />";
	}
	rewinddir($fileResource);
	echo "</td></tr><tr><td width='20%' valign='top'>檔案：</td><td>";
	while($fileList = readdir($fileResource)){
		if(is_file($fileDir.'/'.$fileList))echo $fileList."<br />";
	}
	echo "</td></tr></table>";
	closedir($fileResource);
//檔案操作: 開/讀/關
$filename = fopen("php_file13.htm","r");
while($line = fgets($filename)){
  echo $line;
}
fclose($filename);
```
```php
<?php
header("Content-Type: image/gif");
// fopne圖片/影片時，需使用rb
$filename = fopen("php_file18.gif","rb");
// fread讀取給定size的block進來(這裡的範例為整個圖片讀進來)
echo fread($filename,filesize("php_file18.gif"));
fclose($filename);
?>
```

[PHP 5 Filesystem Functions Reference](http://www.w3schools.com/php/php_ref_filesystem.asp)
```php
//檔案操作: 直接讀
$contents = file_get_contents('php_file11.htm');
echo strip_tags($contents);
//擋案操作: 直接讀成array
$lines = file('php_file11.htm');
foreach ($lines as $line_num => $line) {
    echo "#<b>$line_num</b> : " . htmlspecialchars($line) . "<br />\n";
}
//檔案操作: 直接寫
$content = <<<useHTML
	<html>
	<head>
		<META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8">
		<title>關於文淵閣工作室</title>
	</head>
	<body>
	<p>文淵閣工作室創立於1987年，第一本電腦叢書「快快樂樂學電腦」於該年底問世。工作室的創會成員－鄧文淵、李淑玲均為苦學出身，在學習電腦的過程中，一路顛簸走來，嚐遍人間冷暖。</p>
	<p>因此，決定整合自身的編輯、教學經驗及新生代的高手群，陸續推出 「快快樂樂全系列」 電腦叢書，冀望以輕鬆、深入淺出的筆觸、詳細的圖說，解決電腦學習者的徬徨無助，並搭配相關網站服務讀者。</p>
	<p>感謝您對文淵閣工作室的熱愛，也請您和我們在快快樂樂的氣氛中共同成長，突破極限、超越顛峰。謝謝大家！</p>
	</body>
	</html>
useHTML;
$filesize = file_put_contents("php_file13a.htm", $content);
echo "檔案寫入完成，大小為 $filesize bytes";
```
##檔案上傳
```html
<html>
<head>
	<META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8">
	<title>上傳檔案表單</title>
</head>
<body>
	<form action="php_file9.php" method="post" enctype="multipart/form-data">
	請選取要上傳的檔案：<br />
	<input type="file" name="fileUpload" /><br />
	<input type="submit" value="送出資料" />
	</form>
</body>
</html>
```


```php
<?php
	if($_FILES["fileUpload"]["error"]==0){
		if(move_uploaded_file($_FILES["fileUpload"]["tmp_name"], "./".$_FILES["fileUpload"]["name"])){
			echo "上傳成功<br />";
			echo "檔案名稱：".$_FILES["fileUpload"]["name"]."<br />";
			echo "檔案類型：".$_FILES["fileUpload"]["type"]."<br />";
			echo "檔案大小：".$_FILES["fileUpload"]["size"]."<br />";
		}else{
			echo "上傳失敗! ";
			echo "<a href='javascript:window.history.back();'>回上一頁</a>";
		}
	}
?>
```
6.29下午
物件導向
類別: 定義資料&方法(封裝)
物件: 實體化類別定義
繼承(extends). 多型.
建構子(construct) / 解構子(destruct)


##物件導向

OOPLib.php

```php
<?php
class media {
	private  $name;
	protected  $size;
	public $desc;

	function __construct($fname){
		$this->name = $fname;
		//echo '<h2>new image constrct<br>';
	}

	function echoDesc(){
		echo "<h1>$this->name description: $this->desc<br>";
	}

	function __destruct(){
		echo "<h2>this image($this->name) has been desctrct";
	}
}

class image extends media {
	function __construct($fname){
		parent::__construct($fname . "(image)");
	}
}
```

OOP.php

```php
<?php

include_once 'OOPLib.php';

session_start();
if (!isset($_SESSION['image'])) {
	$img = new image('lily-image.jpg');
	$_SESSION['image']=$img;
}

header("Location: OOP2.php");

?>
```



OOP2.php

```php
<?php
require_once 'OOPLib.php';
session_start();
$img = $_SESSION['image'];

$img->desc = 'boracay';
$img->echoDesc();

echo '<h3>';
var_dump($img);

$img = NULL;

echo '<h3>';
var_dump($img);
```
##JSON

0630

```php
$sJson = '{"cID":"01","cName":"\u7c21\u5949\u541b","cSex":"F","cBirthday":"1987-04-04","cEmail":"elven@superstar.com","cPhone":"0922988876","cAddr":"\u53f0\u5317\u5e02\u6fdf\u6d32\u5317\u8def12\u865f"}';

$obj = json_decode($sJson, false);//$assoc代上false表示轉成物件
echo "<h1> $obj->cName";
$arr = json_decode($sJson, true);//$assoc代上true表示轉成陣列
echo "<h2> {$arr['cName']}";

$arrData = Array(1, 2, Array('A', 'B', 'C'), 4, 5);
$arr = json_encode($arrData);
echo "<h3> $arr";
$obj = json_encode($arrData, JSON_FORCE_OBJECT);
//JSON_FORCE_OBJECT (integer) Outputs an object rather than an array when a non-associative array is used. Especially useful when the recipient of the output is expecting an object and the array is empty. Available since PHP 5.3.0.
echo "<h4> $obj";
```
[...] 中括號代表陣列
{...} 大括號代表物件
, 逗號分隔屬性
\: 分號設定屬性值
" 雙引號括住屬性值

```js
a=[1,2,3];
sJson = JSON.stringify(a);
b=JSON.parse(sJson);//嚴謹，JSON字串需符合格式
b=eval(sJson);//較鬆散，JSON字串可有點小錯

```
>同源政策 (Same-origin policy): 同源政策限制了程式碼和不同網域資源間的互動。
>JSONP: JSON Padding, 技術性處理同源政策的issue

scenario: 於localhost跨域要求www.monster.com的資料
solution: 透過指定script的src來跨域取得資料

http://**localhost**/Lab_JSONP/GetDataFromServer_34.php


```js
$("#btnRefresh").click(btnRefresh_click);

function btnRefresh_click() {
	var script = document.createElement('script');
    script.src = 'http://www.monster.com/Lab_JSONP/GetProductJsonp.php?id=1&callback=DataArrived';
    script.type = 'text/javascript';
    document.getElementsByTagName('head')[0].appendChild(script);
}

function DataArrived(data) {
	$("#txtUnitsInStock").val(data.UnitsInStock);
}
```


jQuery的寫法

```js
$("#btnRefresh").click(btnRefresh_click);

function btnRefresh_click() {
	$.ajax({
		url: "http://www.monster.com/Lab_JSONP/GetProductJsonp.php",
		type: "get",
		dataType: 'jsonp',
		data: {id: 1},
		jsonp: 'callback',
		jsonpCallback: 'DataArrived',
    });
}

function DataArrived(data) {
	$("#txtUnitsInStock").val(data.UnitsInStock);
}
```
##XML
0701上午

> **使用xpath來存取資料**
```php
$doc = new DOMDocument();
$doc->Load('employees.xml');
$xpath = new DOMXPath($doc);
//取得屬性值
$entries = $xpath->query("/employees/employee/@EmpType");
//對屬性值設定條件來filter資料
$entries = $xpath->query("/employees/employee[@EmpType='Sales']/lastName");
foreach ($entries as $entry)
{
   echo "結果：" . $entry->nodeValue . "<br>";
}
```
> chunked transfer encoding : Lab_LongRequest
> websocket
> single page application

##安全
0701下午
> 參考WebProgramSecurity.pdf，有server-side及client-side，極重要
> - SQL Injection
> - Server Configuration
> - XSS / CSRF
> -- captcha: 可參考0702 Lab_CAPTCHA
> -- anti CSRF token
> - ClickJacking
> -- frame bustering
> -- header("X-Frame-Options: Deny");

##laravel
Application key [TlDlIaffLhhfrgA5doqNw6iecg9KjNoU] set successfully.


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


# Reference
[PDO Tutorial for MySQL Developers](http://wiki.hashphp.org/PDO_Tutorial_for_MySQL_Developers)
[REST API Turorial](http://www.restapitutorial.com/index.html)
[Scope Resolution Operator (::)](http://php.net/manual/en/language.oop5.paamayim-nekudotayim.php)

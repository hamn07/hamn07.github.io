title: Android小專題 - 網路相簿
date: 2015-07-12 07:08:20
tags:
---
<!-- toc -->

# 專題概述

提供類似[picasa](https://picasaweb.google.com), [flikr](https://www.flickr.com/)等雲端相簿CRUD功能，讓使用者可以使用Android手機將相片存放於雲端來管理。再參考[Animoto](https://animoto.com/), [Stupeflix](https://studio.stupeflix.com), [Magisto](http://www.magisto.com/)等online video editor，讓使用者能輕鬆地以slideshow聲光效果的模式來觀賞相簿。

# 專題功能
- 手機相片上傳
- 雲端相簿管理
- Google帳號登入
- 雲端相簿於手機以slideshow聲光效果的模式播放


# 案例圖use case
![案例圖](use-case.svg)

# ER Diagram
![ER Diagram](er-diagram.svg)

# 雲端服務架構todo
| ![](image-owner.png)     | ![cloud](cloud_80x58.png)     |![](audience.png)
| :------------- | :------------- | :------------- |
| <u>***Android App***</u> | <u>[***LAMP Server***](http://52.26.138.212/)</u>| <u>***Android App***</u>|
| ✓ [prototype](https://popapp.in/w/projects/55a3af3ba8a45529517254bf/preview)  | ✓ create DB schema      | ✓ [prototype](https://popapp.in/w/projects/55a42a94e6f76c5a5a709b1a/preview)     |
| ✖ login activity | ✓ [Entity-Relation diagram](er-diagram.svg) | ✓ play slideshow  |
| ✖ main page activity | ✓ server installation | ✖ subscribe slideshow |
| ✖ describe image | ✓ server configuration    | □ show description    |
| ✖ [photo explore activity](https://github.com/iPaulPro/aFileChooser)     | ✖ slideshow pre-generate             | ✖ music selection |
| ✖ upload image   | ✓ [Creating a RESTful API with PHP](http://coreymaynard.com/blog/creating-a-restful-api-with-php/)| ✖ theme selection |
| ✖ music select activity | ✖ thumnail to speed up layout | □ compression before upload |
| ✖ preview slideshow | □ | □ |
| □ [How can i convert ByteArrayInputStream to jpeg and display on android mobile?](http://stackoverflow.com/questions/12908318/how-can-i-convert-bytearrayinputstream-to-jpeg-and-display-on-android-mobile) | □ | □ |
| □ | □ | □ |
| <u>***Web Browser***</u> | □ | □ |
| ✓ [prototype](http://52.26.138.212/)|□|□|
| ✓ image CURD        |□|□|
| ✖ [Resize image before upload on client-side](https://hacks.mozilla.org/2011/01/how-to-develop-a-html5-image-uploader/) | □ | □ |
| ✖ [auto rotate portrait image](https://github.com/blueimp/JavaScript-Load-Image) | □ | □ |
| □ | □ | □ |
※ **→ : 進行中的項目**
※ **□ : 7月底前完成項目**
※ **✖ : 待規劃時程實作**
※ **✓ : 已完成項目**

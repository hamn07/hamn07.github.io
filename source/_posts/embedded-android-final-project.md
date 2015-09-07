title: 期末專題
date: 2015-08-12 07:45:04
tags:
---
<!-- toc -->
[How to use Code for OV7670 in arduino uno](http://arduino.stackexchange.com/questions/10170/how-to-use-code-for-ov7670-in-arduino-uno)
[Lab5 Arduino 應用教學-安全警衛](http://here-apps.blogspot.tw/2014/07/lab5-arduino.html)
[[Arduino WIFI相机，自动拍照Intel Edison 和云端储存](http://www.dfrobot.com.cn/community/forum.php?mod=viewthread&tid=12432)
[Grove - Serial Camera Kit 串口照相機套件](https://www.mcuapps.com/goods/groves/grove-serial-camera-kit)
[Wireless Camera with Arduino and the CC3000 WiFi chip](https://www.openhomeautomation.net/wireless-camera/)
[OV7670 image sensor data capture with Atxmega32E5 without using external FIFO](https://github.com/kehribar/xmega_ov7670)
[eBook](http://www.psycho-sphere.com/)
[Hacking the OV7670 camera module (SCCB cheat sheet inside)](http://embeddedprogrammer.blogspot.tw/2012/07/hacking-ov7670-camera-module-sccb-cheat.html)
[Arduino + OV7670 - Without FIFO - Reading Snapshot](http://stackoverflow.com/questions/21220738/arduino-ov7670-without-fifo-reading-snapshot)
# 問題
- 是否為x5行車記錄器DV-5200
- 產品的firmware為何? 用c語言編程嗎? 有開發文件可以參考嗎?
- 儲存於EEPROM? Flash?
- 若不插sd卡，是否還有剩餘空間可以儲放拍攝影片?
- A7的development suite
- 相機wifi模組直上雲端如何實作?
- 相機wifi模組連通相機再上雲端?
- 相機vga模組如何串接led螢幕/micro HDMI訊號輸出
[使用手冊](http://www.px.com.tw/file/R5235G%20DV-5200.pdf)
![](http://ec1img.pchome.com.tw/pic/v1/data/item/201408/C/G/A/A/B/X/CGAABX-A9005D4ZF000_53eac536b3bc7.jpg)
![](http://ec1img.pchome.com.tw/pic/v1/data/item/201408/C/G/A/A/B/X/CGAABX-A9005D4ZF000_53eac536b0132.jpg)
[安霸A7LS晶片-Low Power 1080p60 Sports Camera SoC](http://www.ambarella.com/uploads/docs/A7LS-Brief-121713.pdf)
![block diagram](a7ls-block_diagram.png)

# 實作方向
-

# 參考資料
[楊組長的簡報檔](https://docs.google.com/presentation/d/1YDOFxzw0jFc447zhXs8KCW8-JoTZ0Ao2xqPyMnSn_-Y/edit?usp=sharing)
[楊組長的聯絡方式](https://docs.google.com/spreadsheets/d/1G-skGlVBdP6WQUWLTaJT5_X7XU7ljnzfw59Nyij7NAE/edit#gid=943545685)
[結訓時程](https://docs.google.com/spreadsheets/d/1KotoTrQV_vKnJ3HLMOjBfI9rmW9SiOrhkKDv0UzYulM/edit#gid=178974325)
[專題概述(待填寫)](https://docs.google.com/document/d/1l2KaO17MmfEi9_ocZn87gR5tSc4aLQUertcX6FeEVNo/edit)
[SAMSUNG GALAXY Camera EK-GC200](http://24h.pchome.com.tw/prod/DGAD0N-A90066DLL?q=/S/DGAD0Z)
[2015 最強照相手機機皇 Panasonic DMC-CM1 開箱評測：1 吋感光元件、4.7 吋螢幕動手玩](http://lawrencehou.blogspot.tw/2015/05/2015-panasonic-dmc-cm1-1-47.html)

# 大通產品
[X5跨界行車記錄器DV-5200大通](http://my.px.com.tw/PX/moreinfo_38669.htm)
[大通pxtv-100](http://24h.pchome.com.tw/prod/DMAA6X-A80521833)
![大通pxtv-100](http://ec1img.pchome.com.tw/pic/v1/data/item/201310/D/M/A/A/6/X/DMAA6X-A80521833000_5268dba5a3bbc)

# (Draft)  資策會專題google drive生活記錄器實作詢問

楊組長您好,

我們是資策會嵌入式android就業養成班的學員，對於您提供的**google drive生活記錄器**實作很感興趣，想再跟您討論實作細節，先條列如下，看看是否方便跟楊組長約時間當面討論，謝謝。

1. 此裝置firmware開發平台/SDK
2. 此裝置影像上傳雲端機制:
 - 透過手機
 - 直上雲端
3. 除了google drive外，亦可使用[Picasa Web Albums Data API](https://developers.google.com/picasa-web/)上傳影像，與google drive僅做檔案儲存相比，另可於以下3個Google服務中做相片加值應用
 - [Picasa網路相簿](https://picasaweb.google.com/home)，舊有的網路相簿服務，，介面陽春
 - [Google+相片](https://plus.google.com/u/0/photos/highlights)，將上述相片資料及CRUD功能整合進Google+便於社群分享，較特別的是會自動依據GPS資訊產生相片故事集
 - [Google相片](https://photos.google.com/u/0/)，今年3月由Google+獨立出來的相片服務，功能大抵跟Google+ 照片相同
4. 參考您給的簡報，此裝置是否為[x5行車紀錄器](http://my.px.com.tw/PX/moreinfo_38669.htm)?[安霸A7LS](http://www.ambarella.com/uploads/docs/A7LS-Brief-121713.pdf)?

Henry李兆涵 hamn07@gmail.com
Rock張育誠 xiu43317@gmail.com

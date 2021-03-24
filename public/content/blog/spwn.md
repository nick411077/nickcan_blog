+++
title = "SPWN Download Video"
description = "展示使用Youtube-dl 下載Spwn 影片"
author = "Nick Can"
date = "2021-03-24"
tags = ["youtube-dl","spwn"]
categories = ["youtube-dl"]
comments = true
removeBlur = false
[[images]]
  src = "img/spwn/spwn.jpg"
  alt = ""
  stretch = ""
+++
一般使用Youtube-dl可以下在YT上的影片，那是有人已經幫我們寫好內碼了。  
在Spwn或其他網站上就要自行尋找HLS形式的擴展名為.m3u8的影片。

## 下載Youtube-dl

接下來會教學 Windows/Linux/MacOS 下載方式

### Windows 下載

可以使用官網編譯好的.exe  
下載後創建資料夾放入youtube-dl.exe  
可以使用Path路徑 [Path設定教學](http://kevinpaper.blogspot.com/2019/04/window10-win10.html) 在指令呼叫上會比較方便  
![Path](/nickcan_blog/img/spwn/path01.png)  

開啟**PowerShell** 運行以下代碼(這可以免除重新開機來讀取Path)  

```shell
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
```

### Linux 下載

開啟**終端機**使用apt下載  
`sudo apt-get install youtube-dl -y`

### MacOS 下載

開啟**終端機**使用brew下載  
`brew install youtube-dl`

### Python 下載

`sudo pip install --upgrade youtube_dl`

## 執行Youtube-dl

執行
`youtube-dl`

會出現以下訊息

```text
Usage: youtube-dl [OPTIONS] URL [URL...]

youtube-dl: error: You must provide at least one URL.
Type youtube-dl --help to see a list of all options.
```

就是成功了

## 下載Chrome插件

![cookies](/nickcan_blog/img/spwn/cookies.png)  
我們下載使用[Get Cookies.txt](https://chrome.google.com/webstore/detail/get-cookiestxt/bgaddhkoddajcdgocldbbfleckgcbcid)
來取得Spwn的Cookies

## 開啟Spwn.jp

打開[Spwn](https://spwn.jp)註冊或登入  
選擇你要的直播紀錄  
我們選擇 [**未来 × SPWN AR LIVE -into the Virtual World-**](https://spwn.jp/events/200808-mirai/streaming) 來做示範  
開啟時打開 開發人員工具即是**F12**，轉到 Network選項，在搜尋裡輸入**m3u8**  
![stream](/nickcan_blog/img/spwn/stream.png)  

會發現有**index.m3u8**和**index_12.m3u8**，開頭的**index.m3u8**是畫質選擇然而  
**index_12.m3u8**是最高畫質的影片，所以只需要**index_12.m3u8**  

![copy-stream](/nickcan_blog/img/spwn/copy-stream.png)

對**index_12.m3u8**按右鍵複製連接，這樣就拿到串流的連接了  
但是這樣直接丟到**youtube-dl**是沒辦法下載的，要搭配Cookies  

### 點選 Get cookies.txt

確認反白處有沒有跟你的網址路徑相識，這個很重要如果沒有請確認網址是否正確
確認後按下**Export**下載  

![copy-cookies](/nickcan_blog/img/spwn/copy-cookies.png)

## 下載影片拉

打開**PowerShell**或**終端機** Run

```shell
youtube-dl https://vod.spwn.jp/spwn-vod/200808-mirai/grp1/cam1_v1/index_12.m3u8
```

![error-youtube-dl](/nickcan_blog/img/spwn/error-youtube-dl.png)

一定會收到403報錯，因為沒有帶入Cookies，還有串流連接每次都會不一樣且記不要複製我的喔：)  

帶入Cookies

```shell
 youtube-dl --cookies {youcookies.txt} https://vod.spwn.jp/spwn-vod/200808-mirai/grp1/cam1_v1/index_12.m3u8
```

在--cookies後面的`{youcookies.txt}` 是你的Cookies，按照路徑帶進來或者也可以直接把檔案拉到拉到**終端**就會把路徑帶上了  
![youtube-dl](/nickcan_blog/img/spwn/youtube-dl.png)

如上圖就是這樣就是在下載了  

## 進階應用在VLC上觀看

### 適用Linux/MacOS

帶入 vlc 參數就可以如下圖在VLC上觀看

```shell
 youtube-dl --cookies {youcookies.txt} -o - https://vod.spwn.jp/spwn-vod/200808-mirai/grp1/cam1_v1/index_12.m3u8 | vlc -
```

![vlc01](/nickcan_blog/img/spwn/vlc01.png)
![vlc02](/nickcan_blog/img/spwn/vlc02.png)

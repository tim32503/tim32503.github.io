---
title:  WSL 無法開啟 SQLite 檔案
date:   2021-04-08 17:30:00 +0800
image:  /images/20210408173000/cover.png
tags: [技術筆記, WSL, PC, SQLite, 錯誤排除]
---

## 安裝

因為龍哥說明天要用學資料庫，所以請同學們安裝 **SQLite Browser** ，於是便進到官網開始查安裝說明。

> 應用程式名稱：SQLite Browser
>
> 官網連結：[請點我](https://sqlitebrowser.org/)


因應各家系統，所以安裝方式也非常及MacOS多，除了Windows及macOS可以直接下載安裝檔以外，Linux系統也可以透過指令去下載。

由於課程開始時，龍哥建議使用Windows系統的學生們可以安裝WSL來作為Ruby開發環境。所以這邊應用程式的安裝，我就打算直接透過Linux的終端機來安裝，而不是直接下載Windows安裝檔。而我的Linux系統是使用 Ubuntu 20.04 LTS ，我就採用APT指令方式下載。

首先我們先更新APT的cache

`sudo apt-get update`

更新完成後再繼續接著安裝應用程式本體！

`sudo apt-get install sqlitebrowser`

只是想小小吐槽一下的是APT指令安裝完成後，這個應用程式不會回傳安裝完成之類的訊息...

讓人不太確定到底安裝好了沒啊😅😅😅

OK！沒關係，反正我嘗試開啟SQLite檔案就會知道有沒有安裝成功了吧！

下一步我們透過檔案總管的方式來找到想要開啟的SQLite檔案，剛好我們手邊有建立一個練習用的Rails專案，我們直接用裡面的SQLite檔案來測試看看。

![p1.png](/images/20210408173000/p1.png)

看到SQLite檔案就給他用力地點下去！！！

![p2.png](/images/20210408173000/p2.png)

# ⚠️⚠️⚠️登愣⚠️⚠️⚠️

為什麼會出現錯誤訊息啦！雖然我很開心有安裝成功😭

看了一下上頭的錯誤訊息...

> 錯誤訊息：
> 
> Could not open database file.
> 
> Reason: database is locked

我傻眼，我什麼事情都還沒做怎麼會資料庫被鎖定啦！

好吧！看來只能求助Google大神了！

最後找到一篇比較近期發問的文章，進去閱讀後才發現原來是SQLite Browser的GitHub頁面。

[SQLite Browser fails to open a DB inside a wsl2 installation #2142](https://github.com/sqlitebrowser/sqlitebrowser/issues/2142)

看完整串網友們的討論後，結論是目前沒救😭

簡單來說目前WSL的關係，會導致所有儲存在其之下的sqlite檔案被鎖定，無法正常開啟。但開發者大大們目前似乎有想法，該如何解決這個問題，所以期待後續他們的更新改版囉！

如果現階段真的需要開啟檔案的話，可以先將SQLite檔案移至Windows環境底下的任一位置後 (例如桌面)，就可以直接點擊開啟該資料庫囉！
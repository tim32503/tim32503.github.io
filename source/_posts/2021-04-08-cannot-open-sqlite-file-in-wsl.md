---
title:  WSL 無法開啟 SQLite 檔案
date:   2021-04-08 17:30:00
updated: 2021-04-08 17:30:00
categories: [技術筆記, 錯誤排除]
tags: [Windows PC, WSL, SQLite]
toc: true
cover: cover.webp
---

由於上課所需，開始研究如何在 WSL 中安裝 SQLite Browser，結果意外發現有問題啊！！！

<!-- more -->

## 安裝

因為龍哥說明天要用學資料庫，所以請同學們安裝 **SQLite Browser** ，於是便進到官網開始查安裝說明。

{% note info %}
【應用程式名稱】SQLite Browser
【官網連結】{% btn https://sqlitebrowser.org/, 請點我 %}
{% endnote %}

因應各家系統，所以安裝方式也非常及 MacOS 多，除了 Windows 及 macOS 可以直接下載安裝檔以外，Linux 系統也可以透過指令去下載。

由於課程開始時，龍哥建議使用 Windows 系統的學生們可以安裝 WSL 來作為 Ruby 開發環境。所以這邊應用程式的安裝，我就打算直接透過 Linux 的終端機來安裝，而不是直接下載 Windows 安裝檔。而我的 Linux 系統是使用 Ubuntu 20.04 LTS ，我就採用 APT 指令方式下載。

首先我們先更新 APT 的 cache

```
sudo apt-get update
```

更新完成後再繼續接著安裝應用程式本體！

```
sudo apt-get install sqlitebrowser
```

不過想小小吐槽一下的是 APT 指令安裝完成後，這個應用程式不會回傳安裝完成之類的訊息...
讓人不太確定到底安裝好了沒啊😅😅😅

OK！沒關係，反正我嘗試開啟 SQLite 檔案就會知道有沒有安裝成功了吧！

下一步我們透過檔案總管的方式來找到想要開啟的 SQLite 檔案，剛好我們手邊有建立一個練習用的 Rails 專案，我們直接用裡面的 SQLite 檔案來測試看看。

{% asset_img p1.webp %}

看到 SQLite 檔案就給他用力地點下去！！！

{% asset_img p2.webp %}

⚠️⚠️⚠️ 登愣 ⚠️⚠️⚠️
為什麼會出現錯誤訊息啦！雖然我很開心有安裝成功😭
看了一下上頭的錯誤訊息...
我傻眼，我什麼事情都還沒做怎麼會資料庫被鎖定啦！

{% note warning %}
Could not open database file.
Reason: database is locked
{% endnote %}

好吧！看來只能求助 Google 大神了！
最後找到一篇比較近期發問的文章，進去閱讀後才發現原來是 SQLite Browser 的 GitHub 頁面。

[SQLite Browser fails to open a DB inside a wsl2 installation #2142](https://github.com/sqlitebrowser/sqlitebrowser/issues/2142)

看完整串網友們的討論後，結論是目前沒救😭
簡單來說目前 WSL 的關係，會導致所有儲存在其之下的 sqlite 檔案被鎖定，無法正常開啟。但開發者大大們目前似乎有想法，該如何解決這個問題，所以期待後續他們的更新改版囉！
如果現階段真的需要開啟檔案的話，可以先將 SQLite 檔案移至 Windows 環境底下的任一位置後 (例如桌面)，就可以直接點擊開啟該資料庫囉！

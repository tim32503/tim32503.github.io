---
title: Access Database載入錯誤
date: 2019-09-11 12:30:00
updated: 2019-09-11 12:30:00
categories: [技術筆記, 錯誤排除]
tags: [VB.NET, Access Database]
toc: true
cover: cover.webp
---

當出現「Microsoft.ACE.OLEDB.12.0 提供者並未登錄於本機電腦」錯誤訊息時，可參考本文以透過安裝套件來排除問題。

<!-- more -->

## 問題描述

透過VB.NET的程式上傳檔案時，發生錯誤…
發生的程式段落為 `Dim test As New OleDbDataAdapter(sqlText, connString)`
接著畫面就出現以下錯誤訊息了

{% note warning %}
_Microsoft.ACE.OLEDB.12.0 提供者並未登錄於本機電腦_
{% endnote %}

## 解決方法
1. 點選下方至微軟官網下載套件即可排除此錯誤問題
   {% note info %}
    【應用程式名稱】Microsoft Access Database Engine 2010 可轉散發套件
    【下載連結】{% btn https://www.microsoft.com/zh-tw/download/details.aspx?id=13255, 請點我 %}
   {% endnote %}
2. 下載並安裝 64 位元版本：VB 程式仍舊出現相同的錯誤訊息
3. 下載並安裝 32 位元版本：安裝程式告知已安裝過其他版本，需進行移除後方能安裝
4. 將 64 位元版本解除安裝
5. 重新安裝 32 位元版本：**Done!!**

## 參考文件
1. [[C#] 解決’Microsoft.ACE.OLEDB.12.0′ 提供者並未登錄於本機電腦…](https://dotblogs.com.tw/dragoncancer/2016/03/31/102924)
2. [Access Database Engine 2010：安裝 64 位元與 32 位元版本的驅動程式在同一作業系統上](http://sharedderrick.blogspot.com/2013/04/access-database-engine-2010-64-32.html)
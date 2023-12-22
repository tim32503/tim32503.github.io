---
title: 水晶報表發生 JavaScript 執行階段錯誤
date: 2019-10-05 17:11:00 +0800
image: /assets/img/20191005171100/cover.png
categories: [技術筆記, 錯誤排除]
tags: [VB.NET, Crystal Report, Javascript]
hidden: false
---

當 Crystal Report 在本機偵錯時，出現「JavaScript 執行階段錯誤」的錯誤訊息時，可透過文中方法排除問題。

## 問題描述

Crystal Report在本機偵錯時，可能發生此錯誤訊息，如下圖1：

![p1.png](/assets/img/20191005171100/p1.png)

## 解決方法

1. 至 `C:\inetpub\wwwroot\aspnet_client\system_web\4_0_30319` 底下找到 `crystalreportviewers13` 這個資料夾後，複製貼上到開發中的專案資料夾中
  ![p2.png](/assets/img/20191005171100/p2.png)
2. 並在欲開啟報表的網頁中（如圖1中所示的APP_0004_PR.aspx），於標籤中加入以下語法：
```javascript
<script src='<%=ResolveUrl("~/crystalreportviewers13/js/crviewer/crv.js")%>' type="text/javascript"></script>
```
3. 重新嘗試開啟報表後，即可於本機中正常顯示，Done!!
  ![p3.png](/assets/img/20191005171100/p3.png)

## 參考文件
1. [解決crystal report水晶報表在瀏覽器提示bobj未定義的錯誤](https://www.cnblogs.com/muzinian/p/4721690.html)
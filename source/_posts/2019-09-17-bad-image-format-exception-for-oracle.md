---
title: Oracle 用戶端程式庫載入錯誤
date: 2019-09-17 16:20:00
updated: 2019-09-17 16:20:00
categories: [技術筆記, 錯誤排除]
tags: [VB.NET, Oracle]
cover: cover.webp
toc: true
---

偵錯時出現「嘗試載入 Oracle 用戶端程式庫時傳出 BadImageFormatException。當與具有 32 位元的 Oracle 用戶端元件執行 64 位元模式安裝時，會出現此問題。」錯誤訊息時，可透過文中方法排除問題。

<!-- more -->

## 問題描述

嘗試偵錯時，Log 描述中出現下列訊息

{% note warning %}
嘗試載入 Oracle 用戶端程式庫時傳出 BadImageFormatException。
當與具有 32 位元的 Oracle 用戶端元件執行 64 位元模式安裝時，會出現此問題。
{% endnote %}

## 解決方法

設定程式執行在 x86 模式下即可，參考以下設定

1. 開啟 `組態管理員`
   {% asset_img p1.webp %}
2. 點選在 `使用中的方案平台` 下拉清單後，按 `新增` 
   {% asset_img p2.webp %}
3. 在 `輸入或選擇新平台` 選擇 `x86` 後按 `確定` 
   {% asset_img p3.webp %}
4. 設定完成後，重新嘗試進行偵錯：Done!!

## 參考文件

1. [出現 [嘗試載入 Oracle 用戶端程式庫時傳出 BadImageFormatException。當與具有 32 位元的 Oracle 用戶端元件執行 64 位元模式安裝時，會出現此問題。]，該如何處理?](https://dotblogs.com.tw/chou/archive/2011/10/11/41156.aspx)
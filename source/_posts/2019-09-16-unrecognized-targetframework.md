---
title: .NET Framework 組態錯誤
date: 2019-09-16 11:18:00
updated: 2019-09-16 11:18:00
categories: [技術筆記, 錯誤排除]
tags: [VB.NET]
toc: true
cover: cover.webp
---

出現「無法辨認的屬性 ‘targetFramework’。請注意，屬性名稱必須區分大小寫」的錯誤訊息時，可嘗試透過文中方法排除問題。

<!-- more -->

## 問題描述

{% note danger %}
剖析器錯誤訊息：
無法辨認的屬性 ‘targetFramework’。請注意，屬性名稱必須區分大小寫。
{% endnote %}

## 解決方法

調整目標 Framework 至 `.NET Framework 4` 即可
1. 嘗試重開專案並偵錯：仍舊顯示錯誤訊息
2. 對 `專案` 點選右鍵更改 `屬性` 中 `建置` 的 `目標 Framework` 設定：Done!!

{% asset_img p1.webp %}
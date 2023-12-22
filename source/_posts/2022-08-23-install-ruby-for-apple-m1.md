---
title: 都是 M1 惹的禍？輕鬆帶你搞定 Ruby 環境安裝！
date: 2022-08-23 13:56:00 +0800
image: /assets/img/20220823135600/cover.png
categories: [技術筆記, 都是M1惹的禍？]
tags: [Ruby, Mac M1]
hidden: false
---

之前耳聞過 Mac M1 在環境安裝會遇到不少問題⋯⋯本篇將帶你一起解決安裝 Ruby 環境時的疑難雜症！

## 前言
新公司報到第一天，領到公司配發的工作機⋯⋯

**太讚啦！居然是 M1 新機欸！嗯～真香！**

除了認識同事外，報到不外乎要建置開發環境，想到這邊突然有種不好的預感 🤨

## 聲明
> 因本文僅適用於 Mac 環境，還請 Windows 的朋友們尋找其他篇文章協助解決環境安裝問題
{: .prompt-info }

## 安裝過程

### 安裝 RVM
首先我們先安裝 RVM ，這是為了幫助我們可以管理不同版本的 Ruby 環境

1. 透過終端機輸入以下指令
```bash
\curl -sSL https://get.rvm.io | bash -s stable
```
上述的這個指令也可以在 https://rvm.io/ 的首頁找到唷！

2. 查詢 RVM 的版本號，以確認是否成功安裝
```bash
rvm -v
```
如果有正確安裝成功的話，輸入指令後會如下圖，得到現在的版本號
![p1.png](/assets/img/20220823135600/p1.png)

### 安裝 Ruby
操作 RVM 的相關指令，可以在 <https://rvm.io/rvm/cli> 查得到，或是終端機直接輸入指令 `rvm help`

1. 查詢可安裝的 Ruby 種類及其版本號
```bash
rvm list known
```
2. 開始安裝
```bash
rvm install 2.5  # rvm install [版本號]
```
依照你所想安裝的版本，可以任意替換後方版本號的數值

3. 跑跑跑，登愣！！！
![p2.png](/assets/img/20220823135600/p2.png)
沒想到預感成真，居然給我跑紅字出來！果不其然開始安裝不久就遇到問題 🙄\
\
OK Fine! 立刻有請 Google 大神，才剛膜拜完立刻得到解法！
 
4. 調整剛剛的安裝指令
```bash
CFLAGS="-Wno-error=implicit-function-declaration" rvm install 2.5
```
![p3.png](/assets/img/20220823135600/p3.png)

5. 恭喜🎉🎉🎉\
出現 `Install of ruby-2.5.8 - #complete` 就代表安裝完成啦！你也可以再用 `ruby -v` 檢查現在的 Ruby 版本號是不是對應剛剛所安裝的！
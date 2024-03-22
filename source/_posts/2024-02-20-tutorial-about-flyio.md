---
title: 部署平台新寵兒！教你快速上手 Fly.io ！
date: 2024-02-20 13:10:24
categories: [技術筆記]
tags: [Rails, 部署平台, Fly.io, 錯誤處理]
toc: true
cover: cover.webp
top_img: top_image.webp
---

這篇文章主要記錄部署平台改用 Fly&period;io 的歷程，會簡單介紹整個部署流程以及曾遇過的問題。

<!-- more -->

## 前言

還記得當時在 ASTRO Camp 時，總習慣用 Heroku 作為我的部署平台首選，沒有別的原因——就是因為免費！

不過由於平台官方考量[^heroku_next_chapter]，從 2022/10/26 起，Heroku 將開始刪除不活躍的帳號，直到 2022/11/28 將完全停止提供免費方案。
於是大家便開始苦尋下一個替代方案，而其中一個選擇就是這篇要介紹的 **[Fly.io](https://fly.io/)** 啦！

{% note info %}
【網站名稱】Fly&period;io
【網站連結】https://fly.io/
{% endnote %}

## 註冊

Fly&period;io 支援第三方登入功能，所以可以直接透過 Google 或是 GitHub 帳號來註冊。
因為步驟蠻簡單的，所以這部分就先略過囉！
還是有疑問的話，可以在下方留言，如果我幫得上忙的話會盡力回覆的！

註冊完的重點是綁定信用卡！

Fly&period;io 有提供免費試用，但須先完成信用卡綁定，並且使用預設的 `Personal` 組織，不要另外自行建立新組織。
計畫選擇 `Hobby`，完成後，系統就會自動提供 5 美元的額度到 `Personal` 組織底下讓你使用，而這個額度是沒有使用期限[^new_customer_in_fly_io]。
用完額度後系統就會開始按照 `Hobby` 計畫每個月自動扣款 5 美元，大家可以用免費額度來測試看看這個部署平台是否適合自己的需求～

## 部署

正如 Fly&period;io 在官網首頁提及的特色，可以透過簡單的幾個指令就順利將專案部署上去！

```bash
> 在 Mac OS 上安裝 flyctl 工具
$ brew install flyctl

> 在專案中建立部署設定檔
$ fly launch

> 執行部署作業
$ fly deploy
```

## 問題處理

在使用這樣的新興平台，難免會遇到各式各種的問題需要解決。而他們家有提供了 Community 這樣的論壇，讓大家可以盡情發問，而這些留下來的問答紀錄就能在緊要關頭時幫上忙！
下面也紀錄了先前苦惱很久的部署問題，希望能幫大家避開地雷～

### 為什麼我的 Rails 專案總是部署失敗...

每次部署使用 `fly deploy` 的指令後，總是會出現下面的錯誤訊息：

```bash
✖ release_command failed
Error release_command failed running on machine e286000c340386 with exit code 139.
```

原本以為是錯誤訊息所說，跟 `release command` 有關，所以一直在研究 `Dockerfile` 及 `fly.toml` 設定黨哪裡有問題。
直到找到這篇文章[^dockerfile_for_ruby]才解決了我的疑惑，原來一直失敗是跟我的 Ruby 版本有關。

因為在起初設定 VM 時，我只有將主機的記憶體大小設定使用 256 MB，而專案使用的 Ruby 版本則是使用 3.3。
根據文章的回答我推測應該是 Ruby 3.3 版在部署時需要較大一些的記憶體容量來去執行，
所以要解決這個問題就是將主機記憶體設定大一些即可。當然，如果要選擇降版至 3.2 也是可行的做法之一。

後來按照文章的建議，選擇將主機記憶體重新設定為 512 MB 後，便能順利部署成功了！

但畢竟當初會選擇將主機記憶體設定為 256 MB 也是因為免費額度的關係，改為設定 512 MB 後就開始被收費了。
如果只是想玩一些測試用的專案，這點就需要注意一下！

## 參考資料
[^heroku_next_chapter]: [Heroku’s Next Chapter - Focus on Mission Critical](https://blog.heroku.com/next-chapter#focus-on-mission-critical)
[^new_customer_in_fly_io]: [Fly.io Resource Pricing](https://fly.io/docs/about/pricing/?source=post_page-----5f9f5cdb837b--------------------------------#new-customers)
[^dockerfile_for_ruby]: [DockerFile help for Ruby 3.3.0](https://community.fly.io/t/dockerfile-help-for-ruby-3-3-0/17700)
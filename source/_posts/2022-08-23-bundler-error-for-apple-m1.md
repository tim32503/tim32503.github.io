---
title: 都是 M1 惹的禍？連 Bundler 也遭殃？！
date: 2022-08-23 16:35:00 +0800
image: /assets/img/20220823163500/cover.png
categories: [技術筆記, 都是M1惹的禍？]
tags: [Ruby, Ruby on Rails, Mimemagic, Mysql2]
hidden: false
---

都是 M1 惹的禍？第二彈！本篇將帶你一起解決執行 Rails 專案時可能發現的 gem 安裝失敗問題！

## 前言
好不容易搞定了 Ruby 安裝，接下來當然就要開始起專案啦！

## 過程

### Mimemagic 安裝失敗
1. 專案資料夾打開後，起手式當然是
```bash
bundle install
```
![p1.png](/assets/img/20220823163500/p1.png)\
嗯？哈囉？ 為什麼又送我紅字啊——（吶喊）

2. 閱讀了紅字後，先按照紅字建議去處理
```bash
gem install mimemagic -v '0.3.10' --source 'https://rubygems.org/'
```
![p2.png](/assets/img/20220823163500/p2.png)
Rake failed? 怎麼又失敗了

2. 只好把剛剛出現過的紅字複製後，拿去請教 Google 大神\
大神表示：
```bash
brew install shared-mime-info
```
\
![p3.png](/assets/img/20220823163500/p3.png)\
\
執行後，如果有成功的話就會看到這樣的啤酒訊息
```bash
🍺  /opt/homebrew/Cellar/shared-mime-info/2.2: 86 files, 4.6MB
```

### Mysql2 安裝失敗
1. 安裝完 Mimemagic 後，再重新 bundle 一次
![p4.png](/assets/img/20220823163500/p4.png)
真棒🙄 又錯了 呵呵呵

2. 繼續拿著紅字去拜大神
大神表示：確認`mysql`、`openssl`、`zstd`是否安裝，再安裝`mysql2`

3. 透過 homebrew 安裝
因為我需要安裝特定版本的 mysql，所以是使用下方指令
```bash
brew install mysql@5.7 openssl zstd
```

4. 緊接著再安裝`mysql2`
```bash
gem install mysql2 -v '0.5.2' -- --with-mysql-config=$(brew --prefix mysql)@5.7/bin/mysql_config --with-ldflags="-L$(brew --prefix zstd)/lib -L$(brew --prefix openssl)/lib" --with-cppflags=-I$(brew --prefix openssl)/include
```
指令中的`0.5.2`可替換成需安裝的`mysql2`版本號，另外因為我安裝的`mysql`是有指定`5.7`這個版本，所以在上方指令中需加入`@5.7`，若你沒有指定版本的話，可移除

5. 最後再重新 bundle 一次就成功啦🎉

## 參考資料
1. [Mimemagic Issue #162](https://github.com/mimemagicrb/mimemagic/issues/162 "Mimemagic Issue #162") 
2. [How to install mysql2 gem on m1 Mac](https://gist.github.com/fernandoaleman/385aad12a18fe50cf5fd1e988e76fd63 "How to install mysql2 gem on m1 Mac")
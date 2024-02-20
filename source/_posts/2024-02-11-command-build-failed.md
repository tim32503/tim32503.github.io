---
title: Yarn 指令建置失敗！
date: 2024-02-11 16:16:58
categories: [技術筆記]
tags: [Rails, 錯誤處理, Yarn, cssbundling-rails, jsbundling-rails]
toc: true
cover: cover.webp
top_img: top_image.webp
---

最近在練習做 Side project 的時候，發現每次將 commit 推上去到 GitHub 後，CI 都會一直出現 `yarn build:css` 的錯誤，花了很久的時間才總算裡出一些頭緒...
趁著記憶猶新，趕快筆記下來吧！

<!-- more -->

## 情境

每次 GitHub Actions 執行到一半時，都會跳出以下的錯誤訊息：

```bash
yarn install v1.22.21
[1/4] Resolving packages...
success Already up-to-date.
Done in 0.10s.
yarn run v1.22.21
error Command "build:css" not found.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
rake aborted!
cssbundling-rails: Command build failed, ensure `yarn build:css` runs without errors
/home/runner/work/expense-tracker/expense-tracker/vendor/bundle/ruby/3.2.0/gems/cssbundling-rails-1.3.3/lib/tasks/cssbundling/build.rake:14:in `block (2 levels) in <main>'
/home/runner/work/expense-tracker/expense-tracker/vendor/bundle/ruby/3.2.0/gems/rspec-rails-6.1.0/lib/rspec/rails/tasks/rspec.rake:26:in `block (2 levels) in <main>'
Tasks: TOP => test:prepare => css:build
(See full trace by running task with --trace)
Error: Process completed with exit code 1.
```

## 研究過程

```shell
cssbundling-rails: Command build failed, ensure `yarn build:css` runs without errors
```

光研究這問題沒想到就花掉不少時間，而且為了做筆記，又重新釐清較為正確的原因為何。
原先一開始只是猜這個錯誤是由於 `cssbundling-rails` 這個套件所造成的，所以很粗暴的直接把該套件從 Gemfile 中註解掉後重新執行 `bundle install`。
這樣的確是有順利解決錯誤，但總覺得哪裡怪怪的？（ ~~不是解決問題，而是解決出現問題的套件？~~ ）

爬文過程中看到有網友先前在 Rails 的 GitHub issue 中提出問題，而其中有一則[回答](https://github.com/rails/rails/issues/43338#issuecomment-981658685)被不少人按讚。該則回答提到他的解法是在重新安裝 node/npm/yarn 過後執行下列指令重新安裝。

```shell
./bin/rails javascript:install:[esbuild|rollup|webpack]
./bin/rails css:install:[tailwind|bootstrap|bulma|postcss|sass]
```

仔細端詳後發現這兩個指令，似乎就等同我在新建專案時所使用的指令。
現在回想起來當時在新建專案時，我是使用 `rails new expense-tracker --database=postgresql --css=tailwind --javascript=esbuild` 指令。
而上述提到的 `rails css:install:[tailwind|bootstrap|bulma|postcss|sass]` 及 `rails new expense-tracker --css [tailwind|bootstrap|bulma|postcss|sass]` 兩個指令，都是來自於 `cssbundling-rails` 這個套件，這時候才發覺我直接把它從 Gemfile 中註解移除太過暴力了🤣

在把 `cssbundling-rails` 套件重新安裝回去的過程，我另外找到一篇[文章](https://github.com/rails/jsbundling-rails/issues/45)。
發文的網友和我一樣 javascript 部分是選用 `ESBuild`，閱讀完文章內容後，我才瞬間驚醒，原來這才是問題所在啊！

原來 `ESBuild` 和 `cssbundling-rails` 在執行完各自的指令 `build` & `build:css` 後都會產生 `application.css` 檔案，也因此產生衝突。

而這點，後續 DHH 也有在 `jsbundling-rails` 的 GitHub Readme 文件中新增補充說明，可參考[連結](https://github.com/rails/jsbundling-rails/tree/928868ec226eda914c8ba801b94351b949cf9bf4?tab=readme-ov-file#why-does-esbuild-overwrite-my-applicationcss)。

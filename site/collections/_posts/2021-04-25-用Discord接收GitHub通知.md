---
title:  用 Discord 接收 GitHub 通知
date:   2021-04-25 15:00:00 +0800
image:  '/images/20210425150000/cover.png'
tags:   [技術筆記, GitHub, Discord, Webhook]
---

想知道如何在 Discord 聊天室中接收到 GitHub 的事件通知嗎？本篇將帶給你完整的手把手教學！

## Discord 設定

首先在群組中選擇欲設定的【文字頻道】，點擊旁邊齒輪的圖示進入到設定畫面。
![p1.png](/images/20210425150000/p1.png)

接著於左側的選單中選擇【整合】，若之前不曾建立過 Webhook 的話，應該會看到如下圖所示【建立 Webhook】的按鈕。
![p2.png](/images/20210425150000/p2.png)

但如果之前有建過 Webhook 的話，則會如下圖一樣呈現出【查看 Webhook】的字樣，點進去之後點擊【新 Webhook】的按鈕亦可。
![p3.png](/images/20210425150000/p3.png)

成功建立後就會出現可以編輯 Webhook 資訊的區塊，當編輯完欲命名的名稱後，就可以直接點擊【複製 Webhook 網址】。
![p4.png](/images/20210425150000/p4.png)

看到【已複製】的訊息後，我們就可以準備開始設定 GitHub 的部分囉！

**_複製好的 webhook 網址請注意不要任意公開散布出去給他人，因為只要取得此網址後，他人即有權限可傳送訊息至該頻道中。_**



## GitHub 設定

登入 GitHub 並找到你想要設定的 Repo 後，點擊【Settings】頁籤。
然後一樣選擇左側選單中的【Webhooks】，並且找到右側【Add webhook】按鈕點下去！
![p5.png](/images/20210425150000/p5.png)

系統沒意外會請你輸入 GitHub 密碼，確認你的身分。再來就可以開始設定 webhook 啦！接下來的幾個步驟非常重要，千萬要確認你填的資訊都沒有錯喔！
![p6.png](/images/20210425150000/p6.png)

1. **Payload URL**
   必填，請將剛剛從 Discord 上複製好的 webhook 網址貼於此格中，貼好後並於網址最後方加上 `/github` 的字串。
2. **Content type**
   內容類型請選擇【application/json】
3. **Events**
   這邊有三種事件類型可被觸發，個人建議可以選擇第２項【Send me everything.】，這樣就能接收到所有事件的通知。
4. **Active**
   請勾選此欄以確保當有事件被觸發的時候，系統會發送詳細資訊到我們的 Discord 頻道中。

以上都確認填寫完畢後，就可以大膽地點擊綠色的【Add webhook】按鈕啦！
到這邊就完成我們所有的設定啦！ ⁽⁽٩(๑˃̶͈̀ ᗨ ˂̶͈́)۶⁾⁾

## 測試

最後最後我們來簡單的測試一下，確認功能是不是正常運作！
我們隨意編輯一個檔案 (這邊我用 README.md 測試) 後並 commit 送出。

說時遲那時快，Discord 立刻"叮"的一聲！
沒錯！我們成功收到 commit 的通知啦！
![p7.png](/images/20210425150000/p7.png)

這麼方便的通知功能，快用在自己的專案團隊中吧！

## 參考資料
1. [GitHub Docs-Creating webhooks](https://docs.github.com/en/developers/webhooks-and-events/creating-webhooks)
2. [DiscordにGithubのリポジトリの変更通知を送る方法](https://qiita.com/Papillon6814/items/7bfd95cbd1b5a80afb92)

---
title: 與 AI 對話！ LLM 應用開發工作坊心得分享！
date: 2023-11-01 22:59:41
categories: [技術筆記]
tags: [AI, 生成式 AI, LLM, 大語言模型, 五倍學院, 工作坊, 心得分享]
toc: true
cover: cover.webp
top_img: top_image.webp
---

自從 ChatGPT 爆紅後，人們開始更加關注 AI 接下來的發展與應用，甚至 2023 年更被譽為「生成式 AI 元年」。各領域也不斷地尋找 AI 適用的應用情境，思考著能如何用來提升工作效率及增加利潤。然而，身為工程師的我們當面對這樣的新技術誕生時，更不該因為害怕被新技術取代而拒絕去認識它；反之，我們更該嘗試認識它，看能藉由何種方式來幫助提升自我的價值。

<!-- more -->

{% asset_img 5xcampus_post_cover.webp "【圖片出處】Facebook 粉絲專頁 - 五倍學院" %}

## 課程資訊

{% note info %}
**大語言模型 LLM 應用開發工作坊**

【講師】張文鈿（ihower）
【時間】2023/10/15 (日) 10:00 ~ 17:00
【地點】五倍紅寶石
【簡介】[請點我](https://5xcampus.com/courses/ai-workshop.html?utm_source=curihaosity&utm_medium=post)
{% endnote %}

## 麻瓜的有勇無謀

在開始上課前，我想我對於 AI 的認識就和普羅大眾差不多吧！

透過 ChatGPT[^chatgpt] 、 Google Bard[^bard] 等工具協助我們寫文章、找答案，幾乎都快成了 24 小時 On Call 、不須下班的私人家教；在 DALL·E2[^dalle2] 、 Midjourney[^midjourney] 的畫布上用提示詞揮灑出屬於我們的創作，誤以為自己是 21 世紀的畢卡索再世。一晃眼間，許多的 AI 應用網站推陳出新，便已令眾人愛不釋手、陶醉其中。

而比較深入一些的認識，應該就是開始了解「何謂提示詞」了吧！

畢竟在網路上各式各樣的咒語心得文唾手可得，像是教會你如何「成為宮崎駿第二人」、「快速解開程式難題」等等。這類型的分享文章好似咒語百科般數之不盡，多到不禁讓人幻想著是否自己信手捻來便能像哈利波特一樣與「那個人」交戰。網友們口中所謂的「咒語」正是生成式 AI 使用到的「提示詞（Prompt）」，但我們像麻瓜般的有勇無謀，只是一味的使出咒語來自娛娛人，卻不知其中潛藏的危險性。

## 符咒學，上課了！

起初，講者先是帶著我們認識何謂提示詞。我們都知道使用咒語需要手持魔杖、專心一志並且大聲唸出咒語，而工程師想使用 LLM 也只需要透過呼叫 API 並且帶入所需參數及提示詞後便能完成。例如，在相同的提示詞（咒語）之下，若帶入的「溫度（temperature）」數值越接近 1 時，API 的回應及隨機性會更富有創造力；反之，越接近 0 的回覆則更接近機器人般的制式回答。原來只是簡單調整其中這麼一項參數，就能使 AI 的回答更加人性化！

```python
user_message = "小明愛吃什麼? "

messages = [
    {
        "role": "user",
        "content": user_message
    }
]

response = get_completion(messages, temperature=0.9)  # 可以改看看溫度
print(response)  # 我不知道小明喜歡吃什麼，因為我不認識他。每個人都有自己喜歡的食物偏好，只有小明自己知道他愛吃什麼。
```

## 大腦高速運轉後的收穫

講者帶來的內容著實豐富，從基礎到進階、玲琅滿目。隨著課程進度來到進階篇章時，大腦也早已處於高速運轉的狀態中。講師在介紹完「提示詞工程」後，便帶領我們認識 LLM 的幾種常見應用，像是：ChatBot 對話應用、摘要轉錄、QA 應用等等。

{% asset_img p1.webp "【圖片出處】edX LLM Application through Production 課程" %}

而大家最感到興趣的莫過於從早上就開始敲碗的應用主題－－「語意搜尋 + QA 應用」，簡單來說就是先使用程式去搜尋各種相關內容後，再將收集到的資訊及問題拿去問 LLM ，最後就可以得到所需的答案了！整個問答流程前後完全不需要耗費太多時間，也難怪在 ChatGPT 剛問世不久時就已經有客服人員開始擔心自己會不會面臨失業的困境。

在認識完幾種常見應用後，該如何將 LLM 妥善運用至各種情境中，讓其成為一大助力，我想這便是軟體工程師的價值其一所在吧！

## 結語

這堂課確實為我打開 AI 世界大門，儘管尚未能完全掌握課程的全部精華，但至少在我的心中已經埋下一顆對於 AI 好奇心的種子。課程結束不是終點，學海無涯，唯勤是岸，期許自己將講師的豐富教材仔細著墨後，能促使自己躍上另一境界！如果對於 AI 這門學問也甚是好奇，不妨藉由這堂課程帶領你一探箇中奧妙，相信定有所獲的！

## 參考來源

[^chatgpt]: [對話式 AI 工具 – ChatGPT by OpenAI](https://openai.com/chatgpt)
[^bard]: [對話式 AI 工具 – Bard by Google](https://bard.google.com/chat)
[^dalle2]: [生成式 AI 繪圖工具 – DALL·E 2 by OpenAI](https://openai.com/dall-e-2)
[^midjourney]: [生成式 AI 繪圖工具 – Midjourney by Midjourney](https://www.midjourney.com/home)
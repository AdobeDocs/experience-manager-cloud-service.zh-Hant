---
title: 內容更新技能
description: 瞭解Experience Production Agent的內容更新技能以及可為您執行的操作。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8cd524891df550913a734a9355c1012dc11adf5b
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---


# 內容更新技能 {#content-update}

Experience Production Agent的內容更新技能可自動化內容製作，以加速Adobe Experience Manager (AEM) as a Cloud Service和Edge Delivery Services的日常工作。

內容更新技能會更新CMS中的現有內容，包括內容片段、頁面、表單和資產。 代理程式可以執行更新、移除、取代或新增內容元素等動作，以保持體驗精確且最新。 輸入可以是自然語言說明，在搭配Jira PDF使用時，熒幕擷取畫面也可以提供輸入。

## 概觀 {#overview}

內容更新技能透過自然語言或視覺效果將您提供的詳細資料轉換為頁面上的內容更新。 您可以提供需要更新的頁面URL，以及需要更新的詳細資訊，而代理程式技能會完成您的工作。

## 功能 {#capabilities}

您可以從以下位置存取內容更新技能：

* [AI 助理](#ai-assistant)

* [Jira](#jira)

## AI 助理 {#ai-assistant}

您可以透過AI助理存取AEM Business Agent。

從experience.adobe.com開啟AI小幫手，然後使用`Ask AI Assistant anything`欄位以自然語言指定提示來開始互動：

![存取探索代理程式](/help/ai-in-aem/agents/production/assets/content-update-ai-assistant-example.png)

### 範例提示 {#sample-prompts}

若要啟動內容更新，您可以提供各種自然語言提示。 您也必須指定要更新之頁面的公開顯示URL。 例如：

* 修改下列頁面https://www.your-url.com/sale將主圖示題更新為「黑色星期五特大促銷 — 高達70%折扣」、將倒數計時器變更為「48小時後結束」、移除「註冊更新」、將所有「立即購買」按鈕變更為「搶先交易」

* https://www.your-url.com/laptops/your-laptop-model將橫幅副本更新為「僅今日節省300美元」，將價格從1,299美元更新為999美元，移除融資選項橫幅

* https://www.your-url.com/your-sneaker將庫存狀態從「低庫存」更新為「補貨 — 有限數量」，變更大小選擇器以綠色反白顯示可用大小，移除「即將推出」徽章

* https://www.your-url.com/your-sneaker更新產品影像以顯示新色道

>[!NOTE]
>
>使用[Jira](#jira)互動時可以使用檔案上傳，但AI助理不支援此功能。

## Jira {#jira}

搭配Jira使用內容更新技能可讓您建立票證，並附上自動化編輯的指示。

### 建立票證 {#create-a-ticket}

建立Jira票證（任何型別）。

您票證的&#x200B;**描述**&#x200B;欄位中有兩個必要的詳細資料：

1. 您要編輯之頁面的公開顯示URL。

1. 所需的變更。

   目前，該技能支援以下格式範圍來描述您的變更：

   * 票證說明中的自然語言
      * 例如「將標題從X變更為Y」
   * 附加註解的PDF
      * 例如，建立頁面的PDF，並新增註解，詳細說明您要變更的專案
   * 在附加的PDF中發表評論
      * 例如，建立頁面的PDF，並新增詳述您想要變更專案的註解
   * 附加附註的熒幕擷圖
      * 例如，擷取部分頁面的熒幕擷圖，並新增詳細說明您想要變更專案的註解
   * 附加的Microsoft Word檔案，包含自然語言變更

### 從您的票證叫用代理程式 {#invoke-the-agent-from-your-ticket}

若要使用代理程式，請在您的票證中新增註解。 在註解中提及具有`@`符號的代理程式，以及它應執行的命令；例如：

* `@aemagent@adobe.com process`

目前，代理程式瞭解下列命令：

* `process` — 處理要求
* `cancel` — 取消處理請求
* `retry` — 重新處理請求
* `feedback` — 將意見反應套用至上一代
* `reprocess` — 重新處理原始請求

### 代理程式如何互動 {#how-the-agent-interacts}

您向代理程式發出命令後，代理程式會在Jira中回應註釋。 註解會詳細說明代理程式的進度，以及所採取的動作。

若是用來觸發更新的`process`命令，回應可能會依照下列順序：

* 初始註解會確認代理程式已啟動。

* 工作完成後。 代理程式會以另一個註解回應，其中包含所採取動作的詳細資訊。
   * 代理程式進行的內容更新為非破壞性，這表示這些更新會提供給預覽執行個體。
   * 註解包含更新連結，因此您可以視需要檢閱和發佈，或將Jira指派給負責人員。

* 下圖顯示觸發內容更新技能的`process`命令的Jira範例：

  ![使用Experience Production Agent的內容更新技能的Jira範例](assets/content-update-jira-example.png)

## 啟用 {#activation}

若要啟用和存取Experience Production Agent，您需要聯絡Adobe。 若要開始使用，您可以聯絡：

* `experience-production-agent@adobe.com`
* 或聯絡您的帳戶團隊

若要加速此程式，提供下列資訊會有所幫助：

* 適用於AEM as a Cloud Service
   * 您需要提供您的：
      * 組織 ID
      * `product_id`
      * `profile_id`

   * 您可以透過下列步驟找到這些值：
      * 您的管理員需要造訪<https://adminconsole.adobe.com/>
      * 選取&#x200B;**Adobe Experience Manager as a Cloud Service**
      * 選取適當的AEM執行個體
      * 選取允許相關內容讀寫操作的設定檔
      * 抓取瀏覽器URL
      * 從URL擷取`product_id`和`profile_id`。
例如 <https://adminconsole.adobe.com/products/profiles/users>

* Edge Delivery檔案製作
   * 為您的Adobe團隊提供下列資訊：
      * 相關網域
      * 相關Github資訊：
         * 組織
         * 存放庫
         * 分支

## 限制 {#limitations}

目前，內容更新程式的限製為：

* 與[Jira](#jira)互動時，可以使用檔案上傳，但是與[AI小幫手](#ai-assistant)互動時，不支援檔案上傳。

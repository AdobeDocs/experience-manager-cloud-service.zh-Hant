---
title: 內容更新工作
description: 瞭解Brand Experience Agent的內容更新工作是什麼，以及可為您做什麼。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: 71e3770a7a26b8d3144717513f3ec1c997b3b435
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 2%

---


# 內容更新工作 {#content-update}

[Brand Experience Agent](/help/ai-in-aem/agents/brand-experience/overview.md)的內容更新工作會自動執行內容製作，以加速Adobe Experience Manager (AEM) as a Cloud Service和Edge Delivery Services的日常工作。

## 概觀 {#overview}

內容更新工作會更新現有內容，包括內容片段、頁面、表單及資產。 這項工作可以執行更新、移除、取代或新增內容元素等動作，讓體驗保持精確且最新。 輸入可以是自然語言說明，在搭配Jira PDF使用時，熒幕擷取畫面也可以提供輸入。

內容更新工作會將您透過自然語言或視覺效果提供的詳細資料轉換為頁面上的內容更新。 您可以提供需要更新的頁面URL，以及需要更新的詳細資訊，而代理程式技能會完成您的工作。

## 功能 {#capabilities}

您可以從以下位置存取內容更新技能：

* [AI助理](#ai-assistant)
* [Jira](#jira)

## AI 助理 {#ai-assistant}

您可以透過AI助理存取AEM中的工作。

從[`experience.adobe.com`，](https://experience.adobe.com)開啟AI小幫手，然後使用`Ask AI Assistant anything`欄位以自然語言指定提示以開始互動：

![內容更新工作](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### 範例提示 {#sample-prompts}

若要啟動內容更新，您可以提供各種自然語言提示。 您也必須指定要更新之頁面的公開顯示URL。 例如：

* 修改下列頁面`https://www.your-url.com/sale`將主圖示題更新為「黑色星期五特大促銷 — 高達70%折扣」、將倒數計時器變更為「48小時後結束」、移除「註冊更新」、將所有「立即購買」按鈕變更為「搶購優惠」

* `https://www.your-url.com/laptops/your-laptop-model`將橫幅復本更新為「僅今天儲存300美元」，將價格從1,299美元更新為999美元，移除融資選項橫幅

* `https://www.your-url.com/your-sneaker`將庫存狀態從「低庫存」更新為「補貨 — 有限數量」，變更大小選擇器以綠色反白顯示可用大小，移除「即將推出」徽章

* `https://www.your-url.com/your-sneaker`更新產品影像以顯示新色道

>[!NOTE]
>
>使用[Jira](#jira)互動時可以使用檔案上傳，但AI助理不支援此功能。

## Jira {#jira}

搭配Jira使用內容更新工作可讓您建立票證，並附上自動化編輯的指示。

### 建立票證 {#create-a-ticket}

建立Jira票證（任何型別）。 您票證的&#x200B;**描述**&#x200B;欄位中有兩個必要的詳細資料：

1. 您要編輯之頁面的公開顯示URL。

1. 所需的變更。

   此工作支援以下格式範圍，以說明您的變更：

   * 票證說明中的自然語言
      * 例如「將標題從X變更為Y」
   * 附加註解的PDF
      * 例如，建立頁面的PDF，並新增註解，詳細說明您要變更的專案
   * 在附加的PDF中發表評論
      * 例如，建立頁面的PDF，並新增詳述您想要變更專案的註解
   * 附加附註的熒幕擷圖
      * 例如，擷取部分頁面的熒幕擷圖，並新增詳細說明您想要變更專案的註解
   * 附加的Microsoft Word檔案，包含自然語言變更

### 從您的票證叫用工作 {#invoke-the-job-from-your-ticket}

若要使用工作，請在票證中新增註解。 在註解中提及具有`@`符號的工作，以及它應執行的命令；例如：

* `@aemagent@adobe.com process`

目前，工作可瞭解下列命令：

* `process` — 處理要求
* `cancel` — 取消處理請求
* `retry` — 重新處理請求
* `feedback` — 將意見反應套用至上一代
* `reprocess` — 重新處理原始請求

### 工作如何互動 {#how-the-agent-interacts}

您向工作發出命令後，它在Jira中會以評論回應。 註解會詳細說明工作進度，以及所採取的動作。

若是用來觸發更新的`process`命令，回應可能會依照下列順序：

* 初始註解會確認工作已開始。

* 任務完成後，該作業會以另一個註解回應，其中包含所採取動作的詳細資訊。
   * 工作所做的內容更新是非破壞性更新，這表示這些更新會針對預覽執行個體進行。
   * 註解包含更新連結，因此您可以視需要檢閱和發佈，或將Jira指派給負責人員。

* 下圖顯示觸發內容更新工作的`process`命令的Jira範例：

  ![使用Experience Production Agent的內容更新工作的範例Jira](assets/content-update-jira-example.png)

## 啟用 {#activation}

若要啟用並存取通訊建立工作，您需要連絡Adobe。 若要開始使用，您可以：

* 連絡人`experience-production-agent@adobe.com`
* 或聯絡您的帳戶團隊

若要加速此程式，提供下列資訊會有所幫助：

* 針對AEM as a Cloud Service，您需要提供您的：
   * 組織 ID
   * `product_id`
   * `profile_id`

   * 您可以依照以下步驟找到這些值：
      1. 您的管理員需要造訪[`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)
      1. 選取&#x200B;**Adobe Experience Manager as a Cloud Service**
      1. 選取適當的AEM執行個體
      1. 選取允許相關內容讀寫操作的設定檔
      1. 抓取瀏覽器URL
      1. 從URL擷取`product_id`和`profile_id`。
例如 `https://adminconsole.adobe.com/products/profiles/users`

* Edge Delivery檔案製作
   * 為您的Adobe團隊提供下列資訊：
      * 相關網域
      * 相關Github資訊：
         * 組織
         * 存放庫
         * 分支

## 限制 {#limitations}

請留意下列限制:

* 與[Jira](#jira)互動時，可以使用檔案上傳，但是與[AI小幫手互動時，不支援檔案上傳。](#ai-assistant)

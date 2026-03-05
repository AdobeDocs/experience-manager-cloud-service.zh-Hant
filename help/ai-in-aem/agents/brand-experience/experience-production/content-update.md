---
title: 內容更新工作
description: 瞭解Brand Experience Agent的內容更新工作是什麼，以及可為您做什麼。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: baf12e49dadc7b25f5169279a52d5712380445de
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 2%

---


# 內容更新工作 {#content-update}

[Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md)的內容更新工作會自動執行內容生產，以加速Adobe Experience Manager (AEM) as a Cloud Service和Edge Delivery Services的日常工作。

## 概觀 {#overview}

內容更新工作會更新現有內容，包括內容片段、頁面、表單及資產。 這項工作可以執行更新、移除、取代或新增內容元素等動作，讓體驗保持精確且最新。 輸入可以是自然語言說明，在搭配Jira PDF使用時，熒幕擷取畫面也可以提供輸入。

內容更新工作會將您透過自然語言或視覺效果提供的詳細資料轉換為頁面上的內容更新。 您可以提供需要更新的頁面URL，以及需要更新的詳細資訊，而代理程式技能會完成您的工作。 搭配Adobe Experience Manager (AEM) as a Cloud Service使用時，此工作會建立新的[啟動](/help/sites-cloud/authoring/launches/overview.md)，讓您在套用之前可以檢閱更新。 搭配檔案編寫使用時，工作會建立新的[版本](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/sites/document-authoring/how-to/document-versions#)。

## 功能 {#capabilities}

您可以從以下位置存取內容更新技能：

* [AI助理](#ai-assistant)
* [Jira](#jira)

## AI 助理 {#ai-assistant}

您可以透過AI助理存取AEM中的工作。

從[`experience.adobe.com`，](https://experience.adobe.com)開啟AI小幫手，然後使用`Ask AI Assistant anything`欄位以自然語言指定提示以開始互動：

![內容更新工作](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### 設定發佈URL {#configuring-the-publish-url}

若要使用發佈（公開） URL，必須進行一次性設定：

* 先決條件：

   * 要進行設定，使用者必須具有系統管理員或產品管理員許可權。

* 設定：

   1. 請求URL的內容更新以叫用內容更新技能。
   1. 助理會詢問您幾個問題，引導您完成設定。
   1. 完成發佈URL後，即可設定並加以使用。

例如：

![內容更新技能 — 設定發佈URL](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-publish-url-configuration.png)

### 提示 {#prompts}

若要啟動內容更新，您可以提供各種自然語言提示。 您必須指定要更新之頁面的公開（發佈） URL，或作者環境URL。 部分（但非全部）支援的動詞；取代、更新、移除、變更、修訂、修改、調整、刪除。

>[!NOTE]
>
>使用[Jira](#jira)互動時可以使用檔案上傳，但AI助理不支援此功能。

### 範例提示 {#sample-prompts}

範例提示包括：

* 在`<your-publish-URL>`更新時：「您的完美咖啡還有四個問題！」 「您的咖啡，您的方式！」
* 在`<your-author-env-URL>`上，將影像從&quot;holdingcup.png&quot;取代為&quot;stairhead.png&quot;
* 在`<your-publish-URL>`上將「參加我們的咖啡測驗」按鈕變更為更吸引人的版本
* 在`<your-author-env-URL>`上移除「未認領的獎勵是已遺漏的禮物！」區段

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

若要使用工作，請在票證中新增註解。 在註解中，提及具有`@`符號的工作，以及指示。

例如：

* `@aemagent@adobe.com process this ticket`

### 工作如何互動 {#how-the-agent-interacts}

您向工作發出命令後，它在Jira中會以評論回應。 註解會詳細說明工作進度，以及所採取的動作。

若是用來觸發更新的`process`命令，回應可能會依照下列順序：

* 初始註解會確認工作已開始。

* 任務完成後，該作業會以另一個註解回應，其中包含所採取動作的詳細資訊。
   * 工作所做的內容更新是非破壞性更新，這表示這些更新會針對預覽執行個體進行。
   * 註解包含更新連結，因此您可以視需要檢閱和發佈，或將Jira指派給負責人員。

* 下圖顯示觸發內容更新工作的`process`命令的Jira範例：

  ![使用Brand Experience Agent的內容更新工作的範例Jira](assets/content-update-jira-example.png)

## 啟用 {#activation}

您可以透過[遊樂場](https://www.aem.live/developer/aem-playground)探索AEM代理程式，或連絡您的CSM或TAM，討論透過Agentic SKU的存取權。

## 限制 {#limitations}

請留意下列限制:

* 與[Jira](#jira)互動時，可以使用檔案上傳，但是與[AI小幫手互動時，不支援檔案上傳。](#ai-assistant)

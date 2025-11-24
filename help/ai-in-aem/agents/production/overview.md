---
title: Experience Production Agent概述
description: 瞭解AEM中的Experience Production Agent如何協助您加速內容建立並自動協調變更。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8cd524891df550913a734a9355c1012dc11adf5b
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 3%

---


# Experience Production Agent概述 {#experience-production-agent}

Experience Production Agent可自動處理大量及大量工作。 強化團隊，將長達數週的手動流程轉換為快速的AI輔助工作流程，讓每個體驗保持最新且一致，以協助企業達成目標。

## 工作 {#jobs}

代理程式提供下列工作：

* [內容更新](#content-update)
* [表單建立](#form-creation)
* [建立通訊](#communications-creation)
* [網站移轉](#site-migration)

>[!IMPORTANT]
>
>AI產生的回應可能不準確或誤導。 請務必仔細檢查建議的修正和回應。
>
>另請參閱[Adobe Experience Cloud Generative AI使用者指南](https://www.adobe.com/tw/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)。

### 內容更新 {#content-update}

[內容更新](/help/ai-in-aem/agents/production/content-update.md)可輕鬆更新整個CMS的現有內容，包括內容片段、頁面、表單及資產。 代理程式可以執行更新、移除、取代或新增內容元素等動作，以保持體驗精確且最新。 輸入可以是自然語言說明，在搭配Jira PDF使用時，熒幕擷取畫面也可以提供輸入。

### 表單建立 {#form-creation}

[表單建立](/help/ai-in-aem/agents/production/form-creation.md)技能可讓使用者透過自然語言提示建立最適化表單，而不需依賴開發或IT團隊。 此功能可加快表單開發，同時維持品牌一致性，讓業務使用者無須深入瞭解技術產品即可建立表單。

### 建立通訊 {#communications-creation}

[通訊建立](/help/ai-in-aem/agents/production/communications-creation.md)技能可讓商務使用者大規模產生個人化、資料導向的通訊。 從帳戶對帳單和政策檔案，到帳單和歡迎套件，代理商將自然語言需求轉換為專業通訊。

>[!NOTE]
>
> 「通訊建立」技能目前為Alpha版。 如果您想要參與，請將您的正式電子郵件地址傳送至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)。

### 網站移轉 {#site-migration}

[網站移轉](/help/ai-in-aem/agents/production/site-migration.md)將非AEM網站順暢地移轉到AEM (Experience Delivery Services)環境，確保它們符合效能規範，且可供代理程式使用。 此代理程式可簡化設定和轉換，減少手動工作量和實現價值的時間。

代理程式應能使用其他代理程式技能，範例包括：

## 搭配其他代理程式使用 {#use-with-other-agents}

* 從Experience Advisory代理程式取得來源資產

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

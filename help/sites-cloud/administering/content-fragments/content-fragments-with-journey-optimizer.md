---
title: 搭配Adobe Journey Optimizer使用內容片段
description: 瞭解如何將內容片段整合併與Adobe Journey Optimizer搭配使用。
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
exl-id: 4090ee41-80f1-4389-8961-e4af891f01ff
source-git-commit: 0fd7b2633488ceb14d34b1978a91a3a830d8762a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 10%

---

# 使用 Adobe Journey Optimizer 的內容片段 {#content-fragments-with-journey-optimizer}

[Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/get-started/get-started)可協助您為客戶提供連結、情境式和個人化的體驗。 透過整合Adobe Experience Manager (AEM) as a Cloud Service與Adobe Journey Optimizer (AJO)，您可以在AJO傳入頻道和AJO傳出頻道（包括網頁、簡訊、電子郵件等）中重複使用AEM內容。

例如，您可以：

* 將您的[AEM內容片段](/help/sites-cloud/administering/content-fragments/overview.md)緊密整合至您的[Journey Optimizer電子郵件](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/channels/email/email-landing-page)內容
* 直接從AEM預覽AJO體驗

內容片段和AJO之間的連線可簡化存取及運用AEM內容的程式，讓您建立個人化和動態的行銷活動和歷程。

如需詳細資訊，請從AJO檔案開始：

* [在AJO中使用內容片段](https://experienceleague.adobe.com/docs/journey-optimizer/using/integrations/aem-fragments.html?lang=zh-Hant#integrations)
* [整合AJO選件與內容片段](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/decisioning/offer-decisioning/managing-offers-in-the-offer-library/configure-offers/add-representations#urls)

## Dispatcher 設定 {#dispatcher-configuration}

若要允許AJO透過[內容片段管理API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)存取AEM內容片段，您需要設定Dispatcher：

* 在`dispatcher/src/conf.dispatcher.d/filters/filters.any`：

* 新增：

  ```xml
  # Allow Content Fragments API requests, required for integration with AJO 
  /200 {/type "allow" /url "/adobe/sites/cf/*" }
  ```

## 更多資訊 {#further-information}

如需進一步詳細資訊，請參閱：

* [AJO外部參考擴充功能](/help/sites-cloud/administering/content-fragments/extension-content-fragment-ajo-external-references.md)

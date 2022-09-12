---
title: 轉譯多語言網站的內容
description: 概略了解如何翻譯多語言網站的內容。
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 轉譯多語言網站的內容 {#translating-content-for-multilingual-sites}

自動翻譯頁面內容和資產，以建立和維護多語言網站。 為了自動化翻譯工作流，您將翻譯服務提供商與AEM整合，並建立項目以將內容翻譯成多種語言。 AEM支援人工和機器翻譯工作流程。

* **人類翻譯：** 內容將發送給翻譯提供商，並由專業翻譯人員翻譯。 完成時，會傳回翻譯的內容並匯入AEM。 當您的翻譯提供者與AEM整合時，內容會自動在AEM和翻譯提供者之間傳送。
* **機器翻譯：** 機器翻譯服務會立即翻譯您的內容。

>[!TIP]
>
>如果您是初次翻譯內容，請參閱 [網站翻譯歷程，](/help/journey-sites/translation/overview.md) 這是使用AEM功能強大的翻譯工具來轉譯您的AEM Sites內容的引導式路徑，最適合沒有AEM或翻譯體驗的人。

轉譯內容涉及下列步驟：

1. [將AEM與您的翻譯服務提供商連接](integration-framework.md#connecting-to-a-translation-service-provider) 和 [建立翻譯整合框架配置](integration-framework.md).
1. [關聯語言主版的頁面](integration-framework.md#configuring-pages-for-translation) 和框架配置。
1. [識別內容類型](rules.md) 翻譯。
1. [準備翻譯內容](preparation.md) 編寫語言主版並建立語言副本的根頁面。
1. [建立翻譯專案](managing-projects.md) 收集要翻譯的內容並準備翻譯程式。
1. 使用翻譯專案 [管理內容翻譯流程](managing-projects.md).

如果您的翻譯服務提供者未提供與AEM整合的連接器，AEM支援以XML格式手動擷取和重新插入翻譯內容。

>[!NOTE]
>
>您的使用者必須是 `project-administrators` 群組以使用語言副本功能。

## 最佳作法 {#best-practices}

此 [翻譯最佳實務](best-practices.md) 頁面包含與您的實作相關的重要資訊。

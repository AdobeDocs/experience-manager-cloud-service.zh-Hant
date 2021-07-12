---
title: 轉譯多語言網站的內容
description: 概略了解如何翻譯多語言網站的內容。
feature: 語言副本
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# 轉譯多語言網站的內容 {#translating-content-for-multilingual-sites}

自動翻譯頁面內容和資產，以建立和維護多語言網站。 為了自動化翻譯工作流，您將翻譯服務提供商與AEM整合，並建立項目以將內容翻譯成多種語言。 AEM支援人工和機器翻譯工作流程。

* **人工翻譯：** 內容會傳送給您的翻譯提供者，並由專業翻譯人員翻譯。完成時，會傳回翻譯的內容並匯入AEM。 當您的翻譯提供者與AEM整合時，內容會自動在AEM和翻譯提供者之間傳送。
* **機器翻譯：** 機器翻譯服務會立即翻譯您的內容。

轉譯內容涉及下列步驟：

1. [將AEM與您的翻譯服務提供](integration-framework.md#connecting-to-a-translation-service-provider) 商連 [接，並建立翻譯整合架構設定](integration-framework.md)。
1. [將您語言首頁與翻](integration-framework.md#configuring-pages-for-translation) 譯服務和框架配置相關聯。
1. [識別要翻譯的](rules.md) 內容類型。
1. [編寫語言主版](preparation.md) 並建立語言副本的根頁面，以準備翻譯內容。
1. [建立翻](managing-projects.md) 譯專案以收集要翻譯的內容並準備翻譯程式。
1. 使用翻譯專案至[管理內容翻譯程式](managing-projects.md)。

如果您的翻譯服務提供者未提供與AEM整合的連接器，AEM支援以XML格式手動擷取和重新插入翻譯內容。

>[!NOTE]
>
>您的用戶必須是`project-administrators`組的成員才能使用語言副本功能。

## 最佳作法 {#best-practices}

[翻譯最佳實務](best-practices.md)頁面包含有關您實作的重要資訊。

---
title: 翻譯多語言網站的內容
description: 大致了解如何翻譯多語言網站的內容。
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 82%

---

# 翻譯多語言網站的內容 {#translating-content-for-multilingual-sites}

自動翻譯頁面內容和資產以建立和維護多語言網站。若要自動化翻譯工作流程，您可以將翻譯服務提供商與 AEM 相整合，並建立用於將內容翻譯成多種語言的專案。AEM 支援人工和機器翻譯工作流程。

* **人工翻譯：**&#x200B;內容將傳送給您的翻譯提供商並由專業翻譯人員翻譯。完成後，翻譯後的內容將傳回並匯入到 AEM 中。如果您的翻譯提供商與 AEM 相整合，內容會在 AEM 和翻譯提供商之間自動傳送。
* **機器翻譯：**&#x200B;機器翻譯服務會立即翻譯您的內容。

>[!TIP]
>
>如果不熟悉如何翻譯內容，請參閱[網站翻譯歷程](/help/journey-sites/translation/overview.md)，此歷程將引導您使用AEM強大的翻譯工具來翻譯您的AEM Sites內容，非常適合沒有AEM或翻譯經驗的人士。

翻譯內容涉及以下步驟：

1. [將 AEM 與您的翻譯服務提供商連接](integration-framework.md#connecting-to-a-translation-service-provider)並[建立翻譯整合框架設定](integration-framework.md)。
1. [將您語言主版的頁面](integration-framework.md#configuring-pages-for-translation) 與翻譯服務和框架設定相關聯。
1. [識別要翻譯的內容類型](rules.md)。
1. 編寫語言主版並建立語言副本的根頁面，[以備妥內容進行翻譯](preparation.md)。
1. [建立翻譯專案](managing-projects.md)以收集要翻譯的內容並準備翻譯流程。
1. 使用翻譯專案[管理內容翻譯流程](managing-projects.md)。

如果您的翻譯服務提供商不提供連接器以與 AEM 整合，AEM 支援手動擷取和重新插入 XML 格式的翻譯內容。

>[!NOTE]
>
>您的使用者必須是`project-administrators`群組的成員才能使用語言副本功能。

## 最佳做法 {#best-practices}

[翻譯最佳做法](best-practices.md)頁面包含與您的實作相關的重要資訊。

---
title: 翻譯多語言網站的內容
description: 概略瞭解如何翻譯多語言網站的內容。
feature: 語言副本
role: 管理員
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 1%

---


# 翻譯多語言網站的內容{#translating-content-for-multilingual-sites}

自動化頁面內容與資產的翻譯，以建立和維護多語言網站。 為自動化翻譯工作流程，您將翻譯服務提供商與AEM建立項目，以便將內容翻譯成多種語言。 AEM支援人文和機器翻譯工作流程。

* **人文翻譯：** 內容會傳送給翻譯提供者，並由專業翻譯人員翻譯。完成時，會傳回翻譯的內容並匯入至AEM。 當翻譯提供者與之整合時AEM，內容會自動在翻譯提供AEM者與之間傳送。
* **機器翻譯：** 機器翻譯服務可立即翻譯您的內容。

翻譯內容需要執行下列步驟：

1. [與您的AEM翻譯服務提供商](integration-framework.md#connecting-to-a-translation-service-provider) 聯繫並 [建立翻譯整合框架配置](integration-framework.md)。
1. [將您語言的首頁與翻](integration-framework.md#configuring-pages-for-translation) 譯服務和框架配置相關聯。
1. [識別要翻譯的](rules.md) 內容類型。
1. [編寫語言主版](preparation.md) 並建立語言副本的根頁面，以準備翻譯內容。
1. [建立轉](managing-projects.md) 譯專案以收集要翻譯的內容並準備轉譯程式。
1. 使用翻譯項目到[管理內容翻譯流程](managing-projects.md)。

如果您的翻譯服務提供商未提供與整合的連接器AEM,AEM則支援以XML格式手動提取和重新插入翻譯內容。

>[!NOTE]
>
>您的使用者必須是`project-administrators`群組的成員，才能使用「語言複製」功能。

## 最佳作法 {#best-practices}

[翻譯最佳實踐](best-practices.md)頁包含有關您實施的重要資訊。

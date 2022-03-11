---
title: 翻譯多語言站點的內容
description: 獲取如何翻譯多語言站點內容的概述。
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 翻譯多語言站點的內容 {#translating-content-for-multilingual-sites}

自動翻譯頁面內容和資產以建立和維護多語言網站。 要自動化翻譯工作流，您可以將翻譯服務提供商與AEM整合，並建立項目，將內容翻譯成多種語言。 支AEM持人和機器翻譯工作流。

* **人文翻譯：** 內容將發送給您的翻譯提供商，並由專業翻譯員翻譯。 完成後，將返回已翻譯的內容並導入AEM。 當翻譯提供商與之整合AEM時，內容將自動在翻譯提供AEM商之間發送。
* **機器翻譯：** 機器翻譯服務會立即翻譯您的內容。

>[!TIP]
>
>如果您是翻譯內容的新手，請參閱我們的 [網站翻譯之旅，](/help/journey-sites/translation/overview.md) 它是指通過使用功能強大的翻譯工具AEM翻譯您的AEM Sites內容的指導路AEM徑，是那些沒有翻譯經驗的人的理想選擇。

翻譯內容涉及以下步驟：

1. [與翻譯AEM服務提供商連接](integration-framework.md#connecting-to-a-translation-service-provider) 和 [建立翻譯整合框架配置](integration-framework.md)。
1. [關聯您的語言母版頁](integration-framework.md#configuring-pages-for-translation) 翻譯服務和框架配置。
1. [確定內容類型](rules.md) 翻譯。
1. [準備翻譯內容](preparation.md) 通過建立語言首頁和建立語言副本的根頁。
1. [建立翻譯項目](managing-projects.md) 收集要翻譯的內容並準備翻譯過程。
1. 使用翻譯項目 [管理內容翻譯流程](managing-projects.md)。

如果您的翻譯服務提供商未提供與整合的連接AEM器AEM，則支援以XML格式手動提取和重新插入翻譯內容。

>[!NOTE]
>
>您的用戶需要是 `project-administrators` 組以使用「語言複製」功能。

## 最佳作法 {#best-practices}

的 [翻譯最佳做法](best-practices.md) 頁面包含有關您的實施的重要資訊。

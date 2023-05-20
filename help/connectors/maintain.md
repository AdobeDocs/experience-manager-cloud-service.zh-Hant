---
title: 維護 AEM 連接器
description: 維護 AEM 連接器
exl-id: 8122a8c8-6577-4907-8f6e-52711eed3970
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 20%

---

維護 AEM 連接器
============================

本文包含有關維護AEM Connector的資訊，並應與實作與送出連接器的相關文章一 [起](implement.md)[閱讀](submit.md) 。

即使在初始提交後，合作夥伴也可能有理由更新其AEMConnector，這可能是由於新版本AEM或獨立於該版本，例如添加功能或修復錯誤。 本文概述了兩種情形的流程，並介紹了客戶在升級時驗證連接器的典型流AEM程。

每AEM天用維護補AEM丁程式更新as a Cloud Service應用程式，在功能發佈期間每月激活更大的更改。 儘管AEM更新旨在向後相容，因此不會中斷應用程式，但建議供應商合作夥伴定期驗證其連接器是否像預期的那樣工作。 對計畫AEM/環境的訪問將由合作夥伴團隊決定。

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

即使在初次提交後，合作夥伴仍可能因AEM的新版本或獨立於該版本（例如新增功能或修正錯誤）而更新其AEM Connector，這是有原因的。 本文概述兩種情況的程式，並說明客戶在升級AEM時驗證連接器的典型程式。

AEMas a Cloud Service應用程式會每天更新為AEM維護修補程式，在功能發行期間會每月啟動更大的變更。 雖然AEM更新旨在向後相容，因此不會中斷應用程式，但建議廠商合作夥伴定期驗證其連接器是否如預期般運作。 對AEM計畫/環境的存取將由合作夥伴團隊決定。

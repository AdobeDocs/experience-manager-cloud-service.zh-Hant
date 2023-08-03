---
title: 維護 AEM 連接器
description: 瞭解如何在初次提交後維護和更新AEM聯結器。
exl-id: 8122a8c8-6577-4907-8f6e-52711eed3970
source-git-commit: 5482e94bc1a2e7524eb699f2ae766ba40c138e91
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 17%

---

維護 AEM 連接器
============================

本文包含有關維護AEM Connector的資訊，並應與實作與送出連接器的相關文章一 [起](implement.md)[閱讀](submit.md) 。

即使在初次提交後，合作夥伴也可能有理由更新其AEM聯結器，可能是因為AEM的新版本或與此無關 — 例如，新增功能或修正錯誤。 本文會概述這兩種情況的程式，並說明客戶在升級AEM時驗證聯結器的典型程式。

AEMas a Cloud Service應用程式每天都會使用AEM維護修補程式進行更新，在功能發行期間每月會啟動大量變更。 雖然AEM更新旨在回溯相容，因此不會破壞應用程式，但建議廠商合作夥伴定期驗證其聯結器的行為是否符合預期。 對AEM方案/環境的存取權由合作夥伴團隊決定。

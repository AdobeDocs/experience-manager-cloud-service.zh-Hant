---
title: 維護 AEM 連接器
description: 維護 AEM 連接器
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 20%

---


維護 AEM 連接器
============================

本文包含有關維護AEM Connector的資訊，並應與實作與送出連接器的相關文章一 [起](implement.md)[閱讀](submit.md) 。

即使在初次提交後，合作夥伴仍有理由更新其AEM Connector，因為AEM已推出新版本或獨立於此版本——例如新增功能或修正錯誤。 本文概述這兩種情況的程式，並說明客戶在升級AEM時驗證連接器的典型程式。

AEM做為雲端服務應用程式，每天都會以AEM維護修補程式更新，在功能發行期間，每月會啟用較大的變更。 雖然AEM更新旨在向後相容，因此不會中斷應用程式，但建議廠商合作夥伴定期驗證其連接器是否如預期般運作。 AEM計畫／環境的存取權將由合作夥伴團隊決定。
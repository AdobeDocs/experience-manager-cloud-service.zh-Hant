---
title: '生產計畫簡介 '
description: 生產計畫簡介
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# 生產計畫簡介 {#production-programs}

*Production*&#x200B;程式適用於熟悉AEM和Cloud Manager且準備好開始編寫、建立和測試程式碼，以將程式碼部署至生產環境的使用者。

>[!NOTE]
>您將無法刪除生產程式。

方案建立嚮導將根據用戶建立方案的目標引導用戶進行選擇。 根據特定客戶或組織可用的未使用解決方案權益，使用者可控制如何將可用（未使用）的解決方案權益對應至Cloud Manager計畫。

## 程式建立考量事項 {#program-creation-considerations}

下表說明在Cloud Manager中建立程式時要考慮的常見案例：

| 組織中可用的未使用解決方案權益 | 建立方案選項 | 包含的項目 | 使用時機和其他考量事項 |
|--- |--- |--- |--- |
| 1個站點解決方案 | 僅建立1個站點程式 | 1生產+1階段，1開發 | 不適用 |
| 1個Assets解決方案 | 僅建立1個資產方案 | 1生產+1階段，1開發 | 不適用 |
| 1個網站+1個資產 | 建立一個方案：1個網站與資產計畫 | 1生產+1階段，2開發 | 大部分的數位資產都用於支援網站實作。 大部分的數位資產都處於完成狀態，可供透過Sites用於跨管道體驗。通常，單一團隊負責管理Sites和Assets的內容。 **常見範例**:主要用於網站的影像。PDF將透過內建於AEM Sites的內部入口網站發佈。 |
| 1個網站+1個資產 | 建立單獨的程式：1個僅站點計畫和1個僅資產計畫 | 1生產+1級，1開發<br> 1生產+1級，1開發 | 許多數位資產不直接支援網站實作。 管理的資產處於多種狀態，包括原始檔案類型和進行中的工作。 專屬的創意團隊會透過自己的生命週期管理數位資產，且與Sites內容管理團隊相比，有不同的工作流程和發行週期。 *常見範例*:來自像片的原始影像會儲存在Assets程式中，而Sites實作中只會使用少數幾張。大量Creative Cloud檔案類型(例如Photoshop和Illustrator)會在AEM Assets中進行管理，並在產生完成的資產前先執行其自己的核准工作流程。 要利用的功能：[連線資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html?lang=en#overview-of-connected-assets) |
| 1個站點+ 1個站點 | 建立單獨的程式：1個僅站點計畫1個僅站點計畫 | 1生產+1級，1開發<br>1生產+1級，1開發 | 多租用戶網站實施。 有多個網站及其專屬的發行排程和開發與內容團隊。 *常見範例*:兩個零售品牌，有專屬網站和不同的開發團隊 |

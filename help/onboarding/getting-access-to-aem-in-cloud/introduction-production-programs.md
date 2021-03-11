---
title: '生產計畫簡介 '
description: '生產計畫簡介 '
translation-type: tm+mt
source-git-commit: aa42ccf73a6be9050a06f9cbea0d16b80b039d89
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---


# 生產程式簡介{#production-programs}

*Production*&#x200B;程式是專為熟悉和Cloud Manager並準備開始編寫、建立和測試程式碼的使用者而設計，其目的是將程式碼部署至「生產」。

>[!NOTE]
>您將無法刪除生產程式。

程式建立精靈會根據使用者建立程式的目標，引導使用者進行選擇。 根據特定客戶或組織可用的未使用解決方案權益，用戶可以控制如何將可用（未使用）解決方案權益映射到Cloud Manager程式。

## 程式建立注意事項{#program-creation-considerations}

下表說明在Cloud Manager中建立程式時要考慮的常見情況：

| 組織中可用的未使用的解決方案權利 | 建立方案選項 | 包含的項目 | 使用時機和其他考量事項 |
|--- |--- |--- |--- |
| 1個網站解決方案 | 僅建立1個網站計畫 | 1個生產+ 1個階段，1個開發 | 不適用 |
| 1個站點+ 1個站點 | 建立個別的程式：1個僅限網站計畫和1個僅限網站計畫 | 1個生產+ 1個階段，1個開發1個生產+ 1個階段，1個開發 | 多租用戶網站實作。 多個網站擁有其專屬的發行排程和專屬的開發與內容團隊。 *常見範例*:兩個零售品牌設有專屬網站和獨立的開發團隊 |
| 1個網站+1個資產 | 建立一個方案：1個網站與資產計畫 | 1個生產+ 1個階段， 2個開發 | 大部份的數位資產都用於支援網站實作。 大部分數位資產都處於完成狀態，可供透過網站進行跨通道體驗。通常，單一團隊負責管理網站和資產的內容。 *常見範例*:主要用於網站的影像。將透過內建於AEM Sites的內部入口網站發佈的PDF。 |
| 1個網站+1個資產 | 建立個別的程式：1個僅限網站計畫和1個僅限資產計畫 | 1個生產+ 1個階段，1個開發1個生產+ 1個階段，1個開發 | 許多數位資產並不直接支援網站實作。 管理的資產處於各種狀態，包括原始檔案類型和進行中的工作。 專屬的創意團隊透過其專屬的生命週期管理數位資產，與Sites內容管理團隊相比，其工作流程和發行週期也不同。 *常見範例*:來自像片的原始影像會儲存在Assets程式中，而Sites實作中只會使用少數影像。許多Creative Cloud檔案類型(例如Photoshop和Illustrator)都在AEM Assets進行管理，並在產生完成的資產之前，先執行其核准工作流程。 可運用的功能：[連接的資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html?lang=en#overview-of-connected-assets) |
| 1個資產解決方案 | 僅建立1個資產方案 | 1個生產+ 1個階段，1個開發 | 不適用 |



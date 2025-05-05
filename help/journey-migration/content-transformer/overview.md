---
title: 內容轉換器概觀
description: 瞭解如何使用內容轉換器來偵測並修正BPA回報的內容相關問題。
exl-id: aa3397ff-3dd6-4c67-9064-cb9b19bf1c73
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# 概觀 {#overview-ct}

Content Transformer (CT)是由Adobe開發的工具，在將內容從您目前的AEM實作(內部部署或Managed Services)移轉至AEM as a Cloud Service之前，可用來自動偵測和修正[最佳實務分析器(BPA)](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)所回報的內容相關問題。

內容轉換器可以允許使用者執行大量動作，例如移動或刪除，以協助解決屬於下列[BPA模式類別](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=zh-Hant) （如下表所示）的問題。 這可大幅減少與移轉專案相關的時間並降低複雜性。

## 內容轉換器涵蓋的模式類別和建議的解決方案 {#pattern-categories-and-benefits}

| 圖樣代碼 | 懷疑型別/子型別 | 將內容移轉至AEM as a Cloud Service之前的潛在修正 |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendants.violation | 將這些資產移至其他位置或予以刪除，以確保其未移轉至AEM as a Cloud Service。 |
| CAV | content.area.violation | 將路徑暫時移至`/etc/packages/content-transformation/paths`以確保它們未移轉至AEM as a Cloud Service。 |
| DOPI | deprecated.ordered.index | 移除已棄用的索引。 |
| OAUI | non.migrated.oauth.users | 請移除這些使用者，以確保他們不會移轉至AEM as a Cloud Service。 |
| PCX | page.complexity.medium <br> page.complexity.high | 請刪除頁面/子項，或將其移至其他位置，以確保其不會移轉至AEM as a Cloud Service。 |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modification <br> custom.replication.agent.detection | 移除已建立的復寫代理。 <br>或<br>移除修改/新增的屬性。 |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | 移至正確位置，以避免移轉期間發生問題。 |
| URS | node.size | 將節點暫時移至`/etc/packages/content-transformation/paths`，確保它們未移轉至AEM as a Cloud Service。 |

## 內容轉換工具提供的優點 {#benefits}

內容轉換器提供下列優點：

* 防失敗：內容轉換器每次對存放庫進行修改以修正問題時，都會建立套件。 如有需要，您可以安裝套件以還原成先前的狀態。
* 使用方便： Content Transformer已與Content Transfer Tool整合，並提供直覺式的簡單使用者介面。
* 節省時間：當大量內容問題屬於一個模式類別時，您可以使用內容轉換器按幾下即可解決所有問題。

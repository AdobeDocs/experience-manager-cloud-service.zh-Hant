---
title: 內容轉換工具概觀
description: 內容轉換工具概觀
source-git-commit: 55eedd342f048e19bad5c6fbfdd16a468ff1f4f9
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 2%

---

# 概觀 {#overview-ct}

Content Transformer (CT)是由Adobe開發的工具，可用於自動偵測和修正由下列使用者報告的內容相關問題： [Best Practices Analyzer (BPA)](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 將內容從您目前的AEM實作(內部部署或Managed Services)移轉至AEMas a Cloud Service之前。

內容轉換器可以協助解決以下問題 [BPA模式類別](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html) （如下表所示），讓使用者能夠執行大量動作，例如移動或刪除。 這可大幅減少與移轉專案相關的時間並降低複雜性。

## 內容轉換器涵蓋的模式類別和建議的解決方案 {#pattern-categories-and-benefits}

| 圖樣代碼 | 懷疑型別/子型別 | 將內容移轉至AEMas a Cloud Service之前的潛在修正 |
|--------------|--------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| ACV | missing.jcrcontent <br> missing.original.rendition <br> metadata.descendants.violation | 將這些資產移至其他位置或加以刪除，以確保其不會移轉至AEMas a Cloud Service。 |
| CAV | content.area.violation | 將路徑暫時移動到 `/etc/packages/content-transformation/paths` 以確保這些檔案不會移轉至AEMas a Cloud Service。 |
| DOPI | deprecated.ordered.index | 移除已棄用的索引。 |
| OAUI | non.migrated.oauth.users | 請移除這些使用者，以確保他們不會移轉至AEMas a Cloud Service。 |
| PCX | page.complexity.medium <br> page.complexity.high | 刪除頁面/子系，或將其移至其他位置，以確保其不會移轉至AEMas a Cloud Service。 |
| REP | forward.replication <br> reverse.replication <br> standard.replication.agent.modification <br> custom.replication.agent.detection | 移除新建立的復寫代理。 <br> 或 <br> 移除修改/新增的屬性。 |
| URS | clientlibs.location <br> file.location <br> node.location <br> workflow.location | 移至正確位置，以避免移轉期間發生問題。 |
| URS | node.size | 將節點暫時移至`/etc/packages/content-transformation/paths` 以確保這些檔案不會移轉至AEMas a Cloud Service。 |

## 內容轉換工具提供的優點 {#benefits}

內容轉換器提供下列優點：

* 防故障：內容轉換器每次對存放庫進行修改以修復問題時，都會建立套件。 如有需要，您可以安裝套件以回覆成先前的狀態。
* 易於使用： Content Transformer已與Content Transfer Tool整合，並提供直覺式的簡單使用者介面。
* 節省時間：當大量內容問題屬於一個模式類別時，只要按幾下即可使用內容轉換器解決所有問題。

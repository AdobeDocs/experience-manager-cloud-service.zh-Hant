---
title: 使用Cloud Readiness Analyzer
description: 使用Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: f0e69dba5d670d141c82e762069f4831c2527dbe
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# 使用Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## 使用Cloud Readiness Analyzer的重要注意事項 {#imp-considerations}

請依照以下章節瞭解運行雲就緒性分析器(CRA)時的重要考慮事項：

* CRA支援6.1版及更新版本的來源AEM例項
* CRA可在任何環境(最好是 *Stage* )上執行

   >[!NOTE]
   >為了提高偵測率並避免商業關鍵例項的速度變慢，建議在自訂、設定、內容和使用者應用程式方面盡可能接近生產環境的來源作者測試環境上執行CRA。 或者，它也可以在 *Publish環境的仿製程式上* 執行。

## 可用性 {#availability}

Cloud Readiness Analyzer可從軟體分發門戶下載為zip檔案。 您可以透過Package Manager在來源Adobe Experience Manager(AEM)例項上安裝套件。

>[!NOTE]
>從待定的軟體分發門戶下載Cloud Readiness Analyzer **。

## 運行Cloud Readiness Analyzer {#running-tool}

請依照本節內容瞭解如何運行Cloud Readiness Analyzer:

1. 選擇Adobe Experience Manager並導覽至工具-> **Operations** -> **Cloud Readiness Analyzer**。

   ![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. 按一下「 **Cloud Readiness Analyzer**」後，工具就會開始產生報表，幾分鐘後您就會看到產生的報表。

   >[!NOTE]
   >您必須向下捲動頁面才能檢視完整報表。

   ![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### 在摘要報表中檢視結果 {#viewing-the-results}

>[!IMPORTANT]
>從Cloud Readiness Analyzer生成的報告基於模式檢測器。 如需詳細 [資訊，請參閱](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) 「圖樣偵測器」。

向下捲動頁面以檢視完整摘要報表後，您可以看到報表中反白顯示的每個類別的下列資訊：

1. **重要性級別**

   下表說明了各種模式檢測器和雲就緒性分析器重要性級別的含義。

   | 重要性級別 | 說明 |
   |--- |--- |
   | INFO/0 | 此查找結果僅供參考。 |
   | 建議/1 | 這個發現可能是升級問題。 建議進一步調查。 |
   | 主修/2 | 這項發現可能是需要解決的升級問題。 |
   | 緊急/3 | 此發現很可能是升級問題，必須解決以防功能或效能遺失。 |

1. **說明**&#x200B;說明提供報告類別的相關資訊。

1. **文檔URL**&#x200B;文檔URL允許您查看相關類型的技術文檔。

1. **訊息**：單一訊息中尋找結果的說明。

### 以CSV格式檢視結果 {#viewing-the-results-csv}

摘要報表可在AEM使用者介面中使用。 您可以以逗號分隔值(CSV)格式下載完整報表，在重構程式中會有所幫助。

請依照下列步驟，產生摘要報表的CSV格式：

1. 
   1. 選擇Adobe Experience Manager並導覽至工具-> **Operations** -> **Cloud Readiness Analyzer**。

1. 產生報表後，按一下 **CSV** ，以逗號分隔值(CSV)格式下載完整的摘要報表，如下圖所示。

![影像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)


#### 在AEM 6.1例項中檢視報表 {#aem-instances-report}

您可以下載AEM 6.1的csv報表。此為擱置中。


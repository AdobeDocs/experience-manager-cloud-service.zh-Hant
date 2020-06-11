---
title: 使用Cloud Readiness Analyzer
description: 使用Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 47773a56f8bb24342281068a8c4d03d6edfb9277
workflow-type: tm+mt
source-wordcount: '390'
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

### 查看結果 {#viewing-the-results}

>[!IMPORTANT]
>從Cloud Readiness Analyzer生成的報告基於模式檢測器。 如需詳細 [資訊，請參閱](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) 「圖樣偵測器」。

查看Cloud Readiness Analyzer輸出的方法有兩種：

1. **使用有組織的報表**

   >[!NOTE]
   >AEM 6.3版及更新版本提供有組織的報表。

   或,

1. **查看CRA的輸出**

   請遵循以下步驟查看Cloud Readiness Analyzer的輸出：

   >[!NOTE]
   >下列步驟適用於AEM 6.1版及更高版本。

   1. 使用導 **覽至AEM Web Console**`https://serveraddress:serverport/system/console/configMgr`。

   1. 選擇 **狀態——模式檢測器** ，如下圖所示。

#### 在AEM 6.1例項中檢視報表 {#aem-instances-report}

您可以下載AEM 6.1的csv報表。此為擱置中。

#### 瞭解報表中的重要性級別 {#importance-levels}

下表說明了各種模式檢測器和雲就緒性分析器重要性級別的含義。

| 重要性級別 | 說明 |
|--- |--- |
| INFO/0 | 此查找結果僅供參考。 |
| 建議/1 | 這個發現可能是升級問題。 建議進一步調查。 |
| 主修/2 | 這項發現可能是需要解決的升級問題。 |
| 緊急/3 | 此發現很可能是升級問題，必須解決以防功能或效能遺失。 |
---
title: 使用Cloud Readiness Analyzer
description: 使用Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 3d818278c53f3d3b4c5b53aa5b78d06d876bf05f
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# 使用Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## 使用Cloud Readiness Analyzer的重要注意事項 {#imp-considerations}

請依照以下章節瞭解運行雲就緒性分析器(CRA)時的重要考慮事項：

* CRA支援6.1版及更新版本的來源AEM例項。
* CRA可以在任何環境下運作。

   >[!NOTE]
   >為了提高偵測率並避免商業關鍵例項的速度變慢，建議在自訂、設定、內容和使用者應用程式方面盡可能接近生產環境的來源作者測試環境上執行CRA。 或者，也可以在發佈環境的克隆上運行。

## 可用性 {#availability}

Cloud Readiness Analyzer(CRA)可從軟體散發入口網站下載為zip檔案。 您可以透過Package Manager在來源Adobe Experience Manager(AEM)例項上安裝套件。

>[!NOTE]
>從擱置中下載Cloud Readiness Analyzer(CRA) **。

## 運行Cloud Readiness Analyzer {#running-tool}

請依照本節內容瞭解如何運行Cloud Readiness Analyzer:

1. 選擇Adobe Experience Manager並導覽至工具-> **Operations** -> **Cloud Readiness Analyzer**。

### 查看結果 {#viewing-the-results}

有兩種方法可以看到CRA的產出：

1. 使用有組織的報表

   >[!NOTE]
   >AEM 6.3版及更新版本提供有組織的報表。

請參閱CRA檔案規劃與狀態，以說明報告中的重要性等級

1. 檢視CRA的輸出（可與AEM 6.1及更新版本搭配使用）:

   1. 瀏覽至，以導覽至AEM Web Console。

   1. 選擇狀態——雲就緒性分析器，如下圖所示。

#### 瞭解報表中的重要性級別 {#importance-levels}

下表說明了各種模式檢測器和雲就緒性分析器重要性級別的含義。

| 重要性級別 | 說明 |
|--- |--- |
| INFO/0 | 此查找結果僅供參考。 |
| 建議/1 | 這個發現可能是升級問題。 建議進一步調查。 |
| 主修/2 | 這項發現可能是需要解決的升級問題。 |
| 緊急/3 | 此發現很可能是升級問題，必須解決以防功能或效能遺失。 |
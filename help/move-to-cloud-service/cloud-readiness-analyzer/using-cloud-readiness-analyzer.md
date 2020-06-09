---
title: 使用Cloud Readiness Analyzer
description: 使用Cloud Readiness Analyzer
translation-type: tm+mt
source-git-commit: 317dd08600df9c7127cf8502341f93758ac8ce0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 使用Cloud Readiness Analyzer {#using-cloud-readiness-analyzer}

## 使用Cloud Readiness Analyzer的重要注意事項 {#imp-considerations}

請依照以下章節瞭解運行雲就緒性分析器(CRA)時的重要考慮事項：

* CRA支援6.1版及更新版本的來源AEM例項。
* CRA可以在任何環境下運作。 但是，為了提高檢測率並避免業務關鍵型實例出現任何慢速，建議在源作者測試環境上運行它，在定制、配置、內容和用戶應用程式方面盡可能接近生產環境。 或者，也可以在「發佈」環境的克隆上執行。

## 可用性 {#availability}

Cloud Readiness Analyzer(CRA)可從軟體散發入口網站下載為zip檔案。 您可以透過Package Manager在來源Adobe Experience Manager(AEM)例項上安裝套件。

>[!NOTE]
>從待定位置下載Cloud Readiness Analyzer(CRA)。

## 運行Cloud Readiness Analyzer {#running-tool}

請依照本節內容瞭解如何運行Cloud Readiness Analyzer:

1. 選擇Adobe Experience Manager並導覽至工具-> **Operations** -> **Cloud Readiness Analyzer**。

### 查看結果 {#viewing-the-results}

有兩種方法可以看到CRA的產出：

1. 使用有組織的報表（適用於AEM 6.3版及更新版本）請參閱「CRA檔案規劃與狀態」，以說明報表中的重要性等級

若要檢視CRA的輸出（可與AEM 6.1版及更新版本搭配使用）:

1. 瀏覽至，以導覽至AEM Web Console。

1. 選擇狀態——雲就緒性分析器，如下圖所示。
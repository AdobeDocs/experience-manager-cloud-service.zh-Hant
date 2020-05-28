---
title: 評估移轉至雲服務的複雜性
description: 評估移轉至雲服務的複雜性
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Cloud Readiness Analyzer {#accesing-complexity}

## 概覽 {#overview}

Cloud Readiness Analyzer(CRA)可讓您檢查現有的AEM例項是否已準備好移至雲端服務，方法是偵測出以下模式：

* 使用Cloud Service目前不支援的AEM 6.x功能

* 違反將受移至雲端服務影響的特定規則

>[!NOTE]
>CRA的輸出加速了對升級至雲服務所需開發工作的評估。

## 設定Cloud Readiness Analyzer {#setting-up-cra}

CRA會以套件形式發行，可處理XX及以上版本的任何來源AEM版本，以探索移轉至雲端服務。

它可在軟體分發門戶上使用，並可使用包管理器安裝。

### 使用Cloud Readiness Analyzer {#using-cra}

>[!NOTE]
> CRA可以在任何環境下運行，包括本地開發實例。

>[重要]
>但是，為了提高檢測率並避免關鍵業務實例出現任何慢速，建議在與生產環境盡可能接近的測試環境（在用戶應用程式、內容和配置方面）上運行它

### 在Cloud Readiness Analyzer上查看輸出 {#viewing-output-cra}


1. 瀏覽至「 **Adobe Experience Manager Web Console Configuration」（使用），以導覽至AEM Web Console**`https://serveraddress:serverport/system/console/configMgr`。

1. 選擇狀態——雲就緒性分析器，如下圖所示。

1. 您也可以透過反應式文字或一般JSON介面來檢視輸出。

>[!NOTE]
> 如需這些方 [法的詳細資訊](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) ，請參閱Pattern Detector)。 CRA準備就緒後，需要新增此區段。

## 雲準備的後續步驟 {#the-next-steps}

若要進一步瞭解您的雲端服務準備情況，Adobe必須評估CRA的輸出。

請依照下列步驟傳回檔案：

1. 導覽至AEM Web Console並下載xx檔案，如下圖所示。

1. 開啟DayCare票證，透過下列方式將檔案傳送至Adobe:
   1. 在Daycare中記錄名為「 **Cloud Readiness Analyzer輸出」的支援票證**
   1. 將輸出檔案附加到票證


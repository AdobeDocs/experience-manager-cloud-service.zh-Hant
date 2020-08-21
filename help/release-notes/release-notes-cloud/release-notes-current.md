---
title: ' [!DNL Adobe Experience Manager]  雲端服務 2020.8.0 版發行說明。'
description: '[!DNL Adobe Experience Manager] 雲端服務 2020.8.0 版發行說明。'
translation-type: tm+mt
source-git-commit: 27f9f4441a95964a4ae0db798577510c726133c5
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 11%

---


# [!DNL Adobe Experience Manager] 雲端服務 2020.8.0 版發行說明 {#release-notes}

以下章節概述 Experience Manager 雲端服務 2020.8.0 版的一般發行說明。

## [!DNL Adobe Experience Manager Assets] 雲端服務 {#assets}

* 新部署 [!DNL Experience Manager Assets] 預設會與 [!DNL Adobe Developer Console] 整合。 它可協助您更快速地設定智慧標籤功能。 在現有的部署中，管理員 [會像以前一樣設定智慧標籤](/help/assets/smart-tags-configuration.md#aio-integration) 整合。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新功能 {#what-is-new-commerce}

* 產品主控台功能現已推出。 這可讓AEM中的行銷人員／作者檢視並導覽儲存在商務後端的類別和產品。 另外也支援產品主控台中的類別和產品屬性。

* 產品和類別挑選器已改進，可讓行銷人員透過SKU選擇產品，或透過類別ID選擇類別。

## Cloud Manager {#cloud-manager}

### 發行日期 {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### 新功能 {#what-is-new-cloud-manager}

* 「內容審核」是在Cloud Manager Sites生產管道上啟用的功能。 具有「網站」的程式的「生產管道」設定現在包含名為「內容審核」的第 **三個標籤**。 每當生產管道執行時，在自訂功能測試後，管道中就會包含新的「內容稽核」步驟，以根據多項維度評估網站，包括效能、搜尋引擎最佳化(SEO)、協助工具、最佳實務和PWA（漸進式網頁應用程式）。

   Refer to [Content Audit Testing](/help/implementing/cloud-manager/content-audit-testing.md) for more details.

* 「資產」程式中新建立的環境現在會自動設定Smart Content Services。

* 高眠環境可以從Cloud Manager的「概述」頁面中解除高 **眠** 。


### 錯誤修正 {#bug-fixes-cm}

* 在程式碼品質掃描中，會執行一些不必要和不需要的SonarQube外掛程式。

* 在管線執行頁面上，分支名稱格式不正確。

* 在某些情況下，未完成的管線執行未成功記錄為已完成，從而防止了管線的新執行。

* 管道執行偶爾會因 *內部* 通訊問題而卡住。

* 在布建新組織時，系統管理員以外的其他管理角色的部分使用者會錯誤地獲得Cloud Manager的存取權。

* 在特定條件下，更新索引作業並行啟動多次，導致部署失敗。

* 程式卡上的工具提示不一致正確。

* 在刪除環境中嘗試操作時，用戶介面錯誤地允許該操作。

* Cloud Manager的「概述」頁面上有顏色不 **符** 。

### 已知問題 {#known-issues-cm}

* 包含無效頁面，使「內容審核平均分數」低於應有的分數。

* 「內容稽核」標籤會使用作者網域而非發佈網域，錯誤地顯示基本URL。

* 若要啟動「內容稽核」步驟，使用者必須編輯管線，並可選擇新增頁面。 如果未新增任何頁面，則會檢查首頁。

## 內容轉移工具 {#content-transfer-tool}

請依照本節內容，瞭解內容傳輸工具版本v1.0.4的新增功能和更新。

### 新功能 {#what-is-new-ctt}

* 內容傳輸工具現在支援共用S3 DataStore。

### 錯誤修正 {#ctt-bug-fixes}

* 為工具完成動作增加其他逾時。

* 即使記錄顯示錯誤，舊版UI有時仍顯示成功擷取。


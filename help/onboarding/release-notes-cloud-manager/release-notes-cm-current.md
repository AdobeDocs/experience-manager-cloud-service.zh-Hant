---
title: AEM中Cloud Manager的Cloud Manager版本注意事項2020.11.0版
description: AEM中Cloud Manager的Cloud Manager版本注意事項2020.11.0版
translation-type: tm+mt
source-git-commit: 727dfd1d16a80620fba6db00289021ee5efae0fc
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---


# Adobe Experience Manager中Cloud Manager的Cloud Manager版本說明：Cloud Service 2020.11.0 {#release-notes}

本頁概述AEM中Cloud Manager的發行說明，即Cloud Service 2020.11.0。

## 發行日期 {#release-date}

AEM中Cloud Manager作為雲端服務2020.11.0的發行日期為2020年11月12日。

## Cloud Manager {#cloud-manager}

### 新功能 {#what-is-new}

* 現在，用戶可從「環境」卡和「環境摘要」頁上的「環境」菜單選項中使用新的菜單選項&#x200B;**本地登錄**。
有關詳細資訊，請參閱[管理環境](/help/implementing/cloud-manager/manage-environments.md##login-locally)。

* Cloud Manager中的&#x200B;**Learn**&#x200B;標籤已在UI中以新影像重新整理。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在建立執行前載入的相依性需要下載Maven外掛程式。
* 從Cloud Manager頁尾選取語言的連結現在會導覽至正確的位置。
* 有時在程式碼掃描期間，SonarQube程式不會啟動。 現在會自動偵測到此問題，並嘗試重新啟動。
* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。
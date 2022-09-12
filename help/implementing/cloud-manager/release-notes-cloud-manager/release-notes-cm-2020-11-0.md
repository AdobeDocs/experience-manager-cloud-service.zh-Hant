---
title: AEMas a Cloud Service版2020.11.0中的Cloud Manager發行說明
description: AEMas a Cloud Service版2020.11.0中的Cloud Manager發行說明
feature: Release Information
exl-id: e2acf515-d339-4d2b-9b62-09c1dab1ffac
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---

# Adobe Experience Manager as a Cloud Service 2020.11.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2020.11.0中Cloud Manager的發行說明。

## 發行日期 {#release-date}

AEMas a Cloud Service的Cloud Manager發行日期2020.11.0為2020年11月12日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 新功能表選項 **本機登入** 現在，使用者可從「環境」卡片和「環境摘要」頁面上的「環境」功能表選項中使用。
請參閱 [管理環境](/help/implementing/cloud-manager/manage-environments.md#login-locally) 以取得更多詳細資訊。

* 此 **學習** 標籤，且UI中的新影像已重新整理。

### 錯誤修正 {#bug-fixes-cloud-manager}

* 在建置執行前完成的相依性載入需要下載Maven外掛程式。
* 從Cloud Manager頁尾選取語言的連結現在會導覽至正確位置。
* 有時在程式碼掃描期間，SonarQube程式不會啟動。 現在會自動偵測到此問題，並嘗試重新啟動。
* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

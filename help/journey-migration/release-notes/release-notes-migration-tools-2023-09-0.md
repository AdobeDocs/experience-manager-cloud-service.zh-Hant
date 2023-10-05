---
title: AEMas a Cloud Service版本2023.09.0中移轉工具的發行說明
description: AEMas a Cloud Service版本2022.09.0中移轉工具的發行說明
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
source-git-commit: c89ca7320d8f31d2545cadf98f39e577337b8918
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# AEMas a Cloud Service版本2023.09.0中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.09.0中移轉工具發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具3.0.0版的發行日期為2023年9月7日。

### 新增功能 {#what-is-new-ctt}

「內容轉移工具」已大幅改善，可提供下列優點：
* 運用AzCopy僅複製所需的blob id而非複製所有blob id，減少移轉內容存放庫子集時的傳輸時間
* 使用Oak-upgrade更快地追加差異內容
* 將索引程式與內容擷取程式分開，提高了健全性。 如果索引失敗，則不必再次擷取內容。 只有索引會自動重新啟動，以節省大量時間和精力

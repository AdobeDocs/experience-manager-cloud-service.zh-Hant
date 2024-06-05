---
title: AEMas a Cloud Service版本2023.09.0中移轉工具的發行說明
description: AEMas a Cloud Service版本2023.09.0中移轉工具的發行說明
feature: Release Information
exl-id: 484a60d4-a439-43d6-a23e-4a3b45ef4160
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 4%

---

# AEMas a Cloud Service版本2023.09.0中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2023.09.0中移轉工具發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具3.0.0版的發行日期為2023年9月7日。

### 新增功能 {#what-is-new-ctt}

「內容轉移工具」已經過改良，可提供下列優點：

* 使用AzCopy僅複製所需的blob id而非複製所有blob id，藉此減少移轉內容存放庫子集時的移轉時間。
* 使用Oak-upgrade更快地追加差異內容。
* 將索引程式與內容擷取程式分開，提高了健全性。 如果索引失敗，就不必再次擷取內容。 只有索引會自動重新啟動，從而節省大量時間和精力。

---
title: AEMas a Cloud Service2022.1.0版中移轉工具的發行說明
description: AEMas a Cloud Service2022.1.0版中移轉工具的發行說明
feature: Release Information
exl-id: cbd0c316-bda3-48fb-89d6-a8f97bad1970
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# AEMas a Cloud Service2022.1.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2022.1.0中移轉工具的發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.7.18的發行日期為2022年1月18日。

### 新增功能 {#what-is-new-ctt}

* 將切換開關新增至內容轉移工具中的提取階段，以允許使用者停用 [預先複製](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) 擷取期間。 為獲得最佳擷取速度，若是小型移轉集或在上次擷取後只新增了數個blob，擷取期間的預先複製功能應停用。

### 錯誤修正 {#bug-fixes-ctt}

* 預設設定已更新，以減少擷取期間的執行逾時。

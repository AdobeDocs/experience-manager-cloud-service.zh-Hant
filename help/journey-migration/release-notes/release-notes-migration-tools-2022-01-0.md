---
title: AEM as a Cloud Service 2022.1.0版中移轉工具的發行說明
description: AEM as a Cloud Service 2022.1.0版中移轉工具的發行說明
feature: Release Information
exl-id: cbd0c316-bda3-48fb-89d6-a8f97bad1970
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# AEM as a Cloud Service 2022.1.0版中移轉工具的發行說明 {#release-notes}

本頁面總覽AEM as a Cloud Service 2022.1.0中移轉工具的發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.7.18的發行日期為2022年1月18日。

### 新增功能 {#what-is-new-ctt}

* 切換已新增到內容轉移工具中的擷取階段，以允許使用者在擷取期間停用[預先複製](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html)。 為獲得最佳擷取速度，若是小型移轉集或在上次擷取後只新增了數個blob，擷取期間的預先複製功能應停用。

### 錯誤修正 {#bug-fixes-ctt}

* 預設設定已更新，以減少擷取期間的執行逾時。

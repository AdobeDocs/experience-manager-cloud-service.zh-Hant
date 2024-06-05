---
title: AEMas a Cloud Service版本2021.12.0中移轉工具的發行說明
description: AEMas a Cloud Service版本2021.12.0中移轉工具的發行說明
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 13%

---

# AEMas a Cloud Service版本2021.12.0中移轉工具的發行說明 {#release-notes}

本頁面總覽AEMas a Cloud Service2021.12.0中移轉工具發行說明。

>[!NOTE]
>若要查看 Adobe Experience Manager as a Cloud Service 的最新發行說明，請按一下[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html)。

## 最佳做法分析工具 {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.22的發行日期為2021年12月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠偵測和報告所使用的ACS Commons版本。
* 能夠偵測並報告群組中的使用者和子群組數量。
* 能夠偵測並報告MongoDB中超過16MB的節點屬性值。

### 錯誤修正 {#bug-fixes-bpa}

* 已改善對Foundation元件的偵測，以減少誤判。
* 針對AEM Forms客戶，BPA傳訊關於 `EMAIL_PDF_SUBMIT_ACTION` 已修正AEMas a Cloud Service上無法使用的問題。


## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具v1.7.10的發行日期為2021年12月8日。

### 新增功能 {#what-is-new-ctt}

* 將切換開關新增至內容轉移工具中的擷取階段，讓使用者得以停用 [預先複製](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) 在內嵌期間。 為獲得最佳擷取速度，小型移轉集或在上次擷取後僅新增幾個blob時，應停用擷取期間的預先複製。
* 使用者對應已更新，使用改良的使用者管理API，一次可取得2000名使用者，大幅改善效能。

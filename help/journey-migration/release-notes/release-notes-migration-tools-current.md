---
title: AEMas a Cloud Service版2021.12.0中移轉工具發行說明
description: AEMas a Cloud Service版2021.12.0中移轉工具發行說明
feature: Release Information
source-git-commit: a1c57a9d8165c9e67ce270a3f0c2ad80c75b7196
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# AEMas a Cloud Service版2021.12.0中移轉工具發行說明 {#release-notes}

此頁面概述AEM 2021.12.0中移轉工具的發行說明。

>[!NOTE]
>若要查看最新的Adobe Experience Manager as a Cloud Service發行說明，請按一下 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant).

## Best Practices Analyzer {#bpa-release}

### 發行日期 {#release-date-bpa}

Best Practices Analyzer v2.1.22的發行日期為2021年12月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠檢測並報告所使用的ACS公域的版本。
* 偵測群組中使用者和子群組數目並製作報表的功能。
* 能夠偵測並報告MongoDB中超過16MB的節點屬性值。

### 錯誤修正 {#bug-fixes-bpa}

* 對基礎元件的檢測進行了細化，以減少偽陰性。
* 針對AEM Forms客戶，BPA傳訊關於 `EMAIL_PDF_SUBMIT_ACTION` 「AEMas a Cloud Service」上無法使用的問題已修正。


## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容轉移工具1.7.10版的發行日期為2021年12月8日。

### 新增功能 {#what-is-new-ctt}

* 切換在「內容轉移工具」中新增至擷取階段，以允許使用者停用 [預復](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 擷取期間。 為獲得最佳擷取速度，擷取期間的預先複製應針對小型移轉集而停用，或自上次擷取後僅新增幾個Blob時亦應停用。
* 更新「使用者對應」，以使用改良的「使用者管理API」，即可一次讓2000位使用者使用，大幅提升效能。

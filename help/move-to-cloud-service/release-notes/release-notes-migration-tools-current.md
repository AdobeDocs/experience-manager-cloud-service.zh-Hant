---
title: AEMas a Cloud Service版2021.12.0中移轉工具發行說明
description: AEMas a Cloud Service版2021.12.0中移轉工具發行說明
feature: Release Information
source-git-commit: 587258a831fb5cd3b3a23d1f891db8c2254a8d6b
workflow-type: tm+mt
source-wordcount: '163'
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

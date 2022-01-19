---
title: 《 2021.12.0版中遷移工具AEM發行說明》
description: 《 2021.12.0版中遷移工具AEM發行說明》
feature: Release Information
source-git-commit: 2788db9338da5499b4a9e72ce196e4ae9857b5d5
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# 《 2021.12.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2021.12.0中遷移工具的AEM發行說明。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的當前發行說明，請按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 最佳做法分析器 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.22版的發佈日期為2021年12月1日。

### 新增功能 {#what-is-new-bpa}

* 能夠檢測並報告所使用的ACS共用版本。
* 能夠檢測和報告組中的用戶和子組數。
* 能夠檢測並報告超過16MB的MongoDB中的節點屬性值。

### 錯誤修正 {#bug-fixes-bpa}

* 對Foundation元件的檢測進行細化，減少漏檢。
* 對於AEM Forms客戶，BPA消息 `EMAIL_PDF_SUBMIT_ACTION` 未在AEMas a Cloud Service上可用


## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.7.10的發佈日期為2021年12月8日。

### 新增功能 {#what-is-new-ctt}

* 切換添加到內容傳輸工具的接收階段，以允許用戶禁用 [預拷貝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 攝入時。 為了獲得最佳的攝取速度，對於小遷移集或自上次攝取後僅添加了幾個Blob時，應禁用攝取期間的預拷貝。
* 用戶映射已更新為使用改進的用戶管理API，它允許用戶一次獲得2000個用戶，從而顯著提高了效能。

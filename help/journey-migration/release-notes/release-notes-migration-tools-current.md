---
title: 《 2022.1.0版中遷移工具AEM發行說明》
description: 《 2022.1.0版中遷移工具AEM發行說明》
feature: Release Information
source-git-commit: fec3a69db3b05a6b750ebf718f32f599cac24d0c
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 10%

---


# 《 2022.1.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2022.1.0中遷移工具的AEM發行說明。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的當前發行說明，請按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。


## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.7.18的發佈日期為2022年1月18日。

### 新增功能 {#what-is-new-ctt}

* 切換添加到內容傳輸工具的提取階段，以允許用戶禁用 [預拷貝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 在提取期間。 為了獲得最佳提取速度，應對小遷移集禁用提取期間的預拷貝，或自上次提取後僅添加了幾個blob。

### 錯誤修正 {#bug-fixes-ctt}

* 已更新預設配置，以減少提取期間的執行超時。

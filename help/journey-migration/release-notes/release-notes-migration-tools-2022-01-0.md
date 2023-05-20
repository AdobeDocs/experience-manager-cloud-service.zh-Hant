---
title: 《 2022.1.0版中遷移工具AEM發行說明》
description: 《 2022.1.0版中遷移工具AEM發行說明》
feature: Release Information
exl-id: cbd0c316-bda3-48fb-89d6-a8f97bad1970
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 6%

---

# 《 2022.1.0版中遷移工具AEM發行說明》 {#release-notes}

本頁概述了as a Cloud Service2022.1.0中遷移工具的AEM發行說明。

## 內容轉移工具 {#ctt-release}

### 發行日期 {#release-date-ctt}

內容傳輸工具v1.7.18的發佈日期為2022年1月18日。

### 新增功能 {#what-is-new-ctt}

* 切換添加到內容傳輸工具的提取階段，以允許用戶禁用 [預拷貝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 在提取期間。 為了獲得最佳提取速度，應對小遷移集禁用提取期間的預拷貝，或自上次提取後僅添加了幾個blob。

### 錯誤修正 {#bug-fixes-ctt}

* 已更新預設配置，以減少提取期間的執行超時。

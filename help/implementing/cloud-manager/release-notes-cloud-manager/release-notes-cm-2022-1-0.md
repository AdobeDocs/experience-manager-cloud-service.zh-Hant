---
title: Cloud Manager在as a Cloud Service版AEM2022.01.0中的發行說明
description: 以下是as a Cloud Service版本2022.01.0中Cloud Manager的AEM發行說明。
feature: Release Information
exl-id: 2dfdc943-0518-40ea-8712-1dabb97eeaa9
source-git-commit: 6e394aaabcb123aea53fba49684aaade3e6c87a6
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2022.01.0 {#release-notes}

本頁概述了as a Cloud Service2022.01.0中Cloud ManagerAEM的發行說明。

>[!NOTE]
>
>請參閱 [此頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 為Adobe Experience Manager as a Cloud Service提供的本發行說明。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud ServiceAEM2022.01.0中的發佈日期為2022年1月20日。 下一版計畫於2022年2月10日發行。

## 新增功能 {#what-is-new}

* 雲管理器將 [在檢測到使用了相同的git提交時避免重建代碼庫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 在多個全棧流水線執行中。
* 現在訪AEM問環境日誌需要 **部署管理器** 產品配置檔案。 沒有此配置檔案的用戶將在用戶介面中看到禁用按鈕。
* UI將不允許為未將站點作為解決方案啟用的程式配置前端管道。
* 在生成Git密碼時，將顯示過期日期。

## 錯誤修正 {#bug-fixes}

* 已更正某些前端管道部署遇到的空指針異常。
* 現在，當環境運行的是的過期版本時，可以添加、更新和刪AEM除環境變數。
* 對於在某些罕見情況下使用計畫步驟的管線，生成映像步驟將不再標籤為ERROR。
* 對於只有一個儲存庫的程式，管道執行螢幕現在將顯示儲存庫名稱。

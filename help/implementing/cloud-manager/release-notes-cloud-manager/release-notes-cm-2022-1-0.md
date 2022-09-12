---
title: AEMas a Cloud Service版2022.01.0中的Cloud Manager發行說明
description: 以下是AEM 2022.01.0版as a Cloud Service版本中Cloud Manager的發行說明。
feature: Release Information
exl-id: 2dfdc943-0518-40ea-8712-1dabb97eeaa9
source-git-commit: 6e394aaabcb123aea53fba49684aaade3e6c87a6
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud Service 2022.01.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEMas a Cloud Service版2022.01.0中Cloud Manager的發行說明。

>[!NOTE]
>
>請參閱 [本頁](/help/release-notes/release-notes-cloud/release-notes-current.md) Adobe Experience Manager as a Cloud Service的最新發行說明。

## 發行日期 {#release-date}

AEMas a Cloud Service的Cloud Manager發行日期為2022.01.0年1月20日。 下一版預計於2022年2月10日發行。

## 新增功能 {#what-is-new}

* Cloud Manager將 [偵測到使用相同的git提交時，請避免重建程式碼基底](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 在多個完整堆棧管道執行中。
* 現在存取AEM環境記錄時，需要 **部署管理員** 產品設定檔。 沒有此設定檔的使用者會在使用者介面中看到「已停用」按鈕。
* 若程式未啟用Sites作為解決方案，UI將不允許進行前端管道設定。
* 產生Git密碼時，會顯示到期日。

## 錯誤修正 {#bug-fixes}

* 某些前端管道部署遇到的Null指標例外狀況已修正。
* 現在當環境執行過時的AEM版本時，可以新增、更新及刪除環境變數。
* 在某些罕見情況下，使用排程步驟的管道將不再將建置影像步驟標示為「錯誤」。
* 對於只有一個存放庫的程式，管道執行畫面現在會顯示存放庫名稱。

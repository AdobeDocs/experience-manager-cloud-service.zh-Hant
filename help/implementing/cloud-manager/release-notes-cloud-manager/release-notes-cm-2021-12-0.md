---
title: Cloud Manager在as a Cloud Service版AEM2021.12.0中的發行說明
description: 以下是as a Cloud Service版本2021.12.0中Cloud Manager的AEM發行說明。
feature: Release Information
source-git-commit: bd31dc0ca5b0f4cd84314dba67c8a611f490d377
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---


# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.12.0 {#release-notes}

本頁概述了as a Cloud Service2021.12.0中Cloud ManagerAEM的發行說明。

>[!NOTE]
>
>請參閱 [此頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 為Adobe Experience Manager as a Cloud Service提供的本發行說明。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年12月16日。 下一版計畫於2022年1月20日發行。

## 新增功能 {#what-is-new}

* 提交哈希（在UI中已可見）現在也在API中提供。
* 「活動」(Activity)頁面現在包含一個用於運行管道的彈出窗口，該彈出窗口提供了管道詳細資訊的概覽摘要。
* 已添加更新，以包括「活動」頁中顯示的其他詳細資訊。
* Cloud Manager中的「學習」頁籤現在包括對API指南和相關資源的快速訪問。
* 具有部署管理器角色的用戶現在可以從儲存庫頁面上的操作菜單中為沒有分支的儲存庫啟動項目/分支建立嚮導。
* 部署管理器（位於添加或編輯管道工作流中）現在將被告知如何建立分支或項目（如果所選儲存庫沒有分支）。
* 添加了新的Cloud Manager自助服務功能，以允許 [在環境級別添加自由格式變數和機密。](/help/implementing/cloud-manager/environment-variables.md)
* 新 [參考演示附件](/help/journey-sites/demos-add-on/overview.md) （於2021年12月17日提供），可安裝產品的AEM最新演示代碼庫，並準備通過新的 [快速站點建立工具](/help/journey-sites/quick-site/overview.md) 的子菜單。
* 前端管道現在支援管道變數。
* 現在，所有沙箱的「程式編輯」對話框中都可以啟用螢幕。
* 已刷新概述頁中由操作調用卡提供的指導，以準確反映其與生產全堆棧流水線的關聯。
* 「活動」(Activity)頁面的增強功能添加到了適用於管道的附加詳細資訊中，包括原始碼、提交ID等。
* 在複製TXT條目（「TXT值」而不是「TXT記錄」）以消除可能的混淆時，對UI進行了次要更新。
* [與證書錯誤相關的文檔](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) 已更新，以涵蓋其他示例以及故障排除步驟。
* 在前端管道執行中，現在可使用一個選項，以在部署到生產之前拒絕或批准。
* Cloud Manager使用的AEM項目原型版本已更新為版本32。


## 錯誤修正 {#bug-fixes}

* 生成步驟日誌中未包含功能和UItest對象。
* 產品、功能和UItest步驟的日誌無法通過公共API訪問。
* 在極少數情況下，從環境詳細資訊頁面到發佈或預覽服務的連結將無法正常工作。
* 即使用戶在名稱欄位中輸入了不同的名稱，整個堆棧生產管道仍保留為「生產管道」。

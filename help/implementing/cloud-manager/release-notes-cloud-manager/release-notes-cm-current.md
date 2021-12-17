---
title: AEMas a Cloud Service版2021.12.0中的Cloud Manager發行說明
description: 以下是AEM 2021.12.0版as a Cloud Service版本中Cloud Manager的發行說明。
feature: Release Information
source-git-commit: fc1eae86097f0cc928860ff7f43e3177f2e8f3a1
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---


# Adobe Experience Manager as a Cloud Service 2021.12.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEMas a Cloud Service版2021.12.0中Cloud Manager的發行說明。

>[!NOTE]
>
>請參閱 [本頁](/help/release-notes/release-notes-cloud/release-notes-current.md) 以了解Adobe Experience Manager as a Cloud Service的最新發行說明。

## 發行日期 {#release-date}

AEMas a Cloud Service的Cloud Manager發行日期2021.12.0為2021年12月16日。 下一版預計於2022年1月推出。

### 新增功能 {#what-is-new}

* UI中已顯示提交雜湊，現在也會在API中提供。
* 「活動」頁面現在包含用於執行管道的快顯視窗，可提供管道詳細資訊的摘要，一覽無遺。
* 已新增更新，加入「活動」頁面中顯示的其他詳細資料。
* Cloud Manager中的「學習」標籤現在提供API指南和相關資源的快速存取。
* 具有部署管理員角色的用戶現在可以為資料庫啟動項目/分支建立嚮導，該資料庫沒有「資料庫」頁面上的「操作」菜單中的分支。
* 現在，如果所選儲存庫沒有分支，將通知處於添加或編輯管道工作流的部署管理員如何建立分支或項目。
* 新增Cloud Manager自助服務功能，允許 [在環境層級新增自由格式變數和機密。](/help/implementing/cloud-manager/environment-variables.md)
* 使用 [參考示範附加元件](/help/journey-sites/demos-add-on/overview.md) （於2021年12月17日推出），即可安裝AEM產品的最新示範程式碼庫，並透過新的 [快速網站建立工具](/help/journey-sites/quick-site/overview.md) 在網站中。
* 前端管道現在支援管道變數。
* 現在，所有沙箱的「方案編輯」對話方塊中都可以啟用螢幕。
* 概覽頁面中由動作呼叫卡提供的指引已重新整理，以準確反映其與生產完整堆疊管道的關聯。
* 已新增「活動」頁面的增強功能，以顯示適用於管道的其他詳細資料，包括原始碼、提交ID等。
* 複製TXT項目（「TXT值」而非「TXT記錄」）時，已微幅更新UI，以移除可能的混淆。
* [與憑證錯誤相關的檔案](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors) 已更新，涵蓋其他範例及疑難排解步驟。
* 前端管道執行中現在提供選項，可在部署至生產環境前拒絕或核准。

### 錯誤修正 {#bug-fixes}

* 建置步驟記錄中未包含功能和UI測試成品。
* 無法透過公用API存取產品、功能和UI測試步驟的記錄檔。
* 極少數情況下，從環境詳細資料頁面到發佈或預覽服務的連結將無法運作。
* 即使使用者在名稱欄位中輸入不同名稱，完整堆疊生產管道仍會保留名為「生產管道」。

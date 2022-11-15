---
title: AEM as a Cloud Service 版本 2021.12.0 中 Cloud Manager 的發行說明
description: 以下是 AEM as a Cloud Service 版本 2021.12.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: ee920bc5-cad7-4fac-bf73-bc1178699f90
source-git-commit: 1b7183421b9acd30697f1dc228dd9e2728d24ba6
workflow-type: ht
source-wordcount: '479'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.12.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.12.0 中 Cloud Manager 的發行說明

>[!NOTE]
>
>有關 Adobe Experience Manager as a Cloud Service 的目前發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.12.0 中的 Cloud Manager 發行日期是 2021 年 12 月 16 日。下一個版本計畫於 2022 年 1 月 20 日發行。

## 新增功能 {#what-is-new}

* 已經在 UI 中可見的認可雜湊現也在 API 中提供。
* 活動頁面現在包含一個用於執行管道的快顯視窗，其提供一目了然的管道詳細資訊摘要。
* 更新以包括新增的活動頁面中顯示的其他詳細資訊。
* Cloud Manager 中的學習索引標籤現在包括快速存取 API 指南和相關資源。
* 具有 Deployment Manager 角色的使用者現在可以從存放庫頁面上的動作選單為沒有分支的存放庫啟動專案/分支建立精靈。
* 如果所選存放庫沒有分支，系統會通知處於新增或編輯管道工作流程中的部署管理員該如何建立分支或專案。
* 新增了新的 Cloud Manager 自助服務功能，可[在環境層級新增自由格式的變數和密碼。](/help/implementing/cloud-manager/environment-variables.md)
* 校訂中的已知問題使用新的[參考示範附加元件](/help/journey-sites/demos-add-on/overview.md) (2021 年 12 月 17 日可用)，可以安裝 AEM 產品的最新示範計劃碼庫，且可透過 Sites 中新的[快速建立網站工具](/help/journey-sites/quick-site/overview.md)部署計劃碼庫。
* 前端管道現在支援管道變數。
* 現在可以在所有沙箱的「計畫編輯」對話框中啟用畫面。
* 總覽頁面中召喚行動卡提供的指南已更新，以準確反映其與生產完整堆疊管道的關聯。
* 新增了活動頁面的增強功能，以顯示適用於管道的其他詳細資訊，包括原始計劃碼、認可 ID 等。
* 在複製 TXT 專案 (「TXT 值」而不是「TXT 記錄」) 時，對 UI 進行了小幅更新，以消除潛在的混淆。
* 已更新[與憑證錯誤相關的文件](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-errors)，以涵蓋其他範例以及疑難排解步驟。
* 現在前端管道執行中提供了一個選項，用於在部署到生產之前進行拒絕或核准。
* Cloud Manager 使用的 AEM 專案原型版本已更新至版本 32。


## 錯誤修正 {#bug-fixes}

* 功能和 UI 測試成品未包含在建置步驟記錄中。
* 無法透過公共 API 存取產品、功能和 UI 測試步驟的記錄。
* 在極少數情況下，從環境詳細資訊頁面到發佈或預覽服務的連結會無法運作。
* 即便使用者在名稱欄位中輸入了不同的名稱，完整堆疊生產管道仍命名為「生產管道」。

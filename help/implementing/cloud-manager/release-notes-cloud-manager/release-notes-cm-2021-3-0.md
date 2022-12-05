---
title: AEM as a Cloud Service 版本 2021.3.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2021.3.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.3.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.3.0 中 Cloud Manager 的發行說明

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.3.0 中的 Cloud Manager 發行日期是 2021 年 3 月 11 日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 如果客戶的環境中已有 [IP 允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)、[SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)和[自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的現有自訂網域名稱設定，將看到有關其先前現有設定的訊息，也可透過 UI 進行自助服務。

* 擁有必要權限的使用者現在可以編輯方案，好讓他們以自助方式執行以下作業：
   * 使用 Assets 將 Sites 解決方案新增現有計畫中，反之亦然。
   * 從包含 Sites 和 Assets 的現有方案中移除 Sites 或 Assets。
   * 在現有方案中新增第二個未使用的解決方案權利，或當做新的方案。

* **AEM 維護更新**&#x200B;標籤現在會顯示在管線執行和活動畫面中。

* 如果環境處於休眠狀態，但同時有 AEM 更新可用，則&#x200B;**已休眠**&#x200B;狀態會優先於&#x200B;**有可用的更新**。

* 使用者現在可以在瀏覽至 Unified Shell 的使用者個人資料圖示 (右上方) 後選取「檢視 Cloud Manager 角色」選項，以查看其 Cloud Manager 角色。

* **申請核准**&#x200B;標籤現在已重新標記為&#x200B;**生產核准**，好讓人更容易了解。

* **版本**&#x200B;標籤現已在生產管線執行畫面中重新標記為 **Git Tag**。

* 定義重要度量不符合定義之臨界值時的行為模式的標籤已重新標記，以反映其真正的行為：**立即取消**&#x200B;和&#x200B;**立即核准**。

* 已根據 AEM Cloud Service SDK 的版本 `2021.3.4997.20210303T022849Z-210225` 更新了類別和方法淘汰清單。

* Cloud Manager 生產管線現在包含[自訂 UI 測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 錯誤修正  {#bug-fixes}

* 在 AEM 推送升級期間，某些情況下會跳過套件版本控制。

* 當套件嵌入到其他套件中時，部分品質問題沒有被發現。

* 在不明確的情況下，打開「新增計畫」對話框時生成的預設程序名稱可能與現有程序名稱重複。

* 有時，如果使用者在啟動管道後立即離開管道執行頁面，則會顯示一則錯誤消息，指出操作失敗，儘管執行實際上已開始。

* 當客戶構建導致無效包時，構建步驟不必要地重新啟動。

* 有時，即使未部署該設定，使用者也可能會在 IP 允許清單旁邊看到綠色的「活動」狀態。

* 所有現有的生產管道都將透過體驗稽核步驟自動啟用。

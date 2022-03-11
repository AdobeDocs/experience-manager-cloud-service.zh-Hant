---
title: Cloud Manager在as a Cloud Service版AEM2021.3.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2021.3.0中的發行說明
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.3.0 {#release-notes}

本頁概述了as a Cloud Service2021.3.0中Cloud Manager的發行說明AEM。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年3月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 具有預先存在的自定義域名配置的環境的客戶 [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)。 [SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) 和 [自定義域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) 將看到有關其先前現有配置的消息，並能夠通過UI自助服務。

* 具有必要權限的用戶現在可以編輯程式，允許他們以自助方式執行以下操作：
   * 將「站點」解決方案添加到具有「資產」的現有程式，反之亦然。
   * 從具有站點和資產的現有程式中刪除站點或資產。
   * 將第二個未使用的解決方案權利添加到現有程式或作為新程式。

* **推AEM送更新** 現在將同時顯示「管線執行」和「活動」螢幕的標籤。

* 如果某個環境已休眠，但還有可AEM用的更新， **冬眠** 狀態將優先於 **更新可用**。

* 現在，用戶可以在導航到Unified Shell的「用戶配置檔案」表徵圖（右上）後選擇「查看雲管理器角色」選項來查看其雲管理器角色。

* 標籤 **申請審批** 被重新安排 **生產審批** 更清晰。

* 的 **版本** 標籤已重新標籤為 **Git標籤** 在「生產管道」執行螢幕中。

* 當重要度量不滿足定義的閾值時定義行為的標籤已重新標籤，以反映其真實行為： **立即取消** 和 **立即批准**。

* 類和方法棄用清單已根據版本進行更新 `2021.3.4997.20210303T022849Z-210225` AEM Cloud Service軟體開發工具包。

* Cloud Manager生產管道現在將包括 [自定義UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 功能。

### 錯誤修正  {#bug-fixes}

* 在某些情況下，在推送升級期間跳過了包AEM版本控制。

* 當將包嵌入到其他包中時，未正確發現某些質量問題。

* 在模糊的情況下，開啟「添加程式」對話框時生成的預設程式名稱可能是現有程式名稱的副本。

* 有時，如果用戶在啟動管道後立即從管道執行頁面導航出去，則會顯示一條錯誤消息，指出操作失敗，儘管實際上執行會開始。

* 當客戶生成導致無效包時，生成步驟不必要地重新啟動。

* 有時，即使未部署IP允許清單，用戶也可能看到該配置旁邊的綠色「活動」狀態。

* 使用「體驗審核」步驟將自動啟用所有現有生產管道。

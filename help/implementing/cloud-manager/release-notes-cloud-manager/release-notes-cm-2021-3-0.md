---
title: AEM as a Cloud Service2021.3.0版中Cloud Manager發行說明
description: AEM as a Cloud Service2021.3.0版中Cloud Manager發行說明
feature: Release Information
exl-id: f826e0c6-3b1d-44f5-99a2-f792f5df3a55
source-git-commit: 575be022704e998e63162f19c37ece877efef627
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Adobe Experience Manager as a Cloud Service 2021.3.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2021.3.0as a Cloud Service版中Cloud Manager的發行說明。

## 發行日期 {#release-date}

AEM 2021.3.0中的Cloud Manageras a Cloud Service日期為2021年3月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 環境中具有預先存在之自訂網域名稱設定的客戶 [IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) 和 [自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) 會看到其先前現有設定的相關訊息，且將能透過UI自助服務。

* 擁有必要權限的使用者現在可以編輯方案，讓他們能以自助方式執行下列作業：
   * 使用資產將Sites解決方案新增至現有計畫，反之亦然。
   * 從同時具有Sites和Assets的現有程式中移除Sites或Assets。
   * 將第二個未使用的解決方案權利添加到現有程式或作為新程式添加。

* **AEM維護更新** 標籤現在會針對Pipeline Execution和Activity畫面顯示。

* 如果環境休眠，但也有AEM更新可用，則 **休眠** 狀態優先於 **可用更新**.

* 使用者現在可以在導覽至統一殼層的「使用者設定檔」圖示（右上）後，選取「檢視Cloud Manager角色」選項，查看其Cloud Manager角色。

* 標籤 **申請批准** 已重新標籤為 **生產核准** 更清晰。

* 此 **版本** 標籤已重新標籤為 **Git標籤** 在「生產管道」執行畫面中。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標示，以反映其真實行為： **立即取消** 和 **立即核准**.

* 類別和方法取代清單已根據版本更新 `2021.3.4997.20210303T022849Z-210225` AEM Cloud Service SDK的ID服務。

* Cloud Manager生產管道現在將包含 [自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 功能。

### 錯誤修正  {#bug-fixes}

* 在AEM推送升級期間，在某些情況下會略過套件版本設定。

* 將包嵌入其他包時，未正確發現某些質量問題。

* 在模糊的情況下，開啟「添加程式」對話框時生成的預設程式名稱可能與現有程式名稱重複。

* 有時，如果使用者在啟動管道後立即離開管道執行頁面進行導覽，雖然實際上會開始執行，但會顯示錯誤訊息，指出動作失敗。

* 當客戶建置導致無效的套件時，建置步驟會不必要地重新啟動。

* 有時，即使未部署該設定，使用者仍可能會在IP允許清單旁看到綠色的「作用中」狀態。

* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

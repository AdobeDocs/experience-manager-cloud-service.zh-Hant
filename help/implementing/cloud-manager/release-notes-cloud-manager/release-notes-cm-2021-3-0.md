---
title: AEM as aCloud Service中Cloud Manager的發行說明2021.3.0版
description: AEM as aCloud Service中Cloud Manager的發行說明2021.3.0版
feature: Release Information
source-git-commit: a707968483dc1196628b737ad207bfefe63ca94b
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Adobe Experience Manager as aCloud Service2021.3.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM as a 2021.3.0Cloud Service中Cloud Manager的發行說明。

## 發行日期 {#release-date}

AEM as aCloud Service2021.3.0中的Cloud Manager發行日期為2021年3月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* 若客戶的環境中已有[IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)和[自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的先前自訂網域名稱設定，則會看到有關其先前現有設定的訊息，且將能透過UI自行服務。

* 擁有必要權限的使用者現在可以編輯方案，讓他們能以自助方式執行下列作業：
   * 使用資產將Sites解決方案新增至現有計畫，反之亦然。
   * 從同時具有Sites和Assets的現有程式中移除Sites或Assets。
   * 將第二個未使用的解決方案權利添加到現有程式或作為新程式添加。

* **AEM Push** Updatelabel現在會針對Pipeline Execution和Activity畫面顯示。

* 如果環境已休眠，但也有AEM更新可用，則&#x200B;**已休眠**&#x200B;狀態將優先於&#x200B;**可用更新**。

* 使用者現在可以在導覽至統一殼層的「使用者設定檔」圖示（右上）後，選取「檢視Cloud Manager角色」選項，查看其Cloud Manager角色。

* 標籤&#x200B;**申請核准**&#x200B;已重新標示為&#x200B;**生產核准**，以更清楚明瞭。

* 在「生產管道」執行畫面中，**Version**&#x200B;標籤已重新標示為&#x200B;**Git Tag**。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標示，以反映其真實行為：**取消立即**&#x200B;和&#x200B;**立即批准**。

* 類別和方法取代清單已根據AEMCloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版本更新。

* Cloud Manager生產管道現在將包含[自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 錯誤修正  {#bug-fixes}

* 在AEM推送升級期間，在某些情況下會略過套件版本設定。

* 將包嵌入其他包時，未正確發現某些質量問題。

* 在模糊的情況下，開啟「添加程式」對話框時生成的預設程式名稱可能與現有程式名稱重複。

* 有時，如果使用者在啟動管道後立即離開管道執行頁面進行導覽，雖然實際上會開始執行，但會顯示錯誤訊息，指出動作失敗。

* 當客戶建置導致無效的套件時，建置步驟會不必要地重新啟動。

* 有時，即使未部署該設定，使用者仍可能會在IP允許清單旁看到綠色的「作用中」狀態。

* 所有現有的生產管道都會透過體驗稽核步驟自動啟用。

---
title: 沙箱方案簡介
description: 了解哪些沙箱方案與生產方案有何不同。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 2%

---


# 沙箱方案簡介 {#sandbox-programs}

了解哪些沙箱方案與生產方案有何不同。

## 簡介 {#introduction}

沙箱計畫通常是為了提供培訓、執行示範、培訓或概念驗證(POC)之目的而建立，因此不適用於傳送即時流量。

沙箱方案是AEM Cloud Service提供的兩種方案之一，另一種是 [生產計畫。](introduction-production-programs.md) 請參閱該文檔 [了解方案和方案類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 以深入了解方案類型。

## 自動建立 {#auto-creation}

沙箱方案可自動建立。 每當您建立新的沙箱方案時，Cloud Manager就會自動：

* 將AEM Sites和AEM Assets新增為計畫中的解決方案。
* 設定專案Git存放庫，並根據 [AEM專案原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* 建立開發環境。
* 建立可部署至開發環境的非生產管道。

沙箱方案只會有一個開發環境。

## 限制與條件 {#limitations}

由於沙箱方案不適用於即時流量，因此其使用方式有特定限制和條件，使其與生產方案有所區別。

### 無即時流量 {#live-traffic}

沙箱方案不適用於傳送即時流量，因此不受 [AEMas a Cloud Service承諾。](https://www.adobe.com/legal/service-commitments.html)

### 無自動縮放 {#auto-scaling}

沙箱程式中建立的環境沒有針對自動縮放進行設定。 因此，這些環境不適合進行效能或負載測試。

### 沒有自訂網域或IP允許清單 {#ip-allow}

沙箱方案中無法使用自訂網域和IP允許清單。

### 無高級網路 {#advanced-networking}

[高級網路功能](/help/security/configuring-advanced-networking.md) （例如，自助配置VPN、非標準埠、專用輸出IP地址等） 沙箱方案中無法使用。

### 手動更新AEM {#updates}

AEM更新不會自動推送至沙箱方案，但可手動套用至沙箱方案中的環境。

* 手動更新只能在目標環境具有正確配置的管道時執行。
* 手動更新至生產或測試環境會自動更新另一個環境。 生產+預備環境集必須位於相同AEM版本上。

請參閱該文檔 [AEM版本更新](/help/implementing/deploying/aem-version-updates.md) 以取得更多詳細資訊。

請參閱該文檔 [更新環境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) 了解如何更新環境。

### 休眠和刪除 {#hibernation}

沙箱程式中的環境閒置8小時後會自動休眠。 休眠後，即可手動解除休眠。

沙箱程式在進入連續休眠模式6個月後會遭到刪除，之後可重新建立。

請參閱 [休眠和解除休眠沙箱環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) 以取得更多詳細資訊。

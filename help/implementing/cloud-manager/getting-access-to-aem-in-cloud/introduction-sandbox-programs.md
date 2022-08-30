---
title: '沙盒程式簡介 '
description: 瞭解沙盒程式與生產程式有何不同。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 05cba12cdd14c2e29f6a471047ce95fcf720abc4
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 2%

---


# 沙盒程式簡介 {#sandbox-programs}

瞭解沙盒程式與生產程式有何不同。

## 簡介 {#introduction}

通常，建立沙盒程式是為了滿足培訓、運行演示、支援或概念驗證(POC)的目的，因此它不是為了傳遞即時流量。

沙盒程式是AEM Cloud Service提供的兩種類型的程式之一，另一種是 [生產計畫。](introduction-production-programs.md) 請參閱文檔 [瞭解程式和程式類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 瞭解有關程式類型的詳細資訊。

## 自動建立 {#auto-creation}

沙盒程式具有自動建立功能。 每當您自動建立新沙盒程式時，雲管理器：

* 將AEM Sites和AEM Assets作為解決方案添加到您的計畫中。
* 設定項目Git儲存庫，其中包含基於 [原型AEM計畫。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* 建立開發環境。
* 建立部署到開發環境的非生產管道。

沙盒程式將只有一個開發環境。

## 限制和條件 {#limitations}

由於沙盒程式不適合即時流量，因此它們在使用上存在某些限制和條件，這使它們與生產程式不同。

### 無即時通信 {#live-traffic}

沙盒程式不是用來承載即時流量的，因此不受 [AEMas a Cloud Service。](https://www.adobe.com/legal/service-commitments.html)

### 無自動縮放 {#auto-scaling}

在沙盒程式中建立的環境未配置為自動擴展。 因此，這些環境不適合用於效能或負載測試。

### 沒有自定義域或IP允許清單 {#ip-allow}

自定義域和IP允許清單在沙盒程式中不可用。

### 無高級網路 {#advanced-networking}

[高級網路功能](/help/security/configuring-advanced-networking.md) （例如VPN的自助配置、非標準埠、專用出口IP地址等） 在沙盒程式中不可用。

### 手動更AEM新 {#updates}

更新AEM不會自動推送到沙盒程式，但可以手動應用到沙盒程式中的環境。

* 只有在目標環境具有正確配置的管道時才能運行手動更新。
* 手動更新到生產或登台環境將自動更新另一個環境。 Production+Stage環境集必須位於同一版本AEM上。

請參閱文檔 [版本更新](/help/implementing/deploying/aem-version-updates.md) 的子菜單。

請參閱文檔 [更新環境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) 瞭解如何更新環境。

### 休眠和刪除 {#hibernation}

沙盒程式中的環境在不活動8小時後自動休眠。 冬眠後，可以手動去冬眠。

沙盒程式在進入連續休眠模式6個月後被刪除，之後可以重新建立它們。

請參閱 [冬眠和冬眠沙盒環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) 的子菜單。

---
title: 沙箱程序簡介
description: 了解沙箱程序與生產程序有何不同。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 85%

---


# 沙箱程序簡介 {#sandbox-programs}

了解沙箱程序與生產程序有何不同。

## 簡介 {#introduction}

建立沙箱程序的目的通常是提供培訓、執行示範、培訓、或概念證明 (POC) ，而不是承載即實流量。

沙箱程序是 AEM Cloud Service 中可用的兩種程序之一，另一種是[生產程序。](introduction-production-programs.md) 另請參閱 [瞭解方案和方案型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) 以進一步瞭解程式型別。

## 自動建立 {#auto-creation}

沙箱程序具有自動建立功能。每當您自動建立新的沙箱程序 Cloud Manager 時：

* 在您的程序中新增 AEM Sites 和 AEM Assets 作為解決方案。
* 使用基於範例項目的範例項目設定項目 git 存放庫 [AEM Project 原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)
* 建立開發環境。
* 建立部署到開發環境的非生產管道。

沙箱程序將只有一個開發環境。

## 限制和條件 {#limitations}

由於沙箱程序不適用於即時流量，因此沙箱程序對其使用有一定的限制和條件，這使其與生產程序不同。

### 沒有即時流量 {#live-traffic}

沙箱程序並不意味著承載實時流量，因此不受 [AEM as a Cloud Service 承諾。](https://www.adobe.com/tw/legal/service-commitments.html)

### 沒有自動縮放 {#auto-scaling}

在沙箱程序中建立的環境未配置為自動縮放。因此，這些環境不適合進行性能或負載測試。

### 沒有自訂域或 IP 加入允許清單 {#ip-allow}

自訂域和 IP 允許清單在沙箱程序中不可用。

### 非進階網路 {#advanced-networking}

[進階網路功能](/help/security/configuring-advanced-networking.md) 沙箱程式中無法使用（例如VPN、非標準連線埠、專用出口IP地址的自助配置）。

### 手動 AEM 更新 {#updates}

AEM 更新不會自動推送到沙箱程序，但可以手動應用於沙箱程序中的環境。

* 僅當目標環境具有正確配置的管道時，才能執行手動更新。
* 對生產或登台環境的手動更新將自動更新另一個。Production+Stage 環境集必須位於同一 AEM 版本上。

另請參閱 [AEM版本更新](/help/implementing/deploying/aem-version-updates.md) 以取得更多詳細資料。

另請參閱 [更新環境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) 以瞭解如何更新環境。

### 休眠和刪除 {#hibernation}

沙箱計劃內的環境在八小時不活動後自動休眠。沙箱環境會在連續休眠六個月後刪除。

另請參閱 [使沙箱環境休眠和解除沙箱環境休眠](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) 瞭解更多有關如何解除環境休眠和自動沙箱刪除的詳細資訊。

### 無技術支援 {#no-support}

由於建立沙箱程式的目的通常是要培訓、執行範例、啟用或概念驗證 (POC)，因此無法為沙箱程式中發生的問題提供技術支援。

如果您在建立和管理沙箱程式時發生問題，這仍在技術支援範圍內。

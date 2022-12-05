---
title: 沙箱程序簡介
description: 了解沙箱程序與生產程序有何不同。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: ht
source-wordcount: '438'
ht-degree: 100%

---


# 沙箱程序簡介 {#sandbox-programs}

了解沙箱程序與生產程序有何不同。

## 簡介 {#introduction}

建立沙箱程序的目的通常是提供培訓、執行示範、培訓、或概念證明 (POC) ，而不是承載即實流量。

沙箱程序是 AEM Cloud Service 中可用的兩種程序之一，另一種是[生產程序。](introduction-production-programs.md)請參考[了解程序和程序類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)了解有關程序類型的更多資訊。

## 自動建立 {#auto-creation}

沙箱程序具有自動建立功能。每當您自動建立新的沙箱程序 Cloud Manager 時：

* 在您的程序中新增 AEM Sites 和 AEM Assets 作為解決方案。
* 使用基於範例項目的範例項目設定項目 git 存放庫[AEM Project 原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)
* 建立開發環境。
* 建立部署到開發環境的非生產管道。

沙箱程序將只有一個開發環境。

## 限制和條件 {#limitations}

由於沙箱程序不適用於即時流量，因此沙箱程序對其使用有一定的限制和條件，這使其與生產程序不同。

### 沒有即時流量 {#live-traffic}

沙箱程序並不意味著承載實時流量，因此不受[AEM as a Cloud Service 承諾。](https://www.adobe.com/tw/legal/service-commitments.html)

### 沒有自動縮放 {#auto-scaling}

在沙箱程序中建立的環境未配置為自動縮放。因此，這些環境不適合進行性能或負載測試。

### 沒有自訂域或 IP 加入允許清單 {#ip-allow}

自訂域和 IP 允許清單在沙箱程序中不可用。

### 非進階網路 {#advanced-networking}

[進階網路功能](/help/security/configuring-advanced-networking.md) (例如自助式佈建 VPN、非標準連接埠、專用輸出 IP 位址等)在沙箱程序中不可用。

### 手動 AEM 更新 {#updates}

AEM 更新不會自動推送到沙箱程序，但可以手動應用於沙箱程序中的環境。

* 僅當目標環境具有正確配置的管道時，才能執行手動更新。
* 對生產或登台環境的手動更新將自動更新另一個。Production+Stage 環境集必須位於同一 AEM 版本上。

如需更多詳細資訊，請參閱文件：[AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)。

請參考文件[更新環境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)學習如何更新環境。

### 休眠和刪除 {#hibernation}

沙箱程序內的環境在 8 小時不活動後自動休眠：一旦休眠，它們可以手動解除休眠。

沙箱程序在處於連續休眠模式 6 個月後被刪除，之後可以重新建立它們。

如需了解詳細資訊，請參閱：[休眠和去休眠沙箱環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md)。

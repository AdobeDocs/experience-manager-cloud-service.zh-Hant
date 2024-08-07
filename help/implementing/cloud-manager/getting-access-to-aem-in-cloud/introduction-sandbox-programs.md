---
title: 沙箱計畫簡介
description: 了解沙箱計畫與生產計畫有何不同。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 88b0479c44f6431a9f254551e51b1ce86af91d0f
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 90%

---


# 沙箱計畫簡介 {#sandbox-programs}

了解沙箱計畫與生產計畫有何不同。

## 簡介 {#introduction}

建立沙箱計畫的目的通常是提供培訓、執行示範、培訓、或概念證明 (POC) ，而不是承載即實流量。

沙箱計畫是 AEM Cloud Service 中可用的兩種計畫之一，另一種是[生產計畫。](introduction-production-programs.md) 請參閱[了解計畫和計畫類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)以深入了解程序類型。

## 自動建立 {#auto-creation}

沙箱計畫具有自動建立功能。每當您建立沙箱計畫時，Cloud Manager都會自動：

* 在您的計畫中新增 AEM Sites 和 AEM Assets 作為解決方案。
* 使用基於範執行個體目的範執行個體目設定項目 git 存放庫 [AEM Project 原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)
* 建立開發環境。
* 建立部署到開發環境的非生產管道。

沙箱計畫將只有一個開發環境。

## 限制和條件 {#limitations}

由於沙箱計畫不適用於即時流量，因此沙箱計畫對其使用有一定的限制和條件，這使其與生產計畫不同。

### 沒有即時流量 {#live-traffic}

沙箱計畫並不意味著承載實時流量，因此不受 [AEM as a Cloud Service 承諾。](https://www.adobe.com/tw/legal/service-commitments.html)

### 沒有自動縮放 {#auto-scaling}

在沙箱計畫中建立的環境未配置為自動縮放。因此，這些環境不適合進行性能或負載測試。

### 沒有自訂域或 IP 加入允許清單 {#ip-allow}

[自訂網域](/help/implementing/cloud-manager/custom-domain-names/introduction.md)和[IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)在沙箱程式中無法使用。

### 沒有其他Publish地區 {#additional-publish-regions}

[其他發佈區域](/help/operations/additional-publish-regions.md)不適用於沙箱計畫。

### 無99.99% SLA {#999-sla}

[99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)不適用於沙箱程式。

### 非進階網路 {#advanced-networking}

[進階網路功能](/help/security/configuring-advanced-networking.md) (例如自助式佈建 VPN、非標準連接埠、專用輸出 IP 位址等) 在沙箱計畫中不可用。

### 手動 AEM 更新 {#updates}

AEM 更新不會自動推送到沙箱計畫，但可以手動應用於沙箱計畫中的環境。

* 僅當目標環境具有正確配置的管道時，才能執行手動更新。
* 對生產或中繼環境的手動更新將自動更新另一個。Production+Stage 環境集必須位於同一 AEM 版本上。

如需更多詳細資訊，請參閱 [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)。

請參閱[更新環境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)以了解如何更新環境。

### 休眠和刪除 {#hibernation}

沙箱計畫內的環境在八小時不活動後自動休眠。沙箱環境會在連續休眠六個月後刪除。

如需如何去休眠環境和自動刪除沙箱的詳細資訊，請參閱[休眠和去休眠沙箱環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md)。

### 無技術支援 {#no-support}

由於建立沙箱程式的目的通常是要培訓、執行範例、啟用或概念驗證 (POC)，因此無法為沙箱程式中發生的問題提供技術支援。

如果您在建立和管理沙箱程式時發生問題，這仍在技術支援範圍內。

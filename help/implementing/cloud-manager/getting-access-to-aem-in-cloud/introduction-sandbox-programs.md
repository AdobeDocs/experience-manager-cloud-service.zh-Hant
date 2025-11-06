---
title: 沙箱計畫簡介
description: 瞭解沙箱程式是什麼以及它們與生產程式有何不同。
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 32%

---


# 沙箱計畫簡介 {#sandbox-programs}

瞭解沙箱程式是什麼以及它們與生產程式有何不同。

## 簡介 {#introduction}

建立沙箱計畫的目的通常是提供培訓、執行示範、培訓、或概念驗證 (POC) ，而不是承載即實流量。

沙箱計畫是AEM Cloud Service中可用的兩種計畫之一，另一種是[生產計畫](introduction-production-programs.md)。 請參閱[瞭解程式和程式型別](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)，以進一步瞭解程式型別。

## 自動建立 {#auto-creation}

沙箱計畫具有自動建立功能。每當您[建立沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)時，Cloud Manager都會自動：

* 新增AEM Sites、Assets和Edge Delivery Services作為計畫的預設解決方案。

  ![為沙箱選取解決方案和附加元件](assets/sandbox-solutions-add-ons.png)

* 使用範例專案設定專案Git存放庫(根據[AEM專案原型](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/developing/archetype/overview))。
* 建立開發環境。
* 建立部署到開發環境的非生產管道。

沙箱計畫只有一個開發環境。

## 使用說明和條件 {#usage-notes-conditions}

由於沙箱程式不適用於即時流量，因此沙箱程式對其使用有一定的限制和條件，這使其與生產程式不同。

| 限制/條件 | 說明 |
| --- | --- |
| 沒有即時流量 | 沙箱程式並不意味著承載即時流量，因此不受[AEM as a Cloud Service承諾](https://www.adobe.com/tw/legal/service-commitments.html)的約束。 |
| 無自動縮放 | 在沙箱計畫中建立的環境未配置為自動縮放。因此，這些環境不適合進行效能或負載測試。 |
| 沒有自訂網域或IP允許清單 | 沙箱程式中無法使用[自訂網域](/help/implementing/cloud-manager/custom-domain-names/introduction.md)和[IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| 沒有其他發佈區域 | [其他發佈區域](/help/operations/additional-publish-regions.md)不適用於沙箱計畫。 |
| 否99.99% SLA | [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)不適用於沙箱計畫。 |
| 沒有進階網路 | [進階網路功能](/help/security/configuring-advanced-networking.md) (例如自助式佈建 VPN、非標準連接埠、專用輸出 IP 位址等) 在沙箱計畫中不可用。 |
| 沒有自動的AEM更新 | AEM 更新不會自動推送到沙箱計畫，但可以手動應用於沙箱計畫中的環境。<br>·只有當目標環境具有正確設定的管道時，才能執行手動更新。<br>·對生產或中繼環境的手動更新會自動更新另一個。 Production+Stage 環境集必須位於同一 AEM 版本上。<br>如需詳細資訊，請參閱[AEM版本更新](/help/implementing/deploying/aem-version-updates.md)。<br>請參閱[更新環境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)以瞭解如何更新環境。 |
| 無技術支援 | 由於沙箱計畫通常建立的目的是提供培訓、執行示範、培訓、或POC （概念證明），因此技術支援不適用於沙箱計畫中所遇到的問題。<br>如果您在建立和管理沙箱計畫時遇到問題，這些問題屬於技術支援範圍。 |
| 休眠和刪除 | 沙箱計畫內的環境在八小時不活動後自動休眠。沙箱環境會在連續休眠六個月後刪除。<br>請參閱[休眠和去休眠沙箱環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md)，以取得有關如何去休眠環境和自動刪除沙箱的詳細資訊。 |

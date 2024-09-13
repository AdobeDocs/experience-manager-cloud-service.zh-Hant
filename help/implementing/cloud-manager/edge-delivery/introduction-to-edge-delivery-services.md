---
title: Cloud Manager中的Edge Delivery Services簡介
description: 瞭解如何使用Edge Delivery Services傳遞Cloud Manager專案。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 6%

---

# Cloud Manager中的Edge Delivery Services簡介 {#edge-delivery-services}

Edge Delivery Services 是一組可組合的服務，可讓您以高度靈活的方式在網站上製作內容。此功能可讓您進行以下工作：

* 使用完美的Lighthouse分數建立快速網站。
* 透過RUM （即時監控）持續監控效能。
* 透過分離內容來源來提高撰寫效率。

您可以使用通用編輯器和檔案式編寫，同時使用AEM內容管理和WYSIWYG編寫。

AEM as a Cloud Service中的Cloud Manager可讓您為專案啟用Edge Delivery服務。

>[!TIP]
>
>如需Edge Delivery Services的詳細資訊，以及它如何與AEM搭配使用，請參閱[Edge Delivery Services概觀](/help/edge/overview.md)。

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->


## 關於Cloud Manager中的Edge Delivery Services {#edge-in-cloud-manager}

如果您已將Edge Delivery Services授權為Adobe Experience Manager Sites的一部分，則可以直接在Cloud Manager中使用Edge Delivery Services上線您的網站，並使用引導式自助服務體驗[上線](/help/implementing/cloud-manager/managing-code/private-repositories.md)。

此外，您可以存取統一體驗來管理所有AEM屬性，同時確保關鍵工作流程的一致性。 這些功能包括網域名稱管理、SSL憑證管理和CDN對應。

## 將Edge Delivery Services新增到生產計畫或沙箱計畫

若要新增或編輯程式，您必須是&#x200B;**企業所有者**&#x200B;角色的成員或擁有執行此作業的許可權。

您的組織必須先擁有未使用的Edge Delivery Services授權，才能將其套用至生產計畫。

>[!NOTE]
>
>一旦Edge Delivery Services授權套用至計畫或從計畫中移除，變更就會立即生效，而無需執行管道。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

根據您的使用案例，執行下列任一項作業：

| 使用案例 | 說明 |
| --- | --- |
| 我想將Edge Delivery Services新增到新的生產計畫。 | 請參閱[建立生產計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。<br>在精靈中的&#x200B;**解決方案和附加元件**&#x200B;標籤下，選取&#x200B;**Edge Delivery Services**。 |
| 我想將Edge Delivery Services新增到現有的生產計畫。 | 請參閱[編輯程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。<br>在&#x200B;**編輯程式**&#x200B;對話方塊的&#x200B;**解決方案和附加元件**&#x200B;索引標籤下，選取&#x200B;**Edge Delivery Services**。 |
| 我想將Edge Delivery網站新增至Cloud Manager | 請參閱[新增Edge Delivery網站](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)。 |
| 我想將Edge Delivery Services新增到新的或現有的沙箱計畫。 | 請參閱[建立沙箱計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)。<br>當您建立沙箱計畫時，預設會將Edge Delivery Services新增到計畫中；您不需要選取它。<br>在Edge Delivery正式發行之前的現有沙箱計畫，會自動繼承Edge Delivery Services。 |

## 為簽約客戶Adobe建議路徑 {#recommended-path-eds}

身為合約客戶，請透過Cloud Manager存取及使用您的Adobe授權，確保您從Edge Delivery Services中獲得最大利益。 此方法可讓您使用[Adobe受管理的CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)，並利用自助式CDN管理等關鍵優點，包括設定和增加DV憑證。 此外，建立DV憑證後，Adobe會每三個月自動更新一次（除非憑證被刪除）。 如果您沒有Adobe的Edge Delivery Services授權，並決定略過這些權益，您只能使用客戶管理的CDN。 此安裝程式必須在`aem.live`平台上。

如果您是與AEM as a Cloud Service SitesEdge Delivery Services授權簽約者，請登入Cloud Manager以確保您能夠執行下列動作：

* 使用您所選程式的授權。
* 利用[API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/)的優勢執行CRUD （建立、讀取、更新、刪除）作業。
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* 存取SLA報告（*即將推出*） <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* 獲得Adobe支援。 請確定您的Edge Delivery Services網站已透過Cloud Manager中的生產計畫註冊，以獲得Adobe的適當認可和支援。


## 關於Edge Delivery待辦事項清單 {#ed-todo-list}

**Edge Delivery待辦事項清單**&#x200B;是入門工作檢查清單，旨在引導您完成入門、管理您的Edge Delivery網站直到[上線](/help/journey-onboarding/go-live-checklist.md)。

![Edge Delivery網站待辦事項清單](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|  | 任務 | 說明 |
| --- | --- | --- |
| 1 | 加入產品協作頻道 | 按一下&#x200B;**立即提交請求**&#x200B;提交請求給Adobe以建立貴公司的管道。 如果頻道已存在，則會將您轉送到公司的頻道。 |
| 2 | 完成先決條件 | 按一下&#x200B;**檢視快速入門教學課程**，會將您導向[快速入門 — 開發人員教學課程](https://www.aem.live/developer/tutorial)。 |
| 3 | 新增Edge Delivery網站 | 請參閱[新增Edge Delivery網站](#eds-add-site)。 |
| 4 | 新增網域 | 請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 |
| 5 | 新增 SSL 憑證 | 請參閱[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 |
| 6 | 設定Edge Delivery網站的CDN | 請參閱[新增CDN組態](#add-cdn)。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->

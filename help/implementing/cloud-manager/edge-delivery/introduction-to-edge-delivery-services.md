---
title: Cloud Manager 的 Edge Delivery Services 簡介
description: 了解如何使用 Edge Delivery Services 傳遞您的 Cloud Manager 專案。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 897f6376c594604527231f6f5a05a8b85d6858f3
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 100%

---


# Cloud Manager 的 Edge Delivery Services 簡介 {#edge-delivery-services}

Edge Delivery Services 是一組可組合的服務，可讓您以高度靈活的方式在網站上製作內容。此功能可讓您執行以下操作：

* 建立具有完美 Lighthouse 分數的快速網站。
* 透過操作遙測持續監視效能。
* 透過分離內容來源提高編寫工作效率。

您可以透過通用編輯器與文件型製作來使用 AEM 內容管理和所見即所得製作。

AEM as a Cloud Service 中的 Cloud Manager 可讓您為專案啟用 Edge Delivery Service。

>[!TIP]
>
>有關 Edge Delivery Service 及其如何與 AEM 搭配使用的詳細資訊，請參閱 [Edge Delivery Services 概觀](/help/edge/overview.md)。

## 關於 Cloud Manager 中的 Edge Delivery Services {#edge-in-cloud-manager}

如果您已在 Adobe Experience Manager Sites 中獲得 Edge Delivery Services 授權，現在可以直接在 Cloud Manager 中使用 Edge Delivery Services 讓您的網站上線，並[使用引導式自助服務體驗](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)來啟用網站。

此外，您還可以獲得整合的體驗來管理所有 AEM 屬性，同時確保重要工作流程的一致性。這些工作流程包括網域名稱管理、SSL 憑證管理和內容傳遞網路對應。

## 將 Adobe 建議路徑用於 Edge Delivery Services 的優勢 {#recommended-path-eds}

透過 Cloud Manager 存取和使用您的 Edge Delivery Services 授權，藉此將 Adobe 的優勢提升至最高。這樣做可讓您善用幾個主要優勢。

* [使用您選擇之程式的授權](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)，或[更新其他程式](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md)，或者兩者兼具。
* 善用 [API 優先](https://developer.adobe.com/experience-cloud/experience-manager-apis/)優勢來執行 CRUD (建立、讀取、更新、刪除) 操作。
* [存取 SLA 報告](/help/implementing/cloud-manager/reports/report-sla.md)
* 為您註冊的生產程式[獲取 Adobe 支援](/help/edge/overview.md#support-ticket)。

如果擁有 Edge Delivery Services (EDS) 授權，則可以在您的 Edge Delivery 網站上使用 [Adobe 管理的內容傳遞網路](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)。這樣做可啟用自助式內容傳遞網路管理，以及每三個月自動續約的 DV 憑證，除非您刪除該憑證。

或者，如果您選擇使用您的 CDN (即非 Adobe 託管的 CDN)，無論您的 Edge Delivery Services 授權情形如何，您都必須在 `aem.live` 平台上對其進行設定。請參閱 [BYO CDN 設定](https://www.aem.live/docs/byo-cdn-setup)。


## 關於在生產程式或沙箱程式新增 Edge Delivery Services

根據專案的開始方式或是預計建立網站的時間，您可以透過多種不同方法新增 Edge Delivery Services。

| 使用案例 | 描述 |
| --- | --- |
| 我想將 Edge Delivery Services 新增到新的生產程式中。 | 請參閱[建立生產程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。<br>在精靈中，於「**解決方案與附加元件**」索引標籤下方，選取「**Edge Delivery Services**」。 |
| 我想將 Edge Delivery Services 新增到現有的生產程式中。 | 請參閱[編輯程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。<br>在「**編輯程式**」對話框中，於「**解決方案與附加元件**」索引標籤下方，選取「**Edge Delivery Services**」。 |
| 我想要新增 Edge Delivery 網站至 Cloud Manager | 請參閱[新增 Edge Delivery 網站](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)。 |
| 我現在要建立一個 Edge Delivery 網站 | 請參閱「[透過點選按鈕在 Cloud Manager 中快速建立 Edge Delivery 網站](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)」。 |
| 我想將 Edge Delivery Services 新增到新的或現有的沙箱程式中。 | 請參閱[建立沙箱程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)。<br>建立沙箱程式時，預設會將 Edge Delivery Services 新增至該程式；您不需要選取它。<br>在 Edge Delivery 全面推出之前，現有的沙箱程式會自動繼承 Edge Delivery Services。 |

>[!NOTE]
>
>* 若要新增或編輯程式，您必須是&#x200B;**業務負責人**&#x200B;角色的成員，或具有執行此操作的權限。
>* 您的組織必須擁有未使用的 Edge Delivery Services 授權，然後才能將其套用至生產程式。
>* 將 Edge Delivery Services 授權套用至程式中或從程式中移除後，變更會立即生效，無需執行管道。


## 關於 Cloud Manager 中的 Edge Delivery 待辦事項清單 {#ed-todo-list}

<!-- &#x2460; for "1" inside circle -->

Cloud Manager 中的 **Edge Delivery 待辦事項清單**&#x200B;是上線任務檢查清單，目的為全程引導您上線，管理您的 Edge Delivery 網站一直到[上線](/help/journey-onboarding/go-live-checklist.md)。

![Cloud Manager 中的 Edge Delivery 網站待辦事項清單](/help/implementing/cloud-manager/assets/cm-eds-todo-list.png)

|   | 任務 | 描述 |
| --- | --- | --- |
| 1 | 加入生產共同作業管道 | 按一下「**立即提交請求**」，向 Adobe 提交為貴公司建立管道的請求。如果管道已存在，會將您轉至貴公司的管道。 |
| 2 | 完成先決條件 | 請參閱「[檢視快速入門教學課程](https://www.aem.live/developer/tutorial)」。 |
| 3 | 新增 Edge Delivery 網站或<br>立即建立網站 | 請參閱「[新增 Edge Delivery 網站](#eds-add-site)」。<br>請參閱「[在 Cloud Manager 中建立 Edge Delivery 網站](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)」。 |
| 4 | 設定 Edge Delivery 網站以使用外部 Git 存放庫 | 請參閱[設定 Edge Delivery 網站以使用外部 Git 存放庫](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md)。 |
| 5 | 新增網域 | 請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 |
| 6 | 新增 SSL 憑證 | 請參閱[新增 SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 |
| 7 | 設定您 Edge Delivery 網站的內容傳遞網路 | 請參閱[新增網域對應](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。 |
| 8 | 設定推播驗證 | 請參閱「[為 Edge Delivery 網站設定推播驗證](/help/implementing/cloud-manager/edge-delivery/cdn-setup-push-invalidation.md)」。 |
| 9 | 上線 | 請參閱「[上線檢查清單](https://www.aem.live/docs/go-live-checklist)」。 |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## 記錄支援服務單 {#eds-support-ticket}

{{support-ticket}}




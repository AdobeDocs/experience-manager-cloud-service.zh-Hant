---
title: Cloud Manager 的 Edge Delivery Services 簡介
description: 了解如何使用 Edge Delivery Services 傳遞您的 Cloud Manager 專案。
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 71d514b2eaf83732cc0856f6b508ab814fe7f469
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 56%

---


# Cloud Manager 的 Edge Delivery Services 簡介 {#edge-delivery-services}

Edge Delivery Services 是一組可組合的服務，可讓您以高度靈活的方式在網站上製作內容。此功能可讓您執行以下操作：

* 建立具有完美 Lighthouse 分數的快速網站。
* 透過操作遙測持續監視效能。
* 透過分離內容來源提高編寫工作效率。

您可以透過通用編輯器與文件型製作來使用 AEM 內容管理和所見即所得製作。

AEM as a Cloud Service中的Cloud Manager可讓您為專案啟用Edge Delivery服務。

>[!TIP]
>
>有關 Edge Delivery Service 及其如何與 AEM 搭配使用的詳細資訊，請參閱 [Edge Delivery Services 概觀](/help/edge/overview.md#how-does-it-work)。

## 關於 Cloud Manager 中的 Edge Delivery Services {#edge-in-cloud-manager}

如果您已在 Adobe Experience Manager Sites 中獲得 Edge Delivery Services 授權，現在可以直接在 Cloud Manager 中使用 Edge Delivery Services 讓您的網站上線，並[使用引導式自助服務體驗](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)來啟用網站。

此外，您還可以獲得整合的體驗來管理所有 AEM 屬性，同時確保重要工作流程的一致性。這些工作流程包括網域名稱管理、SSL 憑證管理和內容傳遞網路對應。

Cloud Manager為Adobe Managed CDN中的Edge Delivery Services提供兩種部署型別，且具有不同功能。 [了解更多](#edge-delivery-deployment-options)。

>[!NOTE]
>
>Edge Delivery Services也可以使用設定管道和來源選擇器整合到現有AEM Sites as a Cloud Service環境中。 如需詳細資訊，請參閱[代理至Edge Delivery Services](/help/implementing/dispatcher/cdn-configuring-traffic.md#proxying-to-edge-delivery)和[從現有環境設定Proxy](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment)。

## Adobe Managed CDN中的Edge Delivery Services部署選項 {#edge-delivery-deployment-options}

Adobe Managed CDN中Edge Delivery Services有兩種部署型別：

1. **使用現有的AEMaaCS環境** — 從現有的AEM Sites as a Cloud Service環境設定HTTP Proxy。 如果您已有現有的環境，而且想要將網站的部分內容移轉至Edge Delivery Services，通常就會使用此方法。 請參閱[從現有環境設定Proxy](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment)。

1. **沒有現有的AEMaaCS環境（Edge環境）** — 獨立於AEM Sites as a Cloud Service環境設定新的Edge Delivery網站。 如果您沒有AEM製作或發佈環境，而且想要自行使用Edge Delivery Services，您可使用這種方法。 請參閱[在沒有現有環境的情況下設定Edge Delivery網站](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment)。

這兩個選項也有不同的功能：

* **設定管道**&#x200B;可用於AEM as a Cloud Service環境。
* **設定管道**&#x200B;目前只能透過有限的Beta程式提供給Edge環境使用。

如需完整的設定指示，請參閱[Adobe Managed CDN](https://www.aem.live/docs/byo-cdn-adobe-managed)


## 關於具有AEM製作功能的Edge Delivery Services (Beta) {#eds-aem-authoring}

>[!NOTE]
>
>此處說明的彈性發佈層級和AEM編寫行人穿越道功能位於Beta。 若要加入Beta，請使用您的Adobe組織ID和計畫ID透過電子郵件傳送[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)。

現代的Web體驗需要高效能傳遞，但許多組織也仰賴既有的AEM製作工作流程、控管和內容重複使用模式。 為協助您的團隊在不中斷編寫的情況下實現傳送現代化，Cloud Manager推出可讓您進行下列操作的功能：

* 使用Edge Delivery Services提供體驗。
* 繼續使用AEM Author建立內容。
* 僅布建架構所需的基礎架構。

這些功能可讓組織逐步採用現代化遞送，而不會犧牲現有的工作流程。

### Edge Delivery網站的製作選項 {#authoring-options-eds}

在Cloud Manager中建立Edge Delivery網站時，您可以選擇慣用的撰寫方法：

* 檔案式製作 — 在Google Drive或SharePoint中製作內容。 不需要AEM環境。
* AEM製作 — 使用通用編輯器在AEM中製作內容。 此方法需要AEM製作環境。 使用此選項，當Edge Delivery處理內容傳遞時，不需要發佈階層。

組織可以根據其工作流程偏好設定，選擇或遞增使用這兩種方法。 請參閱[按一下即可建立您的第一個Edge Delivery網站](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)。

### 彈性的發佈階層 {#flexible-publish-tier}

Cloud Manager可讓您設定是否針對您的方案環境布建發佈層級。 並非所有架構都需要發佈階層，如下表所示：

| 架構 | 發佈階層 |
| --- | --- |
| 傳統AEM Sites | 必要 |
| Headless / API優先 | 必要 |
| Edge Delivery Services | 非必要 |

透過只在需要時啟用發佈層級，團隊可以更快速地布建環境、簡化基礎建設，以及減少不必要的元件。 請參閱[彈性發佈階層(Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)。

## 將 Adobe 建議路徑用於 Edge Delivery Services 的優勢 {#recommended-path-eds}

透過 Cloud Manager 存取和使用您的 Edge Delivery Services 授權，藉此將 Adobe 的優勢提升至最高。這樣做可讓您善用幾個主要優勢。

* [使用您選擇之程式的授權](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)，或[更新其他程式](/help/implementing/cloud-manager/edge-delivery/manage-edge-delivery-sites.md)，或者兩者兼具。
* [使用外部Git存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md) （自備Git）來同步和部署您的Edge Delivery Services網站程式碼。 若要運用此功能，您必須先在Cloud Manager[中](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)加入您的網站。<!-- NEW from CQDOC-22867 -->
* [使用Edge Delivery Config Pipeline](/help/implementing/dispatcher/cdn-configuring-traffic.md)，定義流量篩選器、來源選取器和重新導向等規則，為您的Edge Delivery網站設定Adobe管理的CDN設定。<!-- NEW from CQDOC-22867 -->
* 善用 [API 優先](https://developer.adobe.com/experience-cloud/experience-manager-apis/)優勢來執行 CRUD (建立、讀取、更新、刪除) 操作。
* [存取SLA報告](/help/implementing/cloud-manager/reports/report-sla.md)。
* 為您註冊的生產程式[獲取 Adobe 支援](/help/edge/overview.md#support-ticket)。

如果擁有 Edge Delivery Services (EDS) 授權，則可以在您的 Edge Delivery 網站上使用 [Adobe 管理的內容傳遞網路](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)。這樣做可啟用自助式內容傳遞網路管理，以及每三個月自動續約的 DV 憑證，除非您刪除該憑證。

或者，如果您選擇使用您的 CDN (即非 Adobe 託管的 CDN)，無論您的 Edge Delivery Services 授權情形如何，您都必須在 `aem.live` 平台上對其進行設定。請參閱 [BYO CDN 設定](https://www.aem.live/docs/byo-cdn-setup)。


## 關於在生產程式或沙箱程式新增 Edge Delivery Services {#about-adding-eds-to-prod-sandbox}

根據專案的開始方式或是預計建立網站的時間，您可以透過多種不同方法新增 Edge Delivery Services。

| 使用案例 | 描述 |
| --- | --- |
| 我想將 Edge Delivery Services 新增到新的生產程式中。 | 請參閱[建立生產程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。<br>在精靈中，於「**解決方案與附加元件**」索引標籤下方，選取「**Edge Delivery Services**」。 |
| 我想將 Edge Delivery Services 新增到現有的生產程式中。 | 請參閱[編輯程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)。<br>在「**編輯程式**」對話框中，於「**解決方案與附加元件**」索引標籤下方，選取「**Edge Delivery Services**」。 |
| 我想要新增 Edge Delivery 網站至 Cloud Manager | 請參閱[新增 Edge Delivery 網站](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)。 |
| 我現在要建立一個 Edge Delivery 網站 | 請參閱「[透過點選按鈕在 Cloud Manager 中快速建立 Edge Delivery 網站](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)」。 |
| 我想將 Edge Delivery Services 新增到新的或現有的沙箱程式中。 | 請參閱[建立沙箱程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)。<br>建立沙箱程式時，預設會將 Edge Delivery Services 新增至該程式；您不需要選取它。<br>在 Edge Delivery 全面推出之前，現有的沙箱程式會自動繼承 Edge Delivery Services。 |
| 我想要建立使用AEM製作的Edge Delivery網站 | 請參閱[建立Edge Delivery網站](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site)。 搭配Edge Delivery使用AEM製作時，發佈層級為選用。 請參閱[彈性發佈階層(Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)。 |

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

>[!VIDEO](https://video.tv.adobe.com/v/3441574?captions=chi_hant&learn=on)

## 記錄支援服務單 {#eds-support-ticket}

{{support-ticket}}




---
title: Cloud Manager 2026.4.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2026.4.0 版的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: aa8aba7f798e251c8a25ee247402e23517707e88
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 20%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2026.4.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2026.4.0 的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2026.4.0發行日期是2026年4月2日星期四。

下一個預計發行日期為2026年5月7日星期四。


## 新增功能 — Cloud Manager {#cloud-manager-whats-new}

* 用於AI支援的IDE的&#x200B;**Cloud Manager MCP伺服器**

  您現在可以使用MCP （模型內容通訊協定）伺服器，將Cloud Manager公用API公開為啟用AI的IDE （例如游標）的工具。 連線後，您可以使用對話式提示來列出和管理計畫、管道、環境和存放庫，幫助您在不離開編輯器的情況下更快速地移動。

  請參閱檔案[搭配AEM as a Cloud Service使用MCP](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)。

  請參閱教學課程[Cloud Manager MCP伺服器](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager#)。

* 使用模組快取加快建置速度&#x200B;**&#x200B;**

  新的建置模型會使用模組層級快取來編譯已變更的模組 (而非整個存放庫)，藉此縮短建置時間。 它適用於計畫碼品質非生產管道和開發完整棧疊非生產管道。

  請參閱[關於在非生產管道中使用Smart Build](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build)和[新增非生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。

* **自助式主機連線檢查**

  Cloud Manager現在可讓您從環境執行自助檢查。 這些檢查會驗證主機和連線埠的可達性，並使用您程式設定的網路路徑（包括輸出）確認DNS解析。 此功能可協助您驗證進階網路並更快解決整合問題，無需開啟支援案例或存取Pod。<!-- SKYOPS-23640 -->

  請參閱[網路連線測試](/help/security/network-connectivity-test.md)

* **改善穩定性、效能和可靠性**

  此版本包含最佳化和維護更新，改善了Cloud Manager的穩定性、效能和可靠性。


## Beta 版方案 {#private-beta-program}

參與 Cloud Manager 的 Beta 版方案享有獨家存取權，在即將推出的功能正式發佈之前搶先體驗。

>[!IMPORTANT]
>
>Beta發行版本可能包含瑕疵，並依「現況」提供，並無任何保固。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援（透過Adobe支援服務或其他方式）測試版。 Adobe建議客戶謹慎行事，不要依賴Beta版正確運作或效能，或依賴任何隨附的檔案或資料。 Beta版中的功能和API可能會有所變更，恕不另行通知。 因此，使用測試版完全由客戶自行承擔風險。

另請參閱[AEM Beta計畫](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

目前提供下列機會：

### Edge Delivery Services搭配AEM製作和彈性的發佈層設定 {#eds-with-aem-authoring}

Cloud Manager引進兩項功能，旨在支援現代化的傳遞架構。

* **具有AEM製作功能的Edge Delivery Services**
您現在可以使用Edge Delivery Services傳送網站，同時繼續在AEM作者模式中作者內容。 根據您的工作流程偏好設定，您可以選擇下列編寫方法：

   * 文件型編寫
   * AEM以作者為基礎的製作

如需詳細資訊，請參閱[在Cloud Manager中建立Edge Delivery網站](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site)。

* **彈性發佈層設定**

Cloud Manager現在可讓您設定您的程式是否需要發佈階層。 此彈性可讓您設定更符合您所選傳送架構的環境。

如需詳細資訊，請參閱[彈性發佈階層(Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)。

若要加入Beta，請使用您的Adobe組織ID和計畫ID透過電子郵件傳送[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)。

### 模組快取能加快建置速度 {#quick-build-cm-pipelines}

新的建置模型會使用模組層級快取來編譯已變更的模組（而非整個存放庫），以縮短建置時間。 其適用於生產管道。 您控制哪些生產管道使用&#x200B;**智慧型組建**。

如需詳細資訊，請參閱下列內容：

* [在生產管道中使用Smart Build](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build)。
* [新增生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。

若要加入Beta，請使用您的Adobe組織ID和計畫ID透過電子郵件傳送[beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com)。

<!-- 
OLD
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

<!-- 
OLD
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.
-->



## 錯誤修正 {#bug-fixes}

2026年4月發行的Cloud Manager沒有重大錯誤修正。

<!-- ## Known issues {#known-issues} -->


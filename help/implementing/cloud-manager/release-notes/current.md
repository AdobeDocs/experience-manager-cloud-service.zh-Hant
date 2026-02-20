---
title: Cloud Manager 2026.1.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2026.1.0 版的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2ea076c42a6406548bf48cd246227fc8ddb3a080
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 43%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2026.1.0 版的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2026.1.0 版的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2026.1.0發行日期是2026年1月22日星期四。

下一個預計發行日期為2026年2月5日星期四。

## 新增功能 — Cloud Manager {#cloud-manager-whats-new}

* **設定管道現在支援受管理的密碼**

  使用者現在可以直接在Cloud Manager設定管道中新增和管理秘密。 這些秘密會安全地覆寫管道設定規格中的值，並支援彈性、特定於環境的部署。

  所選管道的下拉式選單上的![檢視/編輯變數選項](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-option.png)
  所選管道的下拉式選單上的&#x200B;*檢視/編輯變數選項。*

  ![變數設定對話方塊&#x200B;](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-variablesconfig-dialogbox.png)*變數設定對話方塊。*

* **改善穩定性、效能和可靠性**

  此版本包含最佳化和維護更新，改善了Cloud Manager的穩定性、效能和可靠性。




## Beta 版方案 {#private-beta-program}

參與 Cloud Manager 的 Beta 版方案享有獨家存取權，在即將推出的功能正式發佈之前搶先體驗。

>[!IMPORTANT]
>
>Beta發行版本可能包含瑕疵，並依「現況」提供，並無任何保固。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援(透過Adobe支援服務或其他方式)測試版。 Adobe建議客戶謹慎行事，不要依賴Beta版正確運作或效能，或依賴任何隨附的檔案或資料。 Beta版中的功能和API可能會有所變更，恕不另行通知。 因此，使用測試版完全由客戶自行承擔風險。

另請參閱[AEM Beta計畫](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

目前提供下列機會：
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### Experience Hub 的擴展性和自訂 {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) 是您存取 AEM 的入口點，並可根據組織需求進行自訂。告知 Adobe 您現有的 AEM 使用者介面擴充功能，以便協助您花最少的力氣便能在 Experience Hub 中啟用這些功能。

![Experience Hub 擴展性與自訂工作流程的圖表](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

在 Experience Hub 中嵌入自訂體驗，以擴充組織儀表板的功能以及進行個人化設定。除了 Adobe 的內建小工具之外，您可以使用[使用者介面擴展性](https://developer.adobe.com/uix/docs/)框架自行新增小工具。建置以 JavaScript 為基礎的使用者介面應用程式，並將其呈現給您的使用者，以滿足特定業務需求和工作流程。

有興趣使用 Beta 版嗎？請寄送電子郵件至 [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com)，附上您的 Adobe OrgID 並簡短說明您想要算建立的自訂內容。

### 模組快取能加快建置速度 {#quick-build-cm-pipelines}

新的建置模型會使用模組層級快取來編譯已變更的模組 (而非整個存放庫)，藉此縮短建置時間。此建置模型適用於程式碼品質、完整堆疊和僅限中繼管道。

![編輯非生產管道對話方塊，其中顯示兩個建置策略選項，即Full Build和Smart Build](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*編輯非生產管道對話方塊，其中顯示兩個建置策略選項：完整建置和智慧型建置。*

在&#x200B;**新增/編輯管道**&#x200B;對話方塊的&#x200B;**Source程式碼**&#x200B;索引標籤下方，新的&#x200B;**建置策略**&#x200B;區段可讓您選擇下列其中一個建置選項：

* **完整組建** — 每次執行都會建置存放庫中的所有模組。
* **智慧型組建** — 僅建置自上次認可後變更的模組，這會縮短整體建置時間。

您控制哪些管道使用&#x200B;**智慧型組建**。 在Beta版期間，此選項僅針對&#x200B;**程式碼品質**&#x200B;和&#x200B;**開發部署**&#x200B;管道顯示。

感興趣嗎？請寄送電子郵件至 [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com)，並附上您的 Adobe OrgID 和方案 ID。

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

## 錯誤修正 {#bug-fixes}

2025年12月Cloud Manager版本沒有重大錯誤修正。


<!-- ## Known issues {#known-issues} -->


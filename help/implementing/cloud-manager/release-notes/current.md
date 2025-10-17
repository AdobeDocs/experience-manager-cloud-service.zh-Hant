---
title: Cloud Manager 2025.10.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.10.0 版的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 85784a9611bc6f83a1d70b66ff7087117aa7ec0b
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 89%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.10.0 版的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.10.0 版的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中 Cloud Manager 2025.10.0 版的發行日期是 2025 年 10 月 2 日 (星期四)。

下一個版本計劃於 2025 年 11 月 6 日 (星期四) 發行。

## 新增功能 {#what-is-new}

* **專用的僅限中繼和僅限生產的部署管道**

  Cloud Manager現在提供專用的僅限中繼和生產環境部署管道，提供更強大的彈性，可獨立管理至中繼和生產環境的部署。 請參閱[分割僅限階段和僅限生產的管道](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md)。

* **AEM 雲端健康狀態評估服務**

  Adobe 推出 AEM 雲端健康狀態評估服務，這是一項自動化、非侵入性的檢查工具，能讓您的 AEM as a Cloud Service 環境保持最佳化、安全並符合最佳做法的狀態。

  此服務會執行下列動作：

   * 掃描各個環境，找出效能瓶頸、效率不彰之處和潛在風險。
   * 分析內容結構 (Blueprint、Live Copy) 和自訂設定。
   * 找出過時的相依性 (AEM SDK、第三方程式庫)。
   * 標示程式碼品質問題 (註解錯誤、模式效率不彰)。
   * 透過儀表板 (例如&#x200B;**動作中心**) 提供可操作的指引。
   * 透過及早發現問題並進行修復，支援主動式最佳化。

  團隊可以持續監視和改善其 AEM 環境，以達到更順暢的效能、更強大的安全性和長期可維護性。

  請參閱[生產和中繼環境的健康狀態評估](/help/implementing/cloud-manager/reports/report-health-assessment.md)。

* **設定管道支援**

  現在，使用 Edge Delivery Services 建置的網站支援設定管道，因此在 Cloud Service 環境以外也能使用這項功能。您可以使用&#x200B;**設定管道**&#x200B;管理設定，例如內容傳遞網路設定，包括流量篩選器規則和來源選擇器。請參閱[支援的設定](/help/operations/config-pipeline.md#configurations)。

  Edge Delivery 設定管道也能透過 Cloud Manager 管道變數支援密碼。

  請參閱[新增 Edge Delivery 管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)。

* **網域對應內容傳遞網路的設定對話框已簡化**

  Cloud Manager 已簡化&#x200B;**將網域對應至內容傳遞網路**&#x200B;的流程，以減少混淆情形並加快設定速度。對話框現在特別凸顯「**Adobe 管理的內容傳遞網路**」(帶有「建議」標籤)。

  ![「將網域對應至內容傳遞網路」對話框，其中已選取「Adobe 管理的內容傳遞網路」選項按鈕](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png)。

  請參閱[新增網域對應](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。

  對話框也會針對&#x200B;**其他內容傳遞網路提供者**&#x200B;卡片顯示一份簡潔的檢查清單，並著重下列內容的操作說明：

   * 將您的內容傳遞網路來源指向 `publish-p<PROGRAM_ID>-e<ENV_ID>.adobeaemcloud.com`。
   * 設定&#x200B;**主機/SNI** 以便轉寄原始主機。
   * 新增 `X-AEM-Edge-Key` (在 Cloud Manager 中部署金鑰之後)。
   * 將 `X-Forwarded-Host` 設定為面向客戶的網域。
   * 在到達 AEM 前，清除其他 `X-Forwarded-*` 標頭。

  ![「將網域對應至內容傳遞網路」對話框，其中已選取「其他內容傳遞網路提供者」選項按鈕](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-other-cdn-provider.png)

  <!-- (no redundant `Origin` field or "Learn more" clutter) -->隨附的頁尾提供兩個實用連結：主要內容傳遞網路的設定範例以及完整文件的連結。透過一個確認按鈕「我已設定我的內容傳遞網路」完成整個流程。

  請參閱 [AEM as a Cloud Service 中的內容傳遞網路](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)。

<!--
### Staging-Only and Production-Only Pipelines {#staging-production-only-pipelines}

Support for [staging-only and production-only pipelines](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md) has been introduced, enabling you to split full-stack production deployment pipelines into smaller, specialized deployments.

If you are interested in testing this new feature and sharing your feedback, send an email to  `Grp-cloudmanager_splitpipelines@adobe.com` from your email address associated with your Adobe ID. -->


## Beta 版方案 {#private-beta-program}

參與 Cloud Manager 的 Beta 版方案享有獨家存取權，在即將推出的功能正式發佈之前搶先體驗。

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



### 管道部署的一鍵復原 {#one-click-rollback}

如果最新的客戶原始程式碼未按預期運作，則會快速還原至先前的部署，無需重新執行完整管道或手動恢復認可。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![從「環境」卡片還原客戶原始程式碼](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *上方的「環境」卡片顯示所選環境的「**還原**」>「**先前部署的程式碼**」選項。*

![「還原先前部署的程式碼」對話框](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*在「**還原先前部署的程式碼**」對話框中，檢閱目前部署的版本和要還原的版本，然後按一下「**確認***」。

![還原啟用](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager 會將環境還原至先前的建置、將內容和設定保持不變，並將環境標記為&#x200B;**還原中**，直到部署完成。*

![使用中的原始程式碼版本](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *環境詳細資料檢視 (如上所示) 現在也顯示使用中的原始程式碼版本。*

如果您有興趣測試這個新功能並分享意見回饋，請使用與您的 Adobe ID 關聯的電子郵件地址，寄送電子郵件至 [restorecode@adobe.com](mailto:restorecode@adobe.com)。

請參閱[還原 AEM as a Cloud Service 中先前部署的程式碼](/help/operations/restore-previous-code-deployed.md)。

另請參閱 [AEM as a Cloud Service 中的內容還原](/help/operations/restore.md)。

### 專用測試環境 {#specialized-test-environment}

Cloud Manager 現在支援新增名為&#x200B;**專用測試環境**&#x200B;的新環境類型。這類環境的目的為幫助團隊於正式上線之前，在接近生產的條件狀況下驗證功能。此環境類型不同於&#x200B;*生產 + 中繼*、*開發*&#x200B;或&#x200B;*快速開發*&#x200B;環境，其為執行進階的驗證情境提供一個集中的空間。

**最近的增強功能**

* 您現在可以透過更簡單、更直覺易用的工作流程，在非生產管道上設定專用的測試環境。簡化的設定可加速完成並減少設定錯誤。
* 專用的測試環境現在支援&#x200B;**複製內容**。您現在可以在鏡像生產環境的獨立測試環境中安全地執行&#x200B;**複製內容**&#x200B;功能。<!-- (CMGR‑68900) -->

請參閱[新增專用測試環境](/help/implementing/cloud-manager/specialized-test-environment.md)。

![以選取的專用測試環境選項按鈕新增環境對話框：](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

>[!NOTE]
>
>Adobe 已關閉對於專用測試環境的 Beta 版存取請求，目前已獲得足夠多的參與者。該功能目前正在準備全面推出。

<!--
If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


### 自備 Git (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客戶現在可以將其 Azure DevOps Git 存放庫加入 Cloud Manager 中，並同時支援現代 Azure DevOps 和舊版 VSTS (Visual Studio Team Services) 存放庫。

* Edge Delivery Services 使用者可以使用所加入的存放庫來同步處理及部署網站程式碼。
* AEM as a Cloud Service 和 Adobe Managed Services (AMS) 使用者可以將此存放庫連結至全堆疊以及前端管道。

即將推出對更多管道類型的支援以及透過程式碼品質管道驗證提取要求的功能。

請查看[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![Add Repository dialog box](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

**關於 BYOG 的常見問題集**

| 問題 | 答案 |
|---|---|
| *如有必要，專案如何切換回 Adobe 管理的 Git 存放庫？* | 切換回來是很簡單直覺的操作。[更新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)使其指向 Adobe 存放庫並移除不再需要的外部存放庫。 |
| *是否可能針對不同環境 (例如非生產環境和生產環境) 設定不同的存放庫，以便先在非生產環境中進行測試？* | 是的，可以為不同的環境設定不同存放庫。例如，開發或程式碼品質管道可以指向外部存放庫，而生產管道與 Adobe 存放庫保持連線。在此設定期間，請確保兩個存放庫之間的同步作業保持「使用中」狀態。 |
| *`IP Allow` 清單等現有設定是否會繼續運作？* | 是的，現有的 `IP Allow` 清單會繼續照常運作。但是，如果外部 Git 存放庫受防火牆保護，則必須將必要的 [Adobe IP 位址新增至允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有 GitLab 存放庫 URL 是否均可運作？使用中的存放庫 URL 遵循 `https://gitlab_dedicated_url.com/path/repo-name.git` 格式，與文件中的範例不同。* | 是的，支援所有支援 API V3 或 V4 的 GitLab 存放庫，包括自行託管的 GitLab URL，例如[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`) 中所說明的 URL。 |


#### 管理存取權杖{#manage-access-tokens}

使用 Cloud Manager 中的&#x200B;**管理存取權杖**，檢視、重新命名及刪除與外部 BYOG 存放庫 (例如 GitHub Enterprise、GitLab、Bitbucket 和 Azure DevOps) 關聯的存取權杖。

請參閱[管理存取權杖](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


## 錯誤修正 {#bug-fixes}

10 月的 Cloud Manager 版本沒有重大錯誤修正。


<!-- ## Known issues {#known-issues} -->


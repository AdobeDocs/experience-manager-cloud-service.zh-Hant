---
title: Cloud Manager 2025.10.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.10.0 版的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 4acedba631b3732b989794c648079356f9b79fdd
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 62%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.10.0 版的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.10.0 版的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.10.0發行日期是2025年10月2日星期四。

下一個預計發行日期為2025年11月6日星期四。

## 新增功能 {#what-is-new}

* **AEM雲端健康情況評估服務**

  Adobe推出AEM雲端健康評估服務，這是一個自動化、非侵入性的檢查工具，可讓您的AEM as a Cloud Service環境保持最佳化、安全並符合最佳實務。

  此服務會執行下列動作：

   * 掃描環境，找出效能瓶頸、低效和潛在風險。
   * 分析內容結構（藍圖、即時副本）和自訂設定。
   * 識別過時的相依性(AEM SDK、協力廠商程式庫)。
   * 標示程式碼品質問題（註解錯誤、模式效率低下）。
   * 透過儀表板（例如&#x200B;**動作中心**）提供可操作的指引。
   * 透過早期問題偵測和補救，支援主動最佳化。

  團隊可以持續監控和改善其AEM環境，以實現更順暢的效能、更強大的安全性和長期可維護性。

  請參閱[生產和中繼環境的健康狀態評估](/help/implementing/cloud-manager/reports/report-health-assessment.md)。

* **設定管道支援**

  現在，使用 Edge Delivery Services 建置的網站已支援設定管道，所以在 Cloud Service 環境以外也可以使用這項功能。您可以使用&#x200B;**設定管道**&#x200B;來管理設定，例如流量篩選規則和 Web 應用程式防火牆 (WAF) 設定等 (如適用)。請參閱[支援的設定](/help/operations/config-pipeline.md#configurations)。

  Edge Delivery設定管道也透過Cloud Manager管道變數支援秘密。

  請參閱[新增Edge Delivery管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)。

* **網域對應 — CDN設定對話方塊已簡化**

  Cloud Manager已簡化&#x200B;**將網域對應至CDN**&#x200B;流程，以減少混淆並加快設定。 此對話方塊現在強調&#x200B;**Adobe Managed CDN** （具有「建議」徽章）。

  ![選取Adobe管理的CDN選項按鈕時，將[網域對應至CDN]對話方塊](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png)。

  請參閱[新增網域對應](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。

  此對話方塊也會針對&#x200B;**其他CDN提供者**&#x200B;卡片提供單一、簡明的檢查清單，其重點為具有下列內容的教學內容：

   * 將您的CDN來源指向`publish-p<PROGRAM_ID>-e<ENV_ID>.adobeaemcloud.com`。
   * 設定&#x200B;**主機/SNI**&#x200B;以轉送原始主機。
   * 新增`X-AEM-Edge-Key` (在Cloud Manager中部署金鑰後)。
   * 將`X-Forwarded-Host`設為您的客戶導向網域。
   * 在到達AEM之前清除其他`X-Forwarded-*`標頭。

  ![選取其他CDN提供者選項按鈕時，將網域對應到CDN對話方塊](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-other-cdn-provider.png)

  <!-- (no redundant `Origin` field or "Learn more" clutter) -->隨附的頁尾提供兩個實用的連結：主要CDN的設定範例和完整檔案的連結。 單一確認按鈕 — 我已設定我的CDN — 完成流程。

  檢視AEM as a Cloud Service[中的](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)CDN。

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

### Experience Hub的可擴充性和自訂 {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md)是您進入AEM的入口點，並根據您組織的需求進行自訂。 告訴Adobe您現有的AEM UI擴充功能，協助您只需最省力就能在Experience Hub中啟用它們。

![Experience Hub擴充性與自訂工作流程圖表](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

在Experience Hub中內嵌自訂體驗，以擴充及個人化您的組織控制面板。 除了Adobe的內建Widget，請使用[UI擴充性](https://developer.adobe.com/uix/docs/)架構新增您自己的。 建置以JavaScript為基礎的UI應用程式，並將其呈現給您的使用者，以符合特定業務的需求和工作流程。

對Beta版感興趣嗎？ 請傳送電子郵件給[beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com)，其中包含您的Adobe OrgID以及您打算建立的自訂專案的簡短說明。

### 模組快取可加快組建速度 {#quick-build-cm-pipelines}

新的建置模型會使用模組層級快取來編譯已變更的模組（而非整個存放庫），以縮短建置時間。 它適用於計畫碼品質、完整棧疊和僅限階段的管道。

有興趣嗎？ 使用您的Adobe OrgID和方案ID以電子郵件傳送[beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com)。

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

10月發行的Cloud Manager沒有重大錯誤修正。


<!-- ## Known issues {#known-issues} -->


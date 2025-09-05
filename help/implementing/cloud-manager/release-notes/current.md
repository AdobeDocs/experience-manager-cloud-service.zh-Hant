---
title: Cloud Manager 2025.9.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.9.0 版的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 98182e835e10b0b29aa2ae21c2a02562ca64111a
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 88%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.9.0 版的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.9.0 版的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.9.0發行日期是2025年9月4日星期四。

下一個預計發行日期為2025年10月2日星期四。

## 新增功能 {#what-is-new}

* **手動續約Adobe管理的網域驗證憑證**

  您現在可以從Cloud Manager或公用API手動續約Adobe管理的網域驗證(DV)憑證，以主動重新整理憑證。<!-- CMGR-68738 -->

  ![SSL憑證續約](/help/implementing/cloud-manager/release-notes/assets/ssl-certificate-adobedv-renew.png)

* **現在已新增私人存放庫的Azure DevOps支援**

  檔案更新包含使用Azure DevOps自攜Git和提取請求驗證的設定步驟。 請參閱[在Cloud Manager中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

* **私人存放庫的提取要求檢查**

  Cloud Manager現在支援在GitHub、Bitbucket、Azure DevOps和GitLab中使用私人存放庫來設定管道。 檢視私人存放庫的[提取要求檢查](/help/implementing/cloud-manager/managing-code/github-check-config.md)。

* **Cloud Manager 新增 ECDSA (橢圓曲線數位簽名演算法) SSL 憑證支援**

  Cloud Manager 現在支援 ECDSA 憑證。此功能透過較小的金鑰提供強大的安全性，讓客戶能夠在其 CDN 設定中套用輕量版的現代加密功能。<!-- https://jira.corp.adobe.com/browse/CMGR-62399 -->

### 僅限中繼和僅限生產管道 {#staging-production-only-pipelines}

已引進[僅限中繼和僅限生產管道](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md)的支援，讓您將全端生產部署管道分割為更小的專門部署。

如果您有興趣測試此新功能並分享您的意見反應，可使用和您 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `Grp-cloudmanager_splitpipelines@adobe.com`。


## Beta 版方案 {#private-beta-program}

參與 Cloud Manager 的 Beta 版方案享有獨家存取權，在即將推出的功能正式發佈之前搶先體驗。

目前提供下列機會：
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

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

### 新增Edge Delivery設定管道 {#add-eds-pipeline}

現在，使用 Edge Delivery Services 建置的網站已支援設定管道，所以在 Cloud Service 環境以外也可以使用這項功能。您可以使用&#x200B;**設定管道**&#x200B;來管理設定，例如流量篩選規則和 Web 應用程式防火牆 (WAF) 設定等 (如適用)。請參閱[支援的設定](/help/operations/config-pipeline.md#configurations)。

**最近的增強功能**

* Edge Delivery設定管道現在透過Cloud Manager管道變數支援秘密。
* 現在，Edge Delivery Services 管道會在「**已部署程式碼**」欄中顯示「**設定**」，方便您立即識別僅限設定的部署。<!-- CMGR‑69681 -->
* 若方案包含至少一個 Edge Delivery Services 網站和一個對應的網域，Cloud Manager 便會顯示「**新增 Edge Delivery 管道**」。否則，該選項會顯示為停用，並透過工具提示說明未達到哪些要求。<!-- CMGR‑69680 -->
* 「**Edge Delivery**」索引標籤顯示一個新的 **Edge Delivery 管道**&#x200B;小工具，其中列出每個管道的名稱、狀態、存放庫和分支。<!-- (CMGR-69052) -->

  ![Edge Delivery 管道小工具顯示管道名稱、狀態、存放庫和分支](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* 「**篩選器**」面板新增「**傳遞類型**」區段；其中包括「**邊緣傳遞**」和「**發佈傳遞**」核取方塊。<!-- (CMGR-69682) -->

  ![篩選器面板顯示新的傳遞類型包括邊緣傳遞與發佈傳遞](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *從&#x200B;**計劃概觀**頁面的&#x200B;**管道**卡片新增 Edge Delivery 管道。*

![Add Edge Delivery pipeline dialog box](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *新增 Edge Delivery 管道對話框。*

請參閱[新增 Edge Delivery 管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)

若您有興趣測試這個新功能並分享意見回饋，請使用與您的 Adobe ID 關聯的電子郵件傳送電子郵件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。

## 錯誤修正 {#bug-fixes}

9月的Cloud Manager版本沒有重大錯誤修正。


<!-- ## Known issues {#known-issues} -->


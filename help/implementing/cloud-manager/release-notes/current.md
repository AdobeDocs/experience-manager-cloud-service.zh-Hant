---
title: Cloud Manager 2025.7.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.7.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: f3e31d1f17283086cd6fe9e73d67feac938d6567
workflow-type: ht
source-wordcount: '1209'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.7.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.7.0 的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中 Cloud Manager 2025.7.0 的發行日期為 2025 年 7 月 10 日 (星期四)。

下一個版本預計於 2025 年 8 月 7 日 (星期四) 發行。

## 新增功能 {#what-is-new}

* **Cloud Manager 新增 ECDSA (橢圓曲線數位簽名演算法) SSL 憑證支援**

  Cloud Manager 現在支援 ECDSA 憑證。此功能透過較小的金鑰提供強大的安全性，讓客戶能夠在其 CDN 設定中套用輕量版的現代加密功能。<!-- https://jira.corp.adobe.com/browse/CMGR-62399 -->

* **下載網站授權使用量報告**

  在「**Sites 使用情況詳細資料**」頁面 (在 Cloud Manager 中按一下「**授權**」。在「解決方案」表格的「**Sites**」列中，按一下「**檢視使用情況詳細資料**」)，客戶現在可以按一下「**下載報告**」，將其資料匯出為 CSV 檔案。此下載簡化了分析和共用使用趨勢。<!-- https://jira.corp.adobe.com/browse/CMGR-42274 -->

  ![「Sites 使用情況詳細資料」頁面](/help/implementing/cloud-manager/release-notes/assets/sites-license-usage-page.png)

  請參閱[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)。

## Alpha/Beta 計劃 {#private-beta-program}

參與 Cloud Manager 的 Alpha 和 Beta 計劃，在即將推出的功能正式發佈之前，享有獨家搶先體驗的機會。

目前提供下列機會：

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

最近的增強功能：您現在可以透過更簡單、更直覺的工作流程，在非生產管道上設定專用的測試環境。簡化的設定可加速完成並減少設定錯誤。

請參閱[新增專用測試環境](/help/implementing/cloud-manager/specialized-test-environment.md)。

![Add environment dialog box with Specialized Testing Environment radio button selected](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

若您有興趣測試這個新功能並分享意見回饋，請使用與您的 Adobe ID 關聯的電子郵件傳送電子郵件至 [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com)。


### 自備 Git (BYOG) - 現在支援 Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客戶現在可以將其 Azure DevOps Git 存放庫加入 Cloud Manager 中，並同時支援現代 Azure DevOps 和舊版 VSTS (Visual Studio Team Services) 存放庫。

* Edge Delivery Services 使用者可以使用所加入的存放庫來同步處理及部署網站程式碼。
* AEM as a Cloud Service 和 Adobe Managed Services (AMS) 使用者可以將此存放庫連結至全堆疊以及前端管道。

即將推出對更多管道類型的支援以及透過程式碼品質管道驗證提取要求的功能。

請查看[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![Add Repository dialog box](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

如果您有興趣測試此新功能並分享您的意見回饋，請使用與您的 Adobe ID 關聯的電子郵件地址向 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) 傳送電子郵件。請務必包含您要使用的 Git 平台以及您是否使用私人/公開或企業存放庫結構。


**關於 BYOG 的常見問題集**

| 問題 | 答案 |
|---|---|
| *如有必要，專案如何切換回 Adobe 管理的 Git 存放庫？* | 切換回來是很簡單直覺的操作。[更新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)使其指向 Adobe 存放庫並移除不再需要的外部存放庫。 |
| *是否可能針對不同環境 (例如非生產環境和生產環境) 設定不同的存放庫，以便先在非生產環境中進行測試？* | 是的，可以為不同的環境設定不同存放庫。例如，開發或程式碼品質管道可以指向外部存放庫，而生產管道與 Adobe 存放庫保持連線。在此設定期間，請確保兩個存放庫之間的同步作業保持「使用中」狀態。 |
| *IP 允許清單等現有設定是否繼續運作？* | 是的，現有的 IP 允許清單繼續照常運作。但是，如果外部 Git 存放庫受防火牆保護，則必須將必要的 [Adobe IP 位址新增至允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有 GitLab 存放庫 URL 是否均可運作？使用中的存放庫 URL 遵循 `https://gitlab_dedicated_url.com/path/repo-name.git` 格式，與文件中的範例不同。* | 是的，支援所有支援 API V3 或 V4 的 GitLab 存放庫，包括自行託管的 GitLab URL，例如[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`) 中所說明的 URL。 |


#### 管理存取權杖{#manage-access-tokens}

使用 Cloud Manager 中的&#x200B;**管理存取權杖**，檢視、重新命名及刪除與外部 BYOG 存放庫 (例如 GitHub Enterprise、GitLab、Bitbucket 和 Azure DevOps) 關聯的存取權杖。

請參閱[管理存取權杖](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

如果您有興趣測試此新功能並分享意見回饋，請使用與您的 Adobe ID 相關聯的電子郵件寄送電子郵件至 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)。


### 新增 Edge Delivery 設定管道 {#add-eds-pipeline}

現在，使用 Edge Delivery Services 建置的網站已支援設定管道，所以在 Cloud Service 環境以外也可以使用這項功能。您可以使用&#x200B;**設定管道**&#x200B;來管理設定，例如流量篩選規則和 Web 應用程式防火牆 (WAF) 設定等 (如適用)。請參閱[支援的設定](/help/operations/config-pipeline.md#configurations)。

![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *從&#x200B;**計劃概觀**頁面的&#x200B;**管道**卡片新增 Edge Delivery 管道。*

![Add Edge Delivery pipeline dialog box](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *新增 Edge Delivery 管道對話框。*

若您有興趣測試這個新功能並分享意見回饋，請使用與您的 Adobe ID 關聯的電子郵件傳送電子郵件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。


## 錯誤修正

* Cloud Manager 現在會在環境升級期間更新所有管道的發行版本，確保所有管道類型間維持一致的版本追蹤。<!-- CMGR-69043 -->
* 網域驗證 (DV) SSL 憑證失敗時，使用者介面現在會顯示狀態和詳細的錯誤訊息，有助於了解和解決憑證問題。<!-- CMGR-68872 -->
* 編輯網域對應時，使用者介面現在可以防止選取與所選網域不相符的 SSL 憑證，從而減少錯誤設定，並改善設定期間的可靠性。<!-- CMGR-64307 -->
* 在某些情況下，憑證並未正確刪除，使得網域維持使用中。<!-- CMGR-69867 -->
* 已修正在特定情況下可能無法從 *Adobe Assets* 升級至 *Adobe Assets Ultimate* 的問題。現在的轉換更順暢且更可靠。<!-- CMGR-69506 -->
* 已解決建立多區域環境時自動設定主要區域欄位的問題，以順暢支援下游服務和部署。<!-- CMGR-69471 -->
* 已解決部分設定管道未在執行後正常停止的問題。目前管道已成功完成並如預期關閉，從而提高可靠性。<!-- CMGR-69344 -->


<!-- ## Known issues {#known-issues} -->


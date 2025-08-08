---
title: Cloud Manager 2025.8.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.8.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 3111e74e844fb37afa0c7d218c37014d32ad0a64
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 59%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.8.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.8.0 的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.8.0發行日期是2025年8月7日星期四。

下一個預計發行日期為2025年9月4日星期四。






## 新增功能 {#what-is-new}

* **Edge Delivery Services授權可以自助方式包含在HIPAA程式中**

  具有醫療保健或敏感資料需求的組織現在可以自助方式使用Edge Delivery Services，以符合HIPAA法規嚴格標準。<!-- CMGR-70016 -->

* **BYOG現在可用於Edge Delivery Services**

  Cloud Manager現在可讓您設定外部Git存放庫，啟用彈性的程式碼管理工作流程。 <!--(CMGR‑69010, CMGR‑70988) -->也可讓您直接在Cloud Manager UI中，從選取的分支提取程式碼，減少手動存放庫工作。 請參閱[設定Edge Delivery網站以使用外部Git存放庫](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md) <!-- (CMGR‑68085)(CMGR-69015) --> <!-- KT: https://wiki.corp.adobe.com/display/DMSArchitecture/%5B2025%5D+Cloud+Manager+-+Bring+Your+Own+Git+with+EDS -->

* **自動布建新的Forms附加元件**

  僅限網站的客戶通常需要以輕量且低成本的方式建立行銷表格。 新的AEM Forms Sites附加元件將有限的Forms功能新增到Sites程式，以符合需求。 如有需要，也可建立完整AEM Forms產品的明確升級路徑。<!-- (CMGR-64301) --> <!-- KT: CMGR Provisioning Support for AEM Forms Sites Add-On SKU https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3578379797 -->

  附加元件：
   * 附加到Sites計畫並與其一起部署 — 沒有單獨的Forms計畫或權益。
   * 鎖定簡單的行銷表格使用案例。
   * 僅當IMS組織擁有可用的Forms附加元件授權時，才會在生產計畫建立或生產計畫編輯期間出現在&#x200B;**解決方案和附加元件**&#x200B;清單中。

     ![Forms附加元件](/help/implementing/cloud-manager/release-notes/assets/forms-add-on.png) *只有在您的IMS組織中有Forms附加元件授權時，才能在程式中新增Forms附加元件。*

     ![建立生產計畫時，在Solutions &amp; Add-Ons中選取Forms附加元件](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-creating-production-program.png) *在計畫建立期間，您可以在Sites解決方案中選取Forms附加元件。*

     ![編輯生產程式時的Forms附加元件](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-editing-production-program.png) *在&#x200B;**編輯程式**中，選取Sites程式的Forms附加元件，然後執行管道以在環境中啟動它。*

     如需詳細資訊，請參閱[建立生產計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。

## Beta計畫 {#private-beta-program}

參與Cloud Manager的Beta版計畫，在即將推出的功能正式發行前取得獨家存取權。

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

**最近的增強功能**

* 您現在可以透過更簡單、更直覺的工作流程，在非生產管道上設定專門測試環境。 簡化的設定可加速完成並減少設定錯誤。
* **Copy Content**&#x200B;現在在專業測試環境中受到支援。 您現在可以在映象生產環境的隔離測試環境中安全地執行&#x200B;**複製內容**。<!-- (CMGR‑68900) -->

請參閱[新增專用測試環境](/help/implementing/cloud-manager/specialized-test-environment.md)。

![Add environment dialog box with Specialized Testing Environment radio button selected](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

若您有興趣測試這個新功能並分享意見回饋，請使用與您的 Adobe ID 關聯的電子郵件傳送電子郵件至 [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com)。


### 自備Git (BYOG) {#gitlab-bitbucket-azure-vsts}

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
| *現有的設定（例如`IP Allow`個清單）是否仍可繼續運作？* | 是，現有的`IP Allow`清單仍照常運作。 但是，如果外部 Git 存放庫受防火牆保護，則必須將必要的 [Adobe IP 位址新增至允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有 GitLab 存放庫 URL 是否均可運作？使用中的存放庫 URL 遵循 `https://gitlab_dedicated_url.com/path/repo-name.git` 格式，與文件中的範例不同。* | 是的，支援所有支援 API V3 或 V4 的 GitLab 存放庫，包括自行託管的 GitLab URL，例如[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`) 中所說明的 URL。 |


#### 管理存取權杖{#manage-access-tokens}

使用 Cloud Manager 中的&#x200B;**管理存取權杖**，檢視、重新命名及刪除與外部 BYOG 存放庫 (例如 GitHub Enterprise、GitLab、Bitbucket 和 Azure DevOps) 關聯的存取權杖。

請參閱[管理存取權杖](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


### 新增 Edge Delivery 設定管道 {#add-eds-pipeline}

現在，使用 Edge Delivery Services 建置的網站已支援設定管道，所以在 Cloud Service 環境以外也可以使用這項功能。您可以使用&#x200B;**設定管道**&#x200B;來管理設定，例如流量篩選規則和 Web 應用程式防火牆 (WAF) 設定等 (如適用)。請參閱[支援的設定](/help/operations/config-pipeline.md#configurations)。

**最近的增強功能**

* Edge Delivery Services管道現在會在&#x200B;**部署的代碼**&#x200B;欄中顯示&#x200B;**組態**，以便即時識別僅限組態的部署。<!-- CMGR‑69681 -->
* 當程式包含至少一個Edge Delivery網站和一個對應的網域時，Cloud Manager會顯示&#x200B;**新增Edge Delivery Services管道**。 否則，該選項會顯示為停用，而工具提示會說明缺少的需求。<!-- CMGR‑69680 -->
* **Edge Delivery**&#x200B;標籤顯示新的&#x200B;**Edge Delivery管道** Widget，其中列出每個管道的名稱、狀態、存放庫和分支。<!-- (CMGR-69052) -->

  ![Edge Delivery管道Widget，顯示管道名稱、狀態、存放庫和分支](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* **篩選器**&#x200B;面板新增&#x200B;**傳遞型別**&#x200B;區段；包含&#x200B;**Edge傳遞**&#x200B;和&#x200B;**發佈傳遞**&#x200B;核取方塊。<!-- (CMGR-69682) -->

  ![篩選器面板，顯示Edge傳遞和發佈傳遞的新傳遞型別](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *從&#x200B;**計劃概觀**頁面的&#x200B;**管道**卡片新增 Edge Delivery 管道。*

![Add Edge Delivery pipeline dialog box](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *新增 Edge Delivery 管道對話框。*

請參閱[新增Edge Delivery管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)

若您有興趣測試這個新功能並分享意見回饋，請使用與您的 Adobe ID 關聯的電子郵件傳送電子郵件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。


## 錯誤修正

* 管道現在僅將變數傳送至作用中的Edge Delivery Services網域設定，略過在管道重新建立期間移除的任何設定。<!-- (CMGR‑70039) -->
* 管道執行現在可以可靠開始；修正了某些管道因內部資源處理錯誤而無法啟動的問題。<!-- (CMGR‑58167) -->
* 內容複製會驗證Cloud Manager許可權，並封鎖由缺少部署管理員或管理員許可權的使用者開始。<!-- (CMGR‑62097) -->


<!-- ## Known issues {#known-issues} -->


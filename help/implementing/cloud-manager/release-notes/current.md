---
title: Cloud Manager 2025.7.0 版發行說明
description: 了解關於 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.7.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 26fbc60b1348e8c5f42adc8fd0e596b639fe9b44
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 64%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.7.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解關於 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.7.0 的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.7.0發行日期是2025年7月10日星期四。

下一個預計發行日期為2025年8月7日星期四。

## 新增功能 {#what-is-new}

* **Cloud Manager新增ECDSA （橢圓曲線數位簽章演演算法） SSL憑證支援**

  Cloud Manager現在支援ECDSA憑證。 此功能透過較小的金鑰大小提供強大的安全性，讓客戶可在其CDN設定中套用輕量型的現代加密技術。<!-- https://jira.corp.adobe.com/browse/CMGR-62399 -->

* **下載網站授權使用量報告**

  在&#x200B;**網站使用詳細資料**&#x200B;頁面(在Cloud Manager中，按一下&#x200B;**授權**)。 在「解決方案」表格的&#x200B;**網站**&#x200B;列中，按一下&#x200B;**檢視使用狀況詳細資料**)，客戶現在可以按一下&#x200B;**下載報表**，將其資料匯出為CSV檔案。 此下載檔案可簡化分析和共用使用趨勢的程式。<!-- https://jira.corp.adobe.com/browse/CMGR-42274 -->

  ![網站使用狀況詳細資訊頁面](/help/implementing/cloud-manager/release-notes/assets/sites-license-usage-page.png)

## 早期採用者計畫 {#private-beta-program}

參與Cloud Manager的Alpha版和Beta版計畫，在一般版本發行前取得即將推出的功能的專屬搶先使用權。

目前提供下列機會：


### 管道部署的一鍵式回覆 {#one-click-rollback}

如果最新的程式碼無法如預期運作，請快速回復到先前的部署，而不需要重新執行完整的管道或手動回覆認可。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

<!-- Add link to topic within the affected article ==>


### Specialized Testing Environment {#specialized-test-environment}

Cloud Manager now supports the addition of a new environment type called **Specialized Testing Environment**. The environment is designed to help teams validate features under near-production conditions before going live. This environment type is distinct from *Production + Stage*, *Development*, or *Rapid Development* environments and offers a focused space for running advanced validation scenarios.

Recent enhancement: You can now configure specialized testing environments on a non-production pipeline through a simpler, more intuitive workflow. The streamlined setup speeds completion and reduces configuration errors.

See [Add a Specialized Testing Environment](/help/implementing/cloud-manager/specialized-test-environment.md).

![Add environment dialog box with Specialized Testing Environment radio button selected](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID.


### Bring Your Own Git (BYOG) - now with support for Azure DevOps {#gitlab-bitbucket-azure-vsts}

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

![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *從&#x200B;**計劃概觀**&#x200B;頁面的&#x200B;**管道**&#x200B;卡片新增 Edge Delivery 管道。*

![Add Edge Delivery pipeline dialog box](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *新增 Edge Delivery 管道對話框。*

若您有興趣測試這個新功能並分享意見回饋，請使用與您的 Adobe ID 關聯的電子郵件傳送電子郵件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。


## 錯誤修正

* Cloud Manager現在會在環境升級期間更新所有管道的發行版本，確保所有管道型別之間的版本追蹤一致。<!-- CMGR-69043 -->
* 現在，當網域驗證(DV) SSL憑證失敗時，UI會顯示狀態和詳細的錯誤訊息，有助於瞭解並解決憑證問題。<!-- CMGR-68872 -->
* 編輯網域對應時，UI現在會防止選取不符合所選網域的SSL憑證，減少設定錯誤並提升設定期間的可靠性。<!-- CMGR-64307 -->
* 在某些情況下，憑證未被正確刪除，維護網域仍然有效。<!-- CMGR-69867 -->
* 修正了在某些情況下可能封鎖從&#x200B;*Adobe Assets*&#x200B;升級至&#x200B;*Adobe Assets Ultimate*&#x200B;的問題。 轉換過程現在更順暢、更可靠。<!-- CMGR-69506 -->
* 解決建立多區域環境時，主要區域欄位會自動設定，以支援順暢下游服務和部署的問題。<!-- CMGR-69471 -->
* 解決某些設定管道在執行後未正確停止的問題。 現在，管道已成功完成並按預期關閉，提高了可靠性。<!-- CMGR-69344 -->


<!-- ## Known issues {#known-issues} -->


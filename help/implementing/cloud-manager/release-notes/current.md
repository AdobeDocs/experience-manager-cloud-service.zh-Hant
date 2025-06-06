---
title: Cloud Manager 2025.6.0 版發行說明
description: 了解有關 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.6.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 52c8745d3a3cc4bc41003a258a85a817e7ccb48b
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 55%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.6.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解有關 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.6.0 的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.6.0發行日期是2025年6月5日星期四。

下一個預計發行日期為2025年7月10日星期四。

## 新增功能 {#what-is-new}

* **授權儀表板現在包含Edge Delivery Services授權**

  Edge Delivery Services授權使用方式現在顯示在授權儀表板中，讓您更清楚地檢視您的權益和狀態。<!-- CMGR-67686 -->

  ![授權儀表板](/help/implementing/cloud-manager/assets/license-dashboard.png)

  請參閱[授權儀表板](/help/implementing/cloud-manager/license-dashboard.md)。

* **Edge Delivery網站設定已更新**

  要求&#x200B;**Edge Delivery Origin**&#x200B;而非&#x200B;**存放庫URL**，簡化新增Edge Delivery網站的流程，讓上線和設定更快速且更直覺<!-- CMGR-67686 -->

  ![新增Edge Delivery網站對話方塊](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-site.png)

  請參閱[新增Edge Delivery網站](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)。

* **管道我的最愛**

  在此版本中，Cloud Manager引入釘選我的最愛管道的功能，可讓您將特定管道標示為我的最愛，以便這些管道顯示在&#x200B;**管道**&#x200B;頁面上的清單頂端。 此增強功能使經常存取的管道更容易找到和執行。<!-- CMGR-68293 -->

  ![管道標示為我的最愛](/help/implementing/cloud-manager/release-notes/assets/pipeline-favorites.png) *兩個管道標示為我的最愛。*

  檢視[標示管道我的最愛](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipeline-favorites)。


## 早期採用者計劃 {#early-adoption}

參與 Cloud Manager 的早期採用者計劃，在即將推出的功能正式發佈之前獲得獨家存取權。

目前提供以下早期採用者機會：


### 專用測試環境 {#specialized-test-environment}

Cloud Manager現在支援新增名為&#x200B;**特殊測試環境**&#x200B;的新環境型別。 此環境旨在協助團隊在接近生產的情況下驗證功能，然後再上線。 此環境型別不同於&#x200B;*生產+階段*、*開發*&#x200B;或&#x200B;*快速開發*&#x200B;環境，並提供執行進階驗證案例的重點空間。

請參閱[新增專業測試環境](/help/implementing/cloud-manager/specialized-test-environment.md)。

![已選取「特殊化測試環境」選項按鈕的「新增環境」對話方塊](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

如果您有興趣測試這項新功能並分享您的意見回饋，請從與Adobe ID相關聯的電子郵件地址傳送電子郵件至[grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com)。


### 自備Git (BYOG) — 現在支援Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客戶現在可以將其 Azure DevOps Git 存放庫加入 Cloud Manager 中，並同時支援現代 Azure DevOps 和舊版 VSTS (Visual Studio Team Services) 存放庫。

* Edge Delivery Services 使用者可以使用所加入的存放庫來同步處理及部署網站程式碼。
* AEM as a Cloud Service 和 Adobe Managed Services (AMS) 使用者可以將此存放庫連結至全堆疊以及前端管道。

即將推出對更多管道類型的支援以及透過程式碼品質管道驗證提取要求的功能。

請查看[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![新增存放庫對話框](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

如果您有興趣測試此新功能並分享您的意見回饋，請使用與您的 Adobe ID 關聯的電子郵件地址向 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) 傳送電子郵件。請務必包含您要使用的 Git 平台以及您是否使用私人/公開或企業存放庫結構。


**關於BYOG的常見問題**

| 問題 | 答案 |
|---|---|
| *如有必要，專案如何切換回 Adobe 管理的 Git 存放庫？* | 切換回來是很簡單直覺的操作。[更新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)使其指向 Adobe 存放庫並移除不再需要的外部存放庫。 |
| *是否可能針對不同環境 (例如非生產環境和生產環境) 設定不同的存放庫，以便先在非生產環境中進行測試？* | 是的，可以為不同的環境設定不同存放庫。例如，開發或程式碼品質管道可以指向外部存放庫，而生產管道與 Adobe 存放庫保持連線。在此設定期間，請確保兩個存放庫之間的同步作業保持「使用中」狀態。 |
| *IP 允許清單等現有設定是否繼續運作？* | 是的，現有的 IP 允許清單繼續照常運作。但是，如果外部 Git 存放庫受防火牆保護，則必須將必要的 [Adobe IP 位址新增至允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有 GitLab 存放庫 URL 是否均可運作？使用中的存放庫 URL 遵循 `https://gitlab_dedicated_url.com/path/repo-name.git` 格式，與文件中的範例不同。* | 是的，支援所有支援 API V3 或 V4 的 GitLab 存放庫，包括自行託管的 GitLab URL，例如[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`) 中所說明的 URL。 |


#### 管理存取權杖{#manage-access-tokens}

在Cloud Manager中使用&#x200B;**管理存取權杖**&#x200B;來檢視、重新命名和刪除與外部BYOG存放庫（例如GitHub Enterprise、GitLab、Bitbucket和Azure DevOps）相關聯的存取權杖。

請參閱[管理存取權杖](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

如果您有興趣測試這項新功能並分享您的意見回饋，請從與Adobe ID相關聯的電子郵件地址傳送電子郵件至[Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)。


### 新增 Edge Delivery 設定管道 {#add-eds-pipeline}

現在，使用 Edge Delivery Services 建置的網站已支援設定管道，所以在 Cloud Service 環境以外也可以使用這項功能。您可以使用&#x200B;**設定管道**&#x200B;來管理設定，例如流量篩選規則和 Web 應用程式防火牆 (WAF) 設定等 (如適用)。請參閱[支援的設定](/help/operations/config-pipeline.md#configurations)。

![在新增管道下拉式清單中新增Edge Delivery管道](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *從&#x200B;**方案總覽**頁面，**管道**卡新增Edge Delivery管道。*

![新增Edge Delivery管道對話方塊](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *新增Edge Delivery管道對話方塊。*

如果您有興趣測試這個新功能並分享意見回饋，請使用與您的 Adobe ID 相關聯的電子郵件寄送電子郵件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。


## 錯誤修正

* 先前標示為`HIBERNATED`的沙箱環境不再卡在該狀態，讓管道執行或部署可如預期繼續進行。<!-- CMGR-67705 -->
* 現在，AEM Cloud Manager在擷取客戶成品時，正確對應了409錯誤所導致的Maven建置失敗（衝突）與客戶導致的失敗。 此變更透過區分內部錯誤和與客戶環境設定相關的問題來改善錯誤訊息。<!-- CMGR-66673 -->


<!-- ## Known issues {#known-issues} -->


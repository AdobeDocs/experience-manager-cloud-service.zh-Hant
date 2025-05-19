---
title: Cloud Manager 2025.5.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.5.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 21%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.5.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.5.0 的發行資訊。

另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.5.0發行日期是2025年5月8日星期四。

下一個預計發行日期為2025年6月5日星期四。

## 新增功能 {#what-is-new}

### 按一下即可設定Edge Delivery Services的內容來源

Adobe Experience Manager (AEM) Edge Delivery Services可使用快速且遍佈全球的邊緣網路，從多種來源(例如Google Drive、SharePoint或AEM本身)進行內容傳送。

Helix 4和Helix 5的內容來源組態不同。 瞭解差異，並遵循兩個版本的完整設定步驟、範例和驗證指示。

請參閱[設定您的內容來源](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md)。


## 早期採用計劃 {#early-adoption}

參與Cloud Manager的早期採用者計畫，在即將推出的功能正式發行之前獲得獨家存取權。

目前提供下列早期採用者機會：

### 新增Edge Delivery設定管道 {#add-eds-pipeline}

使用Edge Delivery Services建置的網站現在支援設定管道，將此功能擴展到Cloud Service環境以外。 您可以視情況使用&#x200B;**設定管道**&#x200B;來管理設定，例如流量篩選規則和Web應用程式防火牆(WAF)設定。 請參閱[支援的組態](/help/operations/config-pipeline.md#configurations)。

![在新增管道下拉式清單中新增Edge Delivery管道](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png)

如果您有興趣測試這項新功能並分享您的意見回饋，請從與Adobe ID相關聯的電子郵件地址傳送電子郵件至[grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。

### 自備Git — 現在支援Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客戶現在可以將其Azure DevOps Git存放庫加入Cloud Manager，並支援現代Azure DevOps和舊版VSTS (Visual Studio Team Services)存放庫。

* 對於Edge Delivery Services使用者，已上線的存放庫可用於同步和部署網站程式碼。
* 對於AEM as a Cloud Service和Adobe Managed Services (AMS)使用者，存放庫可以連結到完整棧疊和前端管道。

即將支援其他管道型別，並透過程式碼品質管道進行提取請求驗證。

請查看[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![新增存放庫對話框](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

如果您有興趣測試此新功能並分享您的意見回饋，請使用與您的 Adobe ID 關聯的電子郵件地址向 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) 傳送電子郵件。請務必包含您要使用的 Git 平台以及您是否使用私人/公開或企業存放庫結構。

#### 自備Git的相關常見問題

| 問號 | 答案 |
|---|---|
| *專案如何視需要切換回Adobe管理的Git存放庫？* | 直接切換回原位。 [更新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)以指向Adobe存放庫，如果不再需要外部存放庫，則將其移除。 |
| *是否可以針對不同的環境（例如，非生產環境與生產環境）設定不同的存放庫，以允許先在非生產環境中測試？* | 可以，可以為不同的環境設定不同的存放庫。 例如，開發或程式碼品質管道可指向外部存放庫，而生產管道仍會連線至Adobe存放庫。 在此設定期間，請確定兩個存放庫之間的同步處理作業保持作用中。 |
| *現有的設定（例如IP允許清單）是否仍可繼續運作？* | 是的，現有的IP允許清單會照常繼續運作。 不過，如果外部Git存放庫受到防火牆保護，則必須將必要的[Adobe IP位址新增至允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有GitLab存放庫URL都運作嗎？ 使用的存放庫URL格式為`https://gitlab_dedicated_url.com/path/repo-name.git`，不同於檔案中的範例。* | 是，支援任何支援API V3或V4的GitLab存放庫，包括自我託管的GitLab URL，例如[在Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`)中新增外部存放庫中所述。 |


<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->


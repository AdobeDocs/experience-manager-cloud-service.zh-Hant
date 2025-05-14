---
title: Cloud Manager 2025.5.0 版發行說明
description: 了解 Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.5.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 3db5ee2852fadc9c86b3a7979ce40296bbaca858
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 14%

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

Helix 4和Helix 5的內容來源組態有下列差異：

| 版本 | 內容來源設定方法 |
| --- | --- |
| Helix 4 | YAML檔案(`fstab.yaml`) |
| Helix 5 | 組態服務API （*否`fstab.yaml`*） |

本文提供這兩個版本的完整設定步驟、範例和驗證指示。

**開始之前**

如果您在Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site)中使用[按一下Edge Delivery，則您的網站為具有單一存放庫的Helix 5。 遵循Helix 5指示，並使用提供的Helix 4 YAML版本指示作為後援。

**決定您的Helix版本**

* Helix 4 — 您的專案包含`fstab.yaml`檔案。
* Helix 5 — 您的專案&#x200B;*不*&#x200B;使用`fstab.yaml`，並已透過Edge Delivery Services UI或API設定。

透過存放庫中繼資料確認，或如果您仍然不確定，請洽詢管理員。

#### 設定Helix 4的內容來源

在Helix 4中，fstab.yaml檔案會定義您網站的內容來源。 此檔案位於GitHub存放庫的根目錄下，會將URL路徑首碼（稱為掛接點）對應至外部內容來源。 典型的範例看起來如下所示：

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

此範例僅供說明之用。 實際URL應指向您的內容來源，例如Google磁碟機資料夾、SharePoint目錄或AEM路徑。

**設定Helix 4的內容來源：**

步驟因您使用的來源系統而異。

* **Google磁碟機**

   1. 建立Google磁碟機資料夾。
   1. 與`helix@adobe.com`共用資料夾。
   1. 取得分享資料夾連結。
   1. 更新您的`fstab.yaml`，如下所示：

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. 提交變更並推送至GitHub。

* **SharePoint**

   1. 建立SharePoint資料夾或檔案庫。
   1. 與`helix@adobe.com`共用存取權。
   1. 取得資料夾URL。
   1. 更新您的`fstab.yaml`，如下所示：

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. 提交變更並推送至GitHub。

* **AEM**

   1. 識別您的AEM內容路徑。
   1. 使用AEM內容匯出URL，如下所示：

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. 提交變更並推送至GitHub。

##### 驗證 

* 使用AEM Sidekick Chrome擴充功能，按一下&#x200B;**預覽** > **發佈** > **測試已上線的網站**。
* 驗證URL： `https://main--<repo>--<org>.hlx.page/`

#### 設定Helix 5的內容來源

Helix 5是重寫程式，不使用`fstab.yaml`，並支援多個網站共用相同的目錄。 透過設定服務API或Edge Delivery Services UI管理設定。 設定是網站層級（而非存放庫層級）。

概念差異如下：

| 外觀 | Helix 4 | Helix 5 |
| --- | --- | --- |
| 設定 | 透過`fstab.yaml`完成 | 透過API或UI （而非YAML）完成。 |
| 掛接點 | 定義於`fstab.yaml`。 | 非必要。 以隱含的方式瞭解根目錄。 |

**設定Helix 5的內容來源：**

1. 使用設定服務API，透過API金鑰或存取權杖進行驗證。
1. 進行下列`PUT` API呼叫：

   ```bash {.line-numbering}
   PUT /api/{program}/{programId}/site/{siteId}
   Content-Type: application/json
   
   {
     "sitename": "my-site",
     "branchName": "main",
     "version": "v5",
     "repo": "my-content-repo-link"
   }
   ```

1. 驗證回應（預期： HTTP 200確定）。

##### 驗證 

* 使用AEM Sidekick Chrome擴充功能，按一下&#x200B;**預覽** > **發佈** > **測試已上線的網站**。
* 驗證URL： `https://main--<repo>--<org>.aem.page/`
* （選用）透過下列`GET` API呼叫檢查目前的設定：

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```

<!--
* **AI-powered build summaries now available for internal use**

    Internal users can now use AI-powered build summaries to simplify build log analysis. The feature provides actionable recommendations and helps identify the root causes of build failures.

    ![Build Summary dialog box](/help/implementing/cloud-manager/release-notes/assets/build-summary.png)
-->


## 早期採用計劃 {#early-adoption}

參與Cloud Manager的早期採用者計畫，在即將推出的功能正式發行之前獲得獨家存取權。

目前提供下列早期採用者機會：

### 新增 Edge Delivery 管道 {#add-eds-pipeline}

**管道**&#x200B;現在支援使用Edge Delivery Services建置的網站，此功能已擴充到不只是Cloud Service環境。 您可以視情況使用&#x200B;**管道**&#x200B;來管理設定，例如流量篩選規則和Web應用程式防火牆(WAF)設定。 請參閱[支援的組態](/help/operations/config-pipeline.md#configurations)。

<!-- ![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png) -->

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


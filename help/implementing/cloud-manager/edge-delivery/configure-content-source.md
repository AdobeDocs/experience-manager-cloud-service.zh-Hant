---
title: 設定您的內容Source
description: 瞭解如何在Helix 4中使用fstab.yaml，或在Helix 5中使用Edge Delivery Services UI （或設定服務API）來設定Edge Delivery網站的內容來源。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 按一下即可設定Edge Delivery Services的內容來源 {#config-content-source}

Adobe Experience Manager (AEM) Edge Delivery Services可使用快速且遍佈全球的邊緣網路，從多種來源(例如Google Drive、SharePoint或AEM本身)進行內容傳送。

Helix 4和Helix 5的內容來源組態有下列差異：

| 版本 | 內容來源設定方法 |
| --- | --- |
| Helix 4 | YAML檔案(`fstab.yaml`) |
| Helix 5 | 組態服務API （*否`fstab.yaml`*） |

本文提供這兩個版本的完整設定步驟、範例和驗證指示。

**開始之前**

如果您在Cloud Manager[&#128279;](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site)中使用按一下Edge Delivery，則您的網站為具有單一存放庫的Helix 5。 [遵循Helix 5指示](#config-helix5)，並使用提供的Helix 4 YAML版本指示作為遞補。

**決定您的Helix版本**

* Helix 4 — 您的專案包含`fstab.yaml`檔案。
* Helix 5 — 您的專案&#x200B;*不*&#x200B;使用`fstab.yaml`，並已透過[Edge Delivery Services UI](#config-helix5)或API設定。

透過存放庫中繼資料確認，或如果您仍然不確定，請洽詢管理員。

## 設定Helix 4的內容來源

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

### 驗證 

* 使用AEM Sidekick Chrome擴充功能，按一下&#x200B;**預覽** > **發佈** > **測試已上線的網站**。
* 驗證URL： `https://main--<repo>--<org>.hlx.page/`

## 設定Helix 5的內容來源 {#config-helix5}

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

### 驗證 

* 使用AEM Sidekick Chrome擴充功能，按一下&#x200B;**預覽** > **發佈** > **測試已上線的網站**。
* 驗證URL： `https://main--<repo>--<org>.aem.page/`
* （選用）透過下列`GET` API呼叫檢查目前的設定：

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```

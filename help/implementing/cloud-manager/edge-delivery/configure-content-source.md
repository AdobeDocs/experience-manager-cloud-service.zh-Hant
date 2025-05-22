---
title: 設定您的內容Source
description: 瞭解如何設定Edge Delivery網站的內容來源。 搭配Helix 4架構使用「fstab.yaml」，或搭配Helix 5架構使用Cloud Manager中的引導式精靈（或設定服務API）。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: f82eafc0-03d0-4c69-9b28-e769a012531b
source-git-commit: 71618a5603328990603db2ee7554048c9020a883
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 63%

---

# 按一下即可設定Edge Delivery Services的內容來源 {#config-content-source}

>[!IMPORTANT]
>
>*Helix*&#x200B;是基礎架構的內部名稱，可支援AEM Sites的檔案式撰寫。 它不是功能或產品名稱。 在本文中，*Helix*&#x200B;是指您的Edge Delivery網站所使用的架構版本。 Helix 5是基礎架構的最新版本；Helix 4是舊版。

Adobe Experience Manager (AEM) Edge Delivery Services 透過快速、遍布全球的邊緣網路，允許透過多個來源 (例如 Google Drive、SharePoint 或 AEM 本身) 進行內容傳遞。

這兩個架構版本的內容來源設定有所不同，其方式如下：

| 版本 | 內容來源設定方法 |
| --- | --- |
| Helix 4 | YAML 檔案 (`fstab.yaml`) |
| Helix 5 | 設定服務 API (*無`fstab.yaml`*) |

此文章提供兩個版本的完整設定步驟、範例和驗證指示。

**開始之前**

如果您在Cloud Manager[&#128279;](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site)中使用按一下Edge Delivery，您的網站會將Helix 5與單一存放庫搭配使用。 [遵循Helix 5指示](#config-helix5)，並使用提供的Helix 4 YAML版本指示作為遞補。

**確定您的 Helix 版本**

* Helix 4 - 您的專案包括一個 `fstab.yaml` 檔案。
* Helix 5 — 您的專案&#x200B;*不*&#x200B;使用`fstab.yaml`，且已透過[Cloud Manager使用引導精靈](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)或API進行設定。

如果您仍然不確定，請透過存放庫中繼資料確認或諮詢您的管理員。

## 設定 Helix 4 的內容來源

在Helix 4中，`fstab.yaml`檔案會定義您網站的內容來源。 此檔案位於 GitHub 存放庫的根目錄，將 URL 路徑前置詞 (稱為掛接點) 對應至外部內容來源。典型範例如下圖所示：

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

以上範例僅供說明之用。 實際 URL 應該指向您的內容來源，例如 Google Drive 資料夾、SharePoint 目錄或 AEM 路徑。

**若要設定 Helix 4 的內容來源：**

根據您使用的來源系統而定，步驟會有所不同。

* **Google Drive**

   1. 建立 Google Drive 資料夾。
   1. 與 `helix@adobe.com` 共用資料夾。
   1. 取得此共用資料夾的連結。
   1. 更新您的 `fstab.yaml`，如下所示：

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. 提交並推送變更至 GitHub。

* **SharePoint**

   1. 建立 SharePoint 資料夾或文件庫。
   1. 與 `helix@adobe.com` 共用存取權限。
   1. 取得資料夾 URL。
   1. 更新您的 `fstab.yaml`，如下所示：

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. 提交並推送變更至 GitHub。

* **AEM**

   1. 確認您的 AEM 內容路徑。
   1. 使用 AEM 內容匯出 URL，如下所示：

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. 提交並推送變更至 GitHub。

### 驗證

* 使用 AEM Sidekick Chrome 擴充功能，按一下「**預覽**」>「**發佈**」>「**測試即時網站**」。
* 驗證 URL：`https://main--<repo>--<org>.hlx.page/`

## 設定 Helix 5 的內容來源 {#config-helix5}

Helix 5 無存放庫、不使用 `fstab.yaml`，並且支援多個網站共用同一個目錄。透過設定服務API或Edge Delivery Sites使用者介面管理設定。 設定為網站層級 (非存放庫層級)。

概念性差異如下：

| 層面 | Helix 4 | Helix 5 |
| --- | --- | --- |
| 設定 | 透過 `fstab.yaml` 完成 | 透過 API 或 UI (而非 YAML) 完成。 |
| 掛接點 | 如 `fstab.yaml` 所定義。 | 不需要。此根目錄不需明言即可理解。 |

**若要設定 Helix 5 的內容來源：**

1. 使用設定服務 API，透過 API 金鑰或存取權杖進行驗證。
1. 進行以下 `PUT` API 呼叫：

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

1. 驗證回應 (預期是 HTTP 200 OK)。

### 驗證

* 使用 AEM Sidekick Chrome 擴充功能，按一下「**預覽**」>「**發佈**」>「**測試即時網站**」。
* 驗證 URL：`https://main--<repo>--<org>.aem.page/`
* (選用) 透過以下 `GET` API 呼叫檢查目前設定：

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```

---
title: Screens as a Cloud Service 常見問題集
description: 本頁面說明 Screens as a Cloud Service 的常見問題。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 100%

---

# Screens as a Cloud Service 常見問題集 {#screens-cloud-faqs}

以下區段提供與 Screens as a Cloud Service 專案相關的常見問題 (FAQ) 的答案。

## 如果指向 Screens as a Cloud Service 的 AEM Screens Player 未挑選採用 etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css 格式的自訂 clientlibs。

AEM as a Cloud Service 在每次部署時變更長快取金鑰。AEM Screens 在內容修改時產生離線快取，而不是在 Cloud Manager 執行部署時產生。清單中的這些長快取金鑰無效，因此播放器無法下載 *clientlibs*。

使用 `longCacheKey="none"`(在您的 `clientlib` 資料夾) 會完全刪除 *clientlibs* 的長快取金鑰。


## 如果離線清單未包含預期的所有資源，我該怎麼辦？ {#offline-manifest}

離線快取是使用 **bulk-offline-update-screens-service** 服務使用者產生的。某些 `bulk-offline-update-screens-service` 無法存取的路徑導致離線清單中缺少內容。

在您的程式碼中，`ui.config or ui.apps` 在設定資料夾中建立一個 OSGi 設定，其內容如下，且檔案名為 `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## 建議使用哪些影像格式在 AEM Screens as a Cloud Service 頻道中無縫轉譯影像？{#screens-cloud-image-format}

Adobe 建議在 AEM Screens as a Cloud Service 頻道中以 `.png` 和 `.jpeg` 格式來使用影像，以獲得最佳的數位招牌體驗。AEM Screens as a Cloud Service 不支援採用 `*.tif` (Tag Image File format) 格式的影像。如果頻道具有此一格式的影像，則在播放器端不會呈現影像。

## 如果處於開發人員模式 (線上) 的頻道在 AEM Screens Player 中未呈現影像，我該怎麼辦？{#screens-cloud-online-channel-blank-iframe}

Adobe 建議您使用 AEM Screens 快取功能。但是，如果您必須在開發者模式下執行頻道而且 AEM Screens Player 顯示空白畫面，請檢查播放器的開發者工具並尋找 `X-Frame-Options` 或 `frame-ancestors` 錯誤。解決方案是設定 Dispatcher，允許內容在 iFrame 中執行。通常，以下設定有效：

```
Header set Content-Security-Policy "frame-ancestors 'self' file: localhost:*;"
```

## 註冊代碼限制有什麼用處？

作為最佳實務，您可以限制註冊代碼的使用。如果註冊代碼被洩露，但註冊次數限制為 100 次，則攻擊者最多只能註冊該數量而不是更多。在建立註冊代碼並且部分客戶的播放器已經註冊後，您可以隨時更新使用限制。如果客戶發現特定註冊代碼發生異常的註冊活動，他們可以在調查時即時降低限制。如果是誤報，則他們可以增加數目，並不會影響已經註冊的播放器。

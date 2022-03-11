---
title: 螢幕as a Cloud Service常見問題
description: 本頁介紹螢幕as a Cloud Service常見問題。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 02c9cbff56399ea2ca1baad7d2289d5d4c17c1c5
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 螢幕as a Cloud Service常見問題 {#screens-cloud-faqs}

以下部分提供與螢幕as a Cloud Service項目相關的常見問題解答。

## 如果AEM Screens播放器指向螢幕as a Cloud Service，但不選擇/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css格式的自定義客戶端，我應該怎麼辦？

AEMas a Cloud Service更改每個部署的長快取鍵。 AEM Screens在修改內容時生成離線快取，而不是在雲管理器運行部署時生成。 清單中的這些長快取鍵無效，因此播放器無法下載這些 *客戶端*。

使用 `longCacheKey="none"` 在 `clientlib` 資料夾將完全刪除這些檔案的長快取項 *客戶端*。


## 如果離線清單未按預期包括所有資源，我們應該怎麼辦？ {#offline-manifest}

使用 **批量離線更新螢幕服務** 服務用戶。 某些路徑，不能由 `bulk-offline-update-screens-service`，導致離線清單中缺少內容。

在你的密碼里， `ui.config or ui.apps`，在配置資料夾中建立OSGi配置，其中包含以下內容，並將檔案名稱標題為 `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## 推薦哪些影像格式用於在AEM Screensas a Cloud Service頻道中無縫再現影像？{#screens-cloud-image-format}

建議使用格式的影像 `.png` 和 `.jpeg` 在AEM Screens的as a Cloud Service頻道，獲得最佳的數字標牌體驗。
格式化的影像 `*.tif` （標籤影像檔案格式）在AEM Screensas a Cloud Service中不受支援。 如果頻道具有此影像格式，則在播放器側將不呈現影像。

## 如果開發者模式（聯機）中的頻道未在AEM Screens播放器上呈現，我應該做什麼？{#screens-cloud-online-channel-blank-iframe}

建議利用AEM Screens快取功能，但是，如果您需要在開發人員模式下運行您的頻道，並且AEM Screens播放器顯示一個空白螢幕，請檢查您的播放器的開發人員工具並查找 `X-Frame-Options` 或 `frame-ancestors` 錯誤。 解決方案是配置調度程式以允許在iFrames中運行內容。 通常，以下配置將起作用：

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## 註冊碼限制的用途是什麼？

作為最佳做法，您可以限制註冊代碼的使用。 如果註冊代碼被洩露，但註冊限制為100個，則攻擊者最多只能註冊該號碼，但不能註冊更多。 在建立註冊代碼並且客戶的某些玩家已經註冊後，您始終可以更新使用限制。 如果客戶發現特定註冊代碼的註冊活動異常，他們可以在調查時即時降低限制，如果是虛警，則可以增加返回數量，而不會影響已註冊的玩家。

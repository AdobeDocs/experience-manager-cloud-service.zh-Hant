---
title: Screensas a Cloud Service常見問題集
description: 本頁面說明Screensas a Cloud Service常見問題集。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: 02c9cbff56399ea2ca1baad7d2289d5d4c17c1c5
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Screensas a Cloud Service常見問題集 {#screens-cloud-faqs}

以下小節提供與Screensas a Cloud Service專案相關的常見問題集(FAQ)的解答。

## 如果AEM Screens Player指向Screens as a Cloud Service未以/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css格式選取自訂clientlib，我該怎麼做？

AEM as a Cloud Service會隨著每次部署變更長快取金鑰。 AEM Screens會在修改內容時（而非Cloud Manager執行部署時）產生離線快取。 清單中的這些長快取密鑰無效，因此播放器無法下載這些 *clientlibs*.

使用 `longCacheKey="none"` 在 `clientlib` 資料夾會完全移除這些資料夾的長快取金鑰 *clientlibs*.


## 如果離線資訊清單未如預期包含所有資源，怎麼辦？ {#offline-manifest}

使用 **bulk-offline-update-screens-service** 服務使用者。 某些路徑，無法存取 `bulk-offline-update-screens-service`，導致離線清單中遺失內容。

在你的程式碼里， `ui.config or ui.apps`，請在設定資料夾中建立OSGi設定，其中包含下列內容，並將檔案名稱標題為 `org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

```
scripts=[
        "
        set principal ACL for bulk-offline-update-screens-service
                allow jcr:read on /content/mysite
                allow jcr:read on /apps/my-resources
        end
        "] 
```

## 在AEM Screensas a Cloud Service頻道中順暢轉譯影像，建議使用哪些影像格式？{#screens-cloud-image-format}

建議使用格式的影像 `.png` 和 `.jpeg` 在AEM Screensas a Cloud Service頻道中，獲得最佳的數位看板體驗。
格式的影像 `*.tif` （標籤影像檔案格式）AEM Screensas a Cloud Service不支援。 如果頻道有此格式的影像，則播放器端不會轉譯影像。

## 如果開發人員模式（線上）中的管道未在AEM Screens Player上呈現，該怎麼辦？{#screens-cloud-online-channel-blank-iframe}

建議您運用AEM Screens快取功能，但若您需要以開發人員模式執行管道，且AEM Screens Player顯示空白畫面，請檢查Player的開發人員工具並尋找 `X-Frame-Options` 或 `frame-ancestors` 錯誤。 解決方式是將Dispatcher設為允許在iFrame中執行內容。 通常下列設定可運作：

```
Header set Content-Security-Policy "frame-ancestors ‘self’ file: localhost:*;"
```

## 註冊代碼限制的用途為何？

您可以限制註冊代碼的使用方式，這是最佳作法。 如果註冊代碼被洩露，但限制為100個註冊，則攻擊者只能註冊最多該號碼，但不能註冊更多。 在建立註冊代碼且客戶的某些播放器已註冊之後，您隨時可以更新使用限制。 如果客戶觀察到特定註冊代碼的異常註冊活動，則他們可以在調查時即時降低限制，如果是虛警，則可以增加數量，而不會影響已註冊的玩家。

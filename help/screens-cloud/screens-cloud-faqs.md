---
title: Screensas a Cloud Service常見問題集
description: 本頁說明Screensas a Cloud Service常見問題集。
exl-id: 93f2144c-0e64-4012-88c6-86972d8cad9f
source-git-commit: cf091056bdb96917a6d22bf1197d9b34ebbf9610
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Screensas a Cloud Service常見問題集 {#screens-cloud-faqs}

以下小節提供與Screensas a Cloud Service專案相關的常見問題集(FAQ)的解答。

## 如果指向Screens as a Cloud Service的AEM Screens播放器未以/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css格式選取自訂clientlib，怎麼辦？

AEM as a Cloud Service會隨著每次部署變更長快取金鑰。 AEM Screens會在修改內容時（而非Cloud Manager執行部署時）產生離線快取。 清單中的這些長快取密鑰無效，因此播放器無法下載這些&#x200B;*clientlibs*。

在`clientlib`資料夾中使用`longCacheKey="none"`會完全移除這些&#x200B;*clientlibs*&#x200B;的長快取金鑰。


## 如果離線資訊清單未如預期包含所有資源，怎麼辦？ {#offline-manifest}

使用&#x200B;**bulk-offline-update-screens-service**&#x200B;服務用戶生成離線快取。 無法透過`bulk-offline-update-screens-service`存取的特定路徑會導致離線清單中遺失內容。

在您的程式碼中，即`ui.config or ui.apps`在設定資料夾中建立OSGi設定，並包含下列內容，並將檔案名稱標題為`org.apache.sling.jcr.repoinit.RepositoryInitializer-serviceusersandacls-content.config`

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

建議在AEM Screensas a Cloud Service頻道中使用`.png`和`.jpeg`格式的影像，以獲得最佳的數位招牌體驗。
AEM Screens as a Cloud Service不支援`*.tif`格式的影像（標籤影像檔案格式）。 如果頻道有此格式的影像，則播放器端不會轉譯影像。
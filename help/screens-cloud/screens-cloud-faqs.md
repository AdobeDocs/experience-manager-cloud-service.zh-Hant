---
title: Screens作為Cloud Service常見問題集
description: 本頁說明Screens作為Cloud Service常見問題集。
source-git-commit: 7a26bb50a8b95a2358912249e21daeb9c5e9c1a3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Screens作為Cloud Service常見問題集 {#screens-cloud-faqs}

以下小節提供與Screens as a Cloud Service專案相關的常見問題集(FAQ)的解答。

## 如果指向Screens as aCloud Service的AEM Screens播放器沒有以/etc.clientlibs/xxx/clientlibs/clientlib-site.lc-813643788974b0f89d686d9591526d63-lc.min.css格式挑選自訂clientlib，怎麼辦？

AEM as aCloud Service會隨著每次部署變更長快取金鑰。 AEM Screens會在修改內容時（而非Cloud Manager執行部署時）產生離線快取。 清單中的這些長快取密鑰無效，因此播放器無法下載這些&#x200B;*clientlibs*。

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

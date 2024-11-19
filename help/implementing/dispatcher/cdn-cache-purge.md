---
title: 清除內容傳遞網路快取
description: 瞭解如何設定清除API權杖（其可用於API呼叫），從AdobeCDN快取中移除快取物件。
feature: CDN Cache
exl-id: 4d091677-b817-4aeb-b131-7a5407ace3e0
role: Admin
source-git-commit: e5e0606c83f144f92f9ae57e5380a30389e8df1b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# 清除內容傳遞網路快取 {#cdn-purge-cache}

整個清除會從AdobeCDN快取中移除物件，導致未來的請求以快取遺失的形式繼續前往來源，而不是從快取提供服務。
AEM as a Cloud Service可讓您設定清除API Token，然後將其用於清除API呼叫。 請參閱[設定CDN認證和驗證](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token)，瞭解如何使用Cloud Manager設定管道驗證指示詞來設定此權杖。

有三個支援的清除變數：

* [單一URL清除](#single-purge) — 一次清除單一資源。
* [透過代理金鑰清除](#surrogate-key-purge) — 一次清除多個資源。
* [完整清除](#full-purge) — 清除所有資源。

所有清除變數都共用下列專案：

* HTTP方法必須設定為`PURGE`。
* URL可以是任何與清除請求適用的AEM服務相關聯的網域。
* `X-AEM-Purge-Key`必須在HTTP標頭中提供。

>[!CAUTION]
>清除CDN快取（尤其是使用硬標幟）將會增加來源處的流量，且如果未正確執行，可能會導致中斷。

您可以參考以設定清除金鑰和執行CDN快取清除為重點的[教學課程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache)。

## 單一URL清除 {#single-purge}

您可以一次永久刪除單一資源，如下所示：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

如上述範例所示，您可以&#x200B;**選擇性**&#x200B;指定CDN是否應對快取物件執行&#x200B;**硬式**&#x200B;清除（預設）或&#x200B;**軟式**&#x200B;清除。

預設的硬清除會使得新請求立即無法存取內容，直到從來源擷取內容為止。 軟清除會將內容標示為過時，但還是會提供給使用者端，因此使用者端不需要等到內容從來源擷取後再執行。

## 替代金鑰清除 {#surrogate-key-purge}

替代索引鍵是用於清除一組內容的唯一識別碼。 將`Surrogate-Key`標頭新增至回應，以將其套用至內容。 可以在清除API呼叫中參考一或多個替代索引鍵。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

`Surrogate-Key`以空格分隔。 與單一URL清除類似，您可以設定硬清除或軟清除。

## 完整清除 {#full-purge}

您可以依照下列步驟，完整清除所有快取資源：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

請注意，`X-AEM-Purge`標頭必須包含「all」值。

## 與客戶管理的CDN互動

若是[客戶管理的CDN](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)，也需要提供`X-Forwarded-Host`和`X-AEM-Edge-Key`：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Edge-Key: <my_edge_key>' \
-H 'X-Forwarded-Host: <my_forwarded_domain>'
```


## 與Apache/Dispatcher層的互動 {#apache-layer}

如[內容傳遞流程](/help/implementing/dispatcher/overview.md)中所述，如果快取已過期，CDN會從Apache/Dispatcher階層擷取內容。 這代表在CDN上清除資源之前，您應該確保Dispatcher上也有內容的新版本。 如需詳細資訊，另請參閱[Dispatcher快取失效](/help/implementing/dispatcher/caching.md#disp)。

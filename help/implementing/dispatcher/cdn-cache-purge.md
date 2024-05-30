---
title: 清除CDN快取
description: 瞭解如何設定清除API權杖（其可用於API呼叫），從AdobeCDN快取中移除快取物件。
feature: CDN Cache
source-git-commit: bd8f534642848a656e5e54c425049c95cdb413f7
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# 清除CDN快取 {#cdn-purge-cache}

>[!NOTE]
>此功能尚未正式推出。若要加入率先採用者計畫，請傳送電子郵件至 `aemcs-cdn-config-adopter@adobe.com`.

整個清除會從AdobeCDN快取中移除物件，導致未來的請求以快取遺失的形式繼續前往來源，而不是從快取提供服務。
AEMas a Cloud Service可讓您設定清除API Token，然後將其用於API呼叫。 閱讀 [設定CDN認證和驗證文章](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) 瞭解如何使用Cloud Manager設定管道驗證指示來設定此Token。

有三個支援的清除變數：

* [單一URL清除](#single-purge)  — 一次清除單一資源。
* [透過代理金鑰清除](#surrogate-key-purge)  — 一次永久刪除多項資源。
* [完整清除](#full-purge)  — 永久刪除所有資源。

所有清除變數都共用下列專案：

* HTTP方法必須設定為 `PURGE`.
* URL可以是任何與清除請求適用的AEM服務相關聯的網域。
* 此 `X-AEM-Purge-Key` 必須在HTTP標頭中提供。

>[!CAUTION]
>清除CDN快取（尤其是使用硬標幟）將會增加來源處的流量，且如果未正確執行，可能會導致中斷。

## 單一URL清除 {#single-purge}

您可以一次永久刪除單一資源，如下所示：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com/resource-path" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H 'X-AEM-Purge: soft'
```

如上述範例所示，您可以 **（選擇性）** 指定CDN是否應該執行 **強烈** 清除（預設）或 **柔和** 清除快取的物件。

預設的硬清除會使得新請求立即無法存取內容，直到從來源擷取內容為止。 軟清除會將內容標示為過時，但還是會提供給使用者端，因此使用者端不需要等到內容從來源擷取後再執行。

## 替代金鑰清除 {#surrogate-key-purge}

替代索引鍵是用於清除一組內容的唯一識別碼。 可藉由新增內容來套用至內容。 `Surrogate-Key` 標頭至回應。 可以在清除API呼叫中參考一或多個替代索引鍵。

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "Surrogate-Key: my-surrogate-key"
-H "X-AEM-Purge: soft" #optional
```

此 `Surrogate-Key`(s)以空格分隔。 與單一URL清除類似，您可以設定硬清除或軟清除。

## 完整清除 {#full-purge}

您可以依照下列步驟，完整清除所有快取資源：

```
curl
-X PURGE "https://publish-p1234-e5467.adobeaemcloud.com" \
-H 'X-AEM-Purge-Key: <my_purge_key>' \
-H "X-AEM-Purge: all"
```

請注意 `X-AEM-Purge` 標頭必須包含「all」值。

## 與Apache/Dispatcher層的互動 {#apache-layer}

如 [內容傳遞流程文章](/help/implementing/dispatcher/overview.md)時，如果快取已過期，CDN會從Apache/Dispatcher層擷取內容。 這代表在CDN上清除資源之前，您應該確保Dispatcher上也有內容的最新版本。 如需詳細資訊，另請參閱 [Dispatcher快取失效](/help/implementing/dispatcher/caching.md#disp).

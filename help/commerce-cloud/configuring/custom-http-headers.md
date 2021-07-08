---
title: 自訂HTTP標題
description: 設定自訂HTTP標題
source-git-commit: 81d6c50635813fa106f58b61c5e88560422adc65
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---


# 自訂HTTP標題 {#custom-http-headers}

## 概覽 {#overview}

為了進一步控制其後端，作者可以設定要傳送至商務引擎的自訂HTTP標題，以及CIF已傳送的標題。 常見的使用案例包括多存放區設定，您可在其中使用HTTP標題來控制商務後端的回應。

>[!NOTE]
>
>開發人員一律可使用GraphQL用戶端設定來設定自訂HTTP標題。


## 設定 {#configuration}

若要設定自訂HTTP標題，您必須先加以定義。 必須先定義自訂HTTP標題，方法是使用OSGi設定將其新增至`com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl`服務設定。

您可以在專案的「Cloud Service設定」頁面中設定HTTP標題的值：

1. 前往「工具 — >Cloud Service-> CIF設定」中的「Cloud Services設定」頁面
1. 開啟現有設定或建立新設定
1. 前往「進階」標籤，並尋找「自訂HTTP標題」多欄位。 您可以選取先前定義的標題，並為其指派值。

使用上述雲端服務設定的元件會隨著每個GraphQL請求傳送這些HTTP標題。

## 限制 {#restrictions}

雖然服務可定義任何標題名稱，包括標準名稱，但無法用於設定。 換言之，您無法使用此功能來覆寫標準HTTP標題。 可在[此處](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)找到受限標題名清單。 除了這些以外，還有兩個無法使用的標題：

* 「商店」 — 由CIF用來識別Magento商店
* 「預覽版本」 — CIF用於擷取分階段產品

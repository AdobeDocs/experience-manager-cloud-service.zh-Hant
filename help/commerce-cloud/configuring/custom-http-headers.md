---
title: 自訂 HTTP 標頭
description: 瞭解如何設定將傳送至商務引擎的自訂HTTP標頭，以及CIF已傳送的標頭。
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# 自訂 HTTP 標頭 {#custom-http-headers}

## 概觀 {#overview}

為了更能掌控其後端，作者可以設定會傳送至商務引擎的自訂HTTP標題，以及CIF已傳送的標題。 常見的使用案例包括多商店設定，您可以在其中使用HTTP標頭控制商務後端的回應。

>[!NOTE]
>
>開發人員一律可以使用GraphQL使用者端設定來設定自訂HTTP標頭。
>

## 設定 {#configuration}

若要設定自訂HTTP標頭，首先必須定義它們。 自訂HTTP標頭必須先透過使用OSGi設定將它們新增到`com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl`服務設定來定義。

您可以在專案的Cloud Service設定頁面中設定HTTP標頭的值：

1. 前往「工具>雲端服務> Cloud Service設定」中的CIF設定頁面
1. 開啟現有設定或建立設定
1. 前往「進階」索引標籤，尋找「自訂HTTP標題」多欄位。 您可以選取先前定義的標頭，並為其指派值。

使用上述雲端服務設定的元件將會隨著每個GraphQL請求傳送這些HTTP標頭。

## 限制 {#restrictions}

雖然此服務可定義任何標頭名稱，包括標準名稱，但無法加以設定。 換言之，您無法使用此功能覆寫標準HTTP標頭。 在[mdn網頁檔案 — HTTP標題](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)下可找到限制的標題名稱清單。 除了這些以外，還有兩個標頭無法使用：

* &quot;Store&quot; — 由CIF用來識別Adobe Commerce商店
* 「Preview-Version」 — 由CIF用於擷取分階段產品

---
title: 資源映射
description: 了解如何使用資源對應來定義AEM的重新導向、虛名URL和虛擬主機。
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 1a1bb23c-d1d1-4e2b-811b-753e6a90a01b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 資源映射{#resource-mapping}

資源對應可用來定義AEM的重新導向、虛名URL和虛擬主機。

例如，您可以將這些對應用於：

* 為所有要求加上前置詞 `/content` 這樣內部結構就不會被網站的訪客隱藏。
* 定義重新導向，以便 `/content/en/gateway` 網站頁面會重新導向至 `https://gbiv.com/`.

一個可能的HTTP對應會將所有要求前置詞為 `localhost:4503` with `/content`. 像這樣的對應可用來隱藏內部結構，讓網站的訪客無法看到它允許的內容：

`localhost:4503/content/we-retail/en/products.html`

以使用：

`localhost:4503/we-retail/en/products.html`

因為對應會自動新增首碼 `/content` to `/we-retail/en/products.html`.

>[!CAUTION]
>
>虛名URL不支援規則運算式模式。

>[!NOTE]
>
>請參閱Sling檔案，以及 [資源解析的映射](https://sling.apache.org/site/resources.html) 和 [資源](https://sling.apache.org/site/mappings-for-resource-resolution.html) 以取得更多資訊。

## 查看映射定義 {#viewing-mapping-definitions}

對應會形成兩個清單，JCR資源解析器會評估這些清單（由上到下）以尋找相符項目。

您可以在 **JCR ResourceResolver** Felix控制台的選項；例如， `https://<*host*>:<*port*>/system/console/jcrresolver`:

* 設定顯示目前的設定(如 [Apache Sling資源解析器](/help/overview/seo-and-url-management.md#etc-map))。

* 配置測試這允許您輸入URL或資源路徑。 按一下 **解決** 或 **地圖** 確認系統將如何轉換項目。

* **解析器對應項目**
ResourceResolver.resolve方法將URL映射至資源所使用的項目清單。

* **映射映射條目**
ResourceResolver.map方法用來將資源路徑對應至URL的項目清單。

這兩個清單顯示各種條目，包括由應用程式定義為預設的條目。 這通常是為了簡化使用者的URL。

清單配對 **圖樣**，此規則運算式與請求相符，具有 **取代** 定義對強加的重定向。

例如：

**圖樣** `^[^/]+/[^/]+/welcome$`

將觸發：

**取代** `/libs/cq/core/content/welcome.html`.

若要重新導向請求：

`https://localhost:4503/welcome` &quot;

至:

`https://localhost:4503/libs/cq/core/content/welcome.html`

系統會在存放庫內建立新的對應定義。

>[!NOTE]
>
>有許多資源可協助說明如何定義規則運算式；例如 [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### 在AEM中建立對應定義 {#creating-mapping-definitions-in-aem}

在標準的AEM安裝中，您可以找到資料夾：

`/etc/map/http`

這是定義HTTP通訊協定的對應時使用的結構。 其他資料夾( `sling:Folder`)可在下建立 `/etc/map` 來對應任何其他通訊協定。

#### 設定內部重新導向至/content {#configuring-an-internal-redirect-to-content}

建立將任何要求加上前置詞的對應至https://localhost:4503/ `/content`:

1. 使用CRXDE導覽至 `/etc/map/http`.

1. 建立新節點：

   * **類型** `sling:Mapping`
此節點類型用於此類映射，但其用途不是強制性的。

   * **名稱** `localhost_any`

1. 按一下 **全部儲存**.
1. **新增** 此節點的以下屬性：

   * **名稱** `sling:match`

      * **類型** `String`

      * **值** `localhost.4503/`
   * **名稱** `sling:internalRedirect`

      * **類型** `String`

      * **值** `/content/`


1. 按一下 **全部儲存**.

這會處理下列請求：
`localhost:4503/geometrixx/en/products.html`
如同：
`localhost:4503/content/geometrixx/en/products.html`
被請求。

>[!NOTE]
>
>請參閱 [資源](https://sling.apache.org/site/mappings-for-resource-resolution.html) ，取得可用sling屬性及其設定方式的詳細資訊。
>例如， [字串插值](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html#string-interpolation-for-etcmap) 非常實用，因為它可設定透過環境變數根據環境值取得的對應。

>[!NOTE]
>
>您可以使用 `/etc/map.publish` 以保留發佈環境的設定。 然後，必須複製這些檔案，並將新位置( `/etc/map.publish`) **映射位置** 的 [Apache Sling資源解析器](/help/overview/seo-and-url-management.md#etc-map) 的子句。

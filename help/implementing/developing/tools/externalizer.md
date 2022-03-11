---
title: 外部化URL
description: Externalizer是OSGi服務，它允許您以寫程式方式將資源路徑轉換為外部和絕對URL。
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# 外部化URL {#externalizing-urls}

在AEM中 **外部化器** 是一種OSGi服務，它允許您以寫程式方式轉換資源路徑(例如， `/path/to/my/page`)到外部和絕對URL(例如， `https://www.mycompany.com/path/to/my/page`)，方法是使用預配置的DNS預先固定路徑。

由於AEMas a Cloud Service實例無法知道其外部可見URL，並且由於有時必須在請求範圍之外建立連結，因此此服務提供了一個中心位置來配置這些外部URL並生成它們。

本文介紹如何配置Externalizer服務以及如何使用它。 有關服務的技術詳細資訊，請參閱 [賈瓦多克](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html)。

## 外部化器的預設行為及如何覆蓋 {#default-behavior}

出廠設定後，Externalizer服務具有如 `author-p12345-e6789.adobeaemcloud.com` 和 `publish-p12345-e6789.adobeaemcloud.com`。

要覆蓋此類值，請使用文章中所述的Cloud Manager環境變數 [配置OSGiAEM以as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) 並設定預定義 `AEM_CDN_DOMAIN_AUTHOR` 和 `AEM_CDN_DOMAIN_PUBLISH` 變數。

## 配置外部化程式服務 {#configuring-the-externalizer-service}

Externalizer服務允許您集中定義可用於以寫程式方式為資源路徑前置詞的域。 Externalizer服務應僅用於具有單個域的應用程式。

>[!NOTE]
>
>應用任何 [OSGi配置AEM用於as a Cloud Service,](/help/implementing/deploying/overview.md#osgi-configuration) 應對本地開發人員實例執行以下步驟，然後提交到您的項目代碼進行部署。

要定義Externalizer服務的域映射，請執行以下操作：

1. 通過以下方式導航到Configuration Manager:

   `https://<host>:<port>/system/console/configMgr`

1. 按一下 **第CQ天連結外部化程式** 的子菜單。

   ![外部化程式OSGi配置](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >到配置的直接連結是 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. 定義 **域** 映射。 映射由唯一名稱組成，該名稱可在代碼中用於引用域、空間和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   位置：

   * **`scheme`** 通常是http或https，但可以是其他協定。

      * 建議使用https強制https連結。
      * 如果客戶端代碼在請求將URL外部化時未覆蓋方案，則將使用它。
   * **`server`** 是主機名（域名或ip地址）。
   * **`port`** （可選）是埠號。
   * **`contextpath`** （可選）僅當作為Webapp安裝AEM在其他上下文路徑下時才設定。

   例如：`production https://my.production.instance`

   以下映射名稱是預定義的，必須始終根據它們AEM進行設定：

   * `local`  — 本地實例
   * `author`  — 創作系統DNS
   * `publish`  — 面向公眾的網站DNS

   >[!NOTE]
   >
   >自定義配置允許您添加新類別，如 `production`。 `staging` 甚至外部非系AEM統，例如 `my-internal-webservice`。 避免在項目代碼庫的不同位置對此類URL進行硬編碼是非常有用的。

1. 按一下 **保存** 的子菜單。

### 使用Externalizer服務 {#using-the-externalizer-service}

本節顯示了如何使用Externalizer服務的幾個示例。

>[!NOTE]
>
>不應在HTML上下文中建立絕對連結。 因此，不應在此類情況下使用此實用程式。

* **要將路徑與「publish」域外部化：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假定域映射：

   * `publish https://www.website.com`

   * `myExternalizedUrl` 最後是值：

   * `https://www.website.com/contextpath/my/page.html`

* **要將路徑與「author」域外部化：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假定域映射：

   * `author https://author.website.com`

   * `myExternalizedUrl` 最後是值：

   * `https://author.website.com/contextpath/my/page.html`

* **要將路徑與「local」域外部化：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假定域映射：

   * `local https://publish-3.internal`

   * `myExternalizedUrl` 最後是值：

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>可以在 [賈瓦多克](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html)。

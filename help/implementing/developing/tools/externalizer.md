---
title: 外部化URL
description: Externalizer是一項OSGi服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL。
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# 外部化URL {#externalizing-urls}

在AEM中，**外部化程式**&#x200B;是OSGi服務，可讓您以程式設計方式將資源路徑（例如`/path/to/my/page`）轉換為外部和絕對URL （例如`https://www.mycompany.com/path/to/my/page`），方法是以預先設定的DNS為路徑加上前置詞。

由於AEM as a Cloud Service執行個體無法知道其外部可見的URL，並且有時必須在請求範圍之外建立連結，此服務會提供中央位置來設定這些外部URL並建置它們。

本文說明如何設定Externalizer服務及其使用方法。 如需服務的技術詳細資訊，請參閱[Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html)。

## 外部化程式的預設行為以及如何覆寫 {#default-behavior}

Externalizer服務可立即將數個網域識別碼對應至絕對URL首碼，這些首碼與已針對環境產生的AEM服務URL相符，例如`author https://author-p12345-e6789.adobeaemcloud.com`和`publish https://publish-p12345-e6789.adobeaemcloud.com`。 每個預設網域的基礎URL都會從Cloud Manager定義的環境變數中讀取。

若需參考，`com.day.cq.commons.impl.ExternalizerImpl.cfg.json`的預設OSGi設定實際上為：

```json
{
   "externalizer.domains": [
      "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
      "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
      "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]",
      "preview $[env:AEM_EXTERNALIZER_PREVIEW;default=http://localhost:4503]"
   ]
}
```

>[!CAUTION]
>
>OSGi設定中的預設`local`、`author`、`preview`和`publish`外部化程式網域對應必須保留上述原始`$[env:...]`值。
>
>將自訂`com.day.cq.commons.impl.ExternalizerImpl.cfg.json`檔案部署到AEM as a Cloud Service時，若省略這些現成可用的網域對應，可能會導致無法預測的應用程式行為。

請勿在Cloud Manager中定義或覆寫`EXTERNALIZER`個環境變數（例如`AEM_EXTERNALIZER_AUTHOR`）。 如果您需要覆寫`publish`或`preview`網域值，請定義並使用`AEM_CDN_DOMAIN_PUBLISH`和`AEM_CDN_DOMAIN_PREVIEW`環境變數。 啟動期間，這些變數會自動指派給外部器設定中的對應欄位。

<!-- Alexandru: hiding this. See CQDOC-23014 for more details

To override the `preview` and `publish` values, use Cloud Manager environment variables as described in the article [Configuring OSGi for AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) and setting the predefined `AEM_CDN_DOMAIN_PUBLISH` and `AEM_CDN_DOMAIN_PREVIEW` variables. -->

## 設定Externalizer服務 {#configuring-the-externalizer-service}

Externalizer服務可讓您集中定義網域，以程式設計方式為資源路徑加上前置詞。 Externalizer服務只應用於具有單一網域的應用程式。

>[!NOTE]
>
>如同為AEM as a Cloud Service[套用任何](/help/implementing/deploying/overview.md#osgi-configuration)OSGi設定一樣，下列步驟應該在本機開發人員執行個體上執行，然後提交至您的專案程式碼以進行部署。

若要定義Externalizer服務的網域對應：

1. 透過以下方式導覽至Configuration Manager：

   `https://<host>:<port>/system/console/configMgr`

1. 按一下&#x200B;**Day CQ Link Externalizer**&#x200B;以開啟設定對話方塊。

   ![外部化程式OSGi設定](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >設定的直接連結是`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. 定義&#x200B;**網域**&#x200B;對應。 對應包含唯一名稱，可用於程式碼中參考網域、空格和網域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **`scheme`**&#x200B;通常是http或https，但可以是另一個通訊協定。

      * Adobe建議使用https來強制執行https連結。
      * 若使用者端代碼在要求外部化URL時未覆寫配置，則會使用它。

   * **`server`**&#x200B;是主機名稱（網域名稱或ip位址）。
   * **`port`** （選擇性）是連線埠號碼。
   * **`contextpath`** （選擇性）只有在將AEM安裝為Webapp時才會設定。

   例如：`production https://my.production.instance`

   下列對應名稱為預先定義，一律必須設定為AEM依賴這些名稱：

   * `local` — 本機執行個體
   * `author` — 編寫系統DNS
   * `publish` — 面向公眾的網站DNS

   >[!NOTE]
   >
   >自訂組態可讓您新增類別，例如`production`、`staging`，甚至外部非AEM系統，例如`my-internal-webservice`。 避免在專案的程式碼基底中跨不同位置對這類URL進行硬式編碼很有用。

1. 按一下[儲存]儲存變更。**&#x200B;**

### 使用Externalizer服務 {#using-the-externalizer-service}

本節顯示幾個如何使用Externalizer服務的範例。

>[!NOTE]
>
>HTML內容中不應建立任何絕對連結。 因此，請勿在這種情況下使用此公用程式。

* **若要外部化具有&#39;publish&#39;網域的路徑：**

  ```java
  String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
  ```

  假設網域對應：

   * `publish https://www.website.com`

   * `myExternalizedUrl`結尾是值：

   * `https://www.website.com/contextpath/my/page.html`

* **若要外部化具有&#39;author&#39;網域的路徑：**

  ```java
  String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
  ```

  假設網域對應：

   * `author https://author.website.com`

   * `myExternalizedUrl`結尾是值：

   * `https://author.website.com/contextpath/my/page.html`

* **若要外部化具有&#39;local&#39;網域的路徑：**

  ```java
  String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
  ```

  假設網域對應：

   * `local https://publish-3.internal`

   * `myExternalizedUrl`結尾是值：

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>您可以在[Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html)中找到更多範例。

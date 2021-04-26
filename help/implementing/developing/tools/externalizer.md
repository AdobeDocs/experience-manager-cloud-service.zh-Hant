---
title: 外部化URL
description: Externalizer是OSGi服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL。
translation-type: tm+mt
source-git-commit: 4c584ceadaa358120d1d4b4cabd7e21ced814b31
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# 將URL外部化{#externalizing-urls}

在中AEM,**Externalizer**&#x200B;是一種OSGi服務，允許您以寫程式方式轉換資源路徑(例如，`/path/to/my/page`)，以預先設定的DNS來預先固定路徑，以匯入外部和絕對URL（例如`https://www.mycompany.com/path/to/my/page`）。

由於AEM作為Cloud Service實例無法知道其外部可見的URL，而且有時必須在請求範圍之外建立連結，因此此服務提供了一個集中位置來配置這些外部URL並構建它們。

本文將說明如何設定Externalizer服務，以及如何使用它。 有關服務的技術詳細資訊，請參閱[Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html)。

## Externalizer的預設行為及如何覆蓋{#default-behavior}

現成可用的Externalizer服務已設定`author-p12345-e6789.adobeaemcloud.com`和`publish-p12345-e6789.adobeaemcloud.com`等值，如此您作為Cloud Service安裝程式時，就AEM可以使用自訂網域。

若要覆寫這些值，請使用[「將OSGi設定為Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties)」文章中所述的Cloud Manager環境變數，並設定預先定義的`AEM_CDN_DOMAIN_AUTHOR`和`AEM_CDN_DOMAIN_PUBLISH`變數。

## 配置Externalizer服務{#configuring-the-externalizer-service}

Externalizer服務允許您集中定義可用於以寫程式方式為資源路徑前置詞的域。 Externalizer服務僅適用於具有單一網域的應用程式。

>[!NOTE]
>
>如同將任何[OSGi組態套用為AEMCloud Service時，](/help/implementing/deploying/overview.md#osgi-configuration)應對本機開發人員例項執行下列步驟，然後將其提交至您的專案程式碼以進行部署。

要定義Externalizer服務的域映射，請執行以下操作：

1. 通過以下方式導航到配置管理器：

   `https://<host>:<port>/system/console/configMgr`

1. 按一下&#x200B;**Day CQ Link Externalizer**&#x200B;開啟配置對話框。

   ![Externalizer OSGi組態](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >配置的直接連結為`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. 定義&#x200B;**Domains**&#x200B;映射。 映射由唯一名稱組成，可用於代碼中以引用域、空間和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **`scheme`** 通常為http或https，但可以是其他通訊協定。

      * 建議使用https來強制https連結。
      * 當要求將URL外部化時，如果用戶端程式碼未覆寫配置，則會使用它。
   * **`server`** 是主機名（域名或IP地址）。
   * **`port`** （可選）是埠號。
   * **`contextpath`** （可選）只有在安裝為不同AEM上下文路徑下的網頁應用程式時才設定。

   例如：`production https://my.production.instance`

   以下映射名稱是預先定義的，必須始終根據這些名稱AEM進行設定：

   * `local` -本機例項
   * `author` -編寫系統DNS
   * `publish` -公眾對應網站DNS

   >[!NOTE]
   >
   >自訂組態可讓您新增新類別，例如`production`、`staging`或甚至外部非系統，AEM例如`my-internal-webservice`。 避免在專案的程式碼基底中不同位置對此類URL進行硬式編碼，是很有用的。

1. 按一下&#x200B;**保存**&#x200B;保存更改。

### 使用Externalizer服務{#using-the-externalizer-service}

本節顯示如何使用Externalizer服務的一些示例。

>[!NOTE]
>
>不應在HTML內容中建立絕對連結。 因此，在這種情況下不應使用此實用程式。

* **若要將路徑外部化為具有「發佈」網域：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假設域映射：

   * `publish https://www.website.com`

   * `myExternalizedUrl` 最後是值：

   * `https://www.website.com/contextpath/my/page.html`

* **要將具有「author」域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假設域映射：

   * `author https://author.website.com`

   * `myExternalizedUrl` 最後是值：

   * `https://author.website.com/contextpath/my/page.html`

* **要將具有「本地」域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假設域映射：

   * `local https://publish-3.internal`

   * `myExternalizedUrl` 最後是值：

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>您可以在[Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html)中找到更多示例。

---
title: 將URL外部化
description: Externalizer是OSGi服務，可讓您以程式設計方式將資源路徑轉換為外部和絕對URL。
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: ce43bdc94f14faa69add16139e22ea3f34dfc52f
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# 將URL外部化{#externalizing-urls}

在AEM中，**Externalizer**&#x200B;是OSGi服務，可讓您以程式設計方式轉換資源路徑(例如`/path/to/my/page`)填入外部和絕對URL（例如`https://www.mycompany.com/path/to/my/page`），方法是使用預先設定的DNS來預先修正路徑。

由於AEM作為Cloud Service例項無法知道其外部可見的URL，且由於有時必須在請求範圍外建立連結，因此此服務提供一個集中位置，可設定這些外部URL並建置這些URL。

本文說明如何配置Externalizer服務及如何使用它。 有關該服務的技術詳細資訊，請參閱[Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html)。

## Externalizer的預設行為和How to Override {#default-behavior}

現成可用的Externalizer服務具有`author-p12345-e6789.adobeaemcloud.com`和`publish-p12345-e6789.adobeaemcloud.com`等值。

若要覆寫這些值，請使用[為AEM設定OSGi作為Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties)一文所述的Cloud Manager環境變數，並設定預先定義的`AEM_CDN_DOMAIN_AUTHOR`和`AEM_CDN_DOMAIN_PUBLISH`變數。

## 配置Externalizer服務{#configuring-the-externalizer-service}

Externalizer服務允許您集中定義可用於以寫程式方式為資源路徑前置詞的域。 Externalizer服務僅應用於具有單個域的應用程式。

>[!NOTE]
>
>如同套用AEM as aCloud Service的任何[OSGi設定時，](/help/implementing/deploying/overview.md#osgi-configuration)應在本機開發人員執行個體上執行下列步驟，然後提交至您的專案程式碼以進行部署。

要定義Externalizer服務的域映射，請執行以下操作：

1. 透過以下網址導覽至Configuration Manager:

   `https://<host>:<port>/system/console/configMgr`

1. 按一下&#x200B;**Day CQ Link Externalizer**&#x200B;以開啟設定對話方塊。

   ![Externalizer OSGi配置](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >配置的直接連結為`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. 定義&#x200B;**Domains**&#x200B;對應。 映射由唯一名稱組成，該名稱可用於代碼中以引用域、空格和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **`scheme`** 通常是http或https，但可以是其他通訊協定。

      * 建議使用https強制https連結。
      * 若要求將URL外部化時用戶端代碼未覆寫配置，則會使用此URL。
   * **`server`** 是主機名（域名或ip地址）。
   * **`port`** （可選）是埠號。
   * **`contextpath`** （選用）只有在AEM安裝為位於不同內容路徑下的網頁應用程式時才會設定。

   例如：`production https://my.production.instance`

   下列對應名稱是預先定義的，且必須一律設定，因為AEM需仰賴這些名稱：

   * `local`  — 本機執行個體
   * `author`  — 編寫系統DNS
   * `publish`  — 公開對應的網站DNS

   >[!NOTE]
   >
   >自訂設定可讓您新增新類別，例如`production`、`staging`或甚至外部非AEM系統，例如`my-internal-webservice`。 建議您避免在專案的程式碼基底中不同位置對這類URL進行硬式編碼。

1. 按一下&#x200B;**儲存**&#x200B;以儲存變更。

### 使用Externalizer服務{#using-the-externalizer-service}

本節介紹如何使用Externalizer服務的一些示例。

>[!NOTE]
>
>不應在HTML內容中建立絕對連結。 因此，不應在此類情況下使用此實用程式。

* **若要將具有&#39;publish&#39;網域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `publish https://www.website.com`

   * `myExternalizedUrl` 結尾為值：

   * `https://www.website.com/contextpath/my/page.html`

* **若要將具有「作者」網域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假設網域對應：

   * `author https://author.website.com`

   * `myExternalizedUrl` 結尾為值：

   * `https://author.website.com/contextpath/my/page.html`

* **要將具有&#39;local&#39;域的路徑外部化：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假設網域對應：

   * `local https://publish-3.internal`

   * `myExternalizedUrl` 結尾為值：

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>您可以在[Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html)中找到更多範例。

---
title: 無管道 URL 重新導向
description: 瞭解如何宣告301或302重新導向，而不需要存取Git或Cloud Manager管道。
feature: Dispatcher
role: Admin
exl-id: dacb1eda-79e0-4e76-926a-92b33bc784de
source-git-commit: 7a543c8fe63166ef34999f23ce9b05de8e8b0e9f
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# 無管道 URL 重新導向 {#pipeline-free-redirects}

由於各種原因，組織會重新寫入URL，引發301 （或302）重新導向，亦即瀏覽器會重新導向至不同頁面。

案例包括：

* 已移除HTML頁面，因此使用者會被帶往替代頁面（有時是首頁），而不會看到`404 Page Not Found`錯誤。
* 已重新命名的HTML頁面。
* SEO最佳化。

AEM as a Cloud Service提供[數個實作伺服器端重新導向的方法](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/administration/url-redirection)，不過本文所述的策略（管線免費重新導向）在以下情況下是很好的選擇：

* 維護重新導向的使用者為商務使用者，他們沒有認可原始檔控制檔案變更的必要存取權，或無法執行Cloud Manager Web層設定管道。
* 重新導向的次數範圍從數到數萬不等。
* 您想要使用者介面的選項，建立為自訂專案或使用[ACS Commons重新導向對應管理員](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html)或[ACS Commons重新導向管理員](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html)。

此功能的核心是AEM Apache/Dispatcher可載入（或重新載入）一或多個已放置在發佈存放庫內指定位置中的重寫對應檔案(以便從AEM發佈下載)。 請務必注意，檔案的傳送方式並不屬於此功能的範圍，但您可以考慮下列其中一個方法：

* 在作者使用者介面中擷取重新寫入對映作為資產並進行發佈。
* 安裝[ACS Commons重新導向對應管理員](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html) （[至少6.7.0版或更新版本](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)），其中包含管理URL對應的使用者介面，也可以發佈重寫對應檔案。
* 安裝[ACS Commons Redirect Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-manager/subpages/rewritemap.html) （[至少6.10.0版或更新版本](https://github.com/Adobe-Consulting-Services/acs-aem-commons/releases)），其中也包含管理URL對應的使用者介面，也可以發佈重寫對應檔案。
* 撰寫自訂應用程式，提供完整的彈性。 例如，使用使用者介面或命令列介面來管理url對應，或是使用表單來上傳重寫對應，接著使用AEM API來發佈重寫對應檔案。

>[!NOTE]
> 此功能需要AEM版本&#x200B;**18311或更新版本**。

>[!NOTE]
> 此功能使用重新導向地圖管理員需要ACS Commons版本&#x200B;**6.7.0或更新版本**，而使用重新導向管理員需要版本&#x200B;**6.10.0或更新版本**。

如需詳細的逐步實作指南，請參閱[實作管道免費URL重新導向](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects)教學課程。

## 重寫對應 {#rewrite-map}

根據預設，Apache HTTP伺服器每300秒會重新載入重寫對應（如果已變更） （可設定此值）。 檔案格式應遵循[Apache檔案](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt)中說明的純文字索引鍵值對應RewriteMap檔案格式。

應建立名為`managed-rewrite-maps.yaml`的檔案，以指定重寫對應檔案的位置，而且必須使用Cloud Manager完整棧疊管道或Web層管道來部署一次。 必須在排程程式設定的[src/選擇加入](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in)資料夾中建立檔案。 請確定您使用[彈性模式檔案結構](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure)。

您可以使用以下模式來設定：

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

例如，如果您選擇用來放置重寫對應檔案的方法是將它作為名為`mysite-redirectmap.txt`的資產擷取到AEM中，然後發佈，則可以在`/content/dam`下指定資料夾：

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

接下來，在Apache設定檔（例如`rewrites/rewrite.rules`或`<yourfile>.vhost`）中，您必須設定名稱屬性參考的對應檔（上述範例中的`my.map`）。 載入後，此對應檔案會儲存在&#x200B;**固定**&#x200B;位置`/tmp/rewrites/`下的Dispatcher本機儲存體中。

`RewriteMap`指示詞應指出資料是以`sdbm` （簡單DBM）格式儲存在資料庫管理員(DBM)檔案格式中，而完整的檔案路徑是從儲存位置首碼和name屬性衍生而來。

其餘組態取決於`redirectmap.txt`的格式。 最簡單的格式（如下面的範例所示）是原始url與對應url之間的一對一對應：

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```

## 考量事項 {#considerations}

請牢記以下事項：

* 依預設，載入重寫對應時，Apache會啟動而不等待完整對應檔案載入，因此在完整對應載入之前可能會暫時出現不一致的情況。 您可以變更此設定，讓Apache等待完整地圖內容載入，但Apache需要更長的時間啟動。 若要變更此行為以便Apache等待，請新增`wait:true`至`managed-rewrite-maps.yaml`檔案。
* 若要變更載入之間的頻率，請新增`ttl: <integer>`至`managed-rewrite-maps.yaml`檔案。 例如：`ttl: 120`。
* Apache對RewriteMap單一專案具有1024長度限制。

## 教學課程 {#tutorials}

1. [正在實作無管道URL重新導向](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/administration/implementing-pipeline-free-url-redirects)
1. [URL重新導向](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/foundation/administration/url-redirection)

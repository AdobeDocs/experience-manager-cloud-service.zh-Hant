---
title: 元件和 GraphQL 清除快取
description: 瞭解如何在AEM CIF中啟用及驗證清除快取功能。
feature: Commerce Integration Framework
role: Admin
exl-id: f89c07c7-631f-41a4-b5b9-0f629ffc36f0
source-git-commit: fb8b2645c0401d1358c7751db03a138dc2de2664
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 3%

---

# 元件和 GraphQL 清除快取 {#clear-cache}

本檔案提供在AEM CIF中啟用及驗證清除快取功能的完整指南。

>[!NOTE]
>
> 此功能屬於實驗性質。

## 在CIF設定中啟用清除快取功能 {#enable-clear-cache}

依預設，CIF設定中的清除快取功能會停用。 若要啟用此功能，您必須將下列專案新增至對應的專案：

* 啟用servlet `/bin/cif/invalidate-cache`，協助您在專案中新增`com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json`設定，以觸發清除快取API及其對應要求，如[這裡](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config.author/com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json)所示。
  >[!NOTE]
  >
  > 僅需要為作者執行個體啟用設定。

* 啟用接聽程式，以在您的專案中新增`com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json`設定，以清除每個AEM執行個體（發佈與作者）的快取，如[這裡](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json)所示。
   * 作者和發佈執行個體皆應啟用設定。
   * 啟用Dispatcher快取（選用）：您可以透過在上述設定中將`enableDispatcherCacheInvalidation`屬性設定為true來啟用Dispatcher清除快取設定。 這提供了從Dispatcher清除快取的功能。

     >[!NOTE]
     >
     > 這僅適用於發佈執行個體。

   * 此外，請務必提供適合您的產品、類別和CMS頁面的對應模式，以便將其新增至上述設定檔案，從Dispatcher快取中移除。

* 若要改善SQL查詢效能，以尋找與產品和類別相關的對應頁面，請在專案中新增對應的索引（建議）。 如需詳細資訊，請參閱[cifCacheInvalidationSupport](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.apps/src/main/content/jcr_root/_oak_index/cifCacheInvalidationSupport/.content.xml)。

## 驗證清除快取功能 {#verify-clear-cache}

若要確認所有專案皆已正確設定：

* 觸發對應servlet至作者執行個體AEM，例如[http://localhost:4502/bin/cif/invalidate-cache](http://localhost:4502/bin/cif/invalidate-cache)，您應該會收到200 HTTP回應。
* 確認已在作者執行個體中的下列路徑下建立節點： `/var/cif/cacheinvalidation`。 節點名稱遵循此模式： `cmd_{{timestamp}}`。
* 確認已在每個發佈執行個體中建立相同的節點。

現在，若要檢查是否已正確清除快取：
1. 導覽至對應的PLP和PDP頁面。
2. 更新商務引擎中的產品或類別名稱。 根據快取設定，變更不會立即反映在AEM中。
3. 觸發servlet API，如下所示：

   ```
   curl --location '{Author AEM Instance Url}/bin/cif/invalidate-cache' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: ••••••' \ // Mandatory
   --header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
   --data '{
       "productSkus": ["Sku1", "Sku2"], // Optional: Pass the corresponding sku which got updated.
       "categoryUids":["CategoryUid"], // Optional : Pass the corresponding category-uid which got updated.
       "storePath": "/content/venia/us/en", // Mandatory : Needs to be given to know for which site we are removing the clear cache.
   }'
   ```

如果一切順利，新變更會反映在每個執行個體中。 如果變更在發佈執行個體上不可見，請嘗試在私人/無痕瀏覽器視窗中存取相關的PLP和PDP頁面。

>[!NOTE]
>
> 發佈執行個體可以有多個層級的快取階層。 此功能只負責從AEM內部記憶體和Dispatcher清除快取。

## 清除快取失效API {#clear-cache-api}

每當您想要從AEM清除商務相關資料的快取時，都必須觸發此API。

要求型別： `POST`

### 標頭

| 參數 | 值 | 必要/必要 | 評論 |
|------------------------------|-------------------|---|---|
| `Content-Type` | `application/json` | 必要 |  |
| `Authorization` | 對應作者的使用者認證（驗證型別：基本驗證） | 必要 | 新增對應的使用者名稱和密碼。 |


### 總額

下表顯示特徵現成可用的現有屬性。 這些`InvalidateType`屬性必須結合必要屬性（例如`storePath`）一起提供。

| `invalidateType` | 值 | 型別（陣列/字串/布林值） | 這是否會清除Dispatcher快取？ | 評論 |
|------------------------------|-------------------|---|---|---|
| `productSkus` | 產品的SKU — 需要從快取中失效。 | 陣列 | 是 | 使用下列模式從內部記憶體中清除快取：<br>```"\"sku\":\\s*\""```<br>Dispatcher<br><ul><li>清除對應SKU的PDP頁面快取</li><li>清除其所在之對應類別頁面的快取（根據來自商務的graphql回應）</li><li>根據下列查詢清除快取：</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content, '{storePath}')<br>AND ( (content.[product] IN ('sku1','sku2') AND content.[productType] = 'combinedSku')<br> OR (content.[selection] IN ('sku1','sku2') AND content.[selectionType] IN ('combinedSku', 'sku')))``` |
| `categoryUids` | 類別的uid — 需要從快取中失效。 | 陣列 | 是 | 使用下列模式從內部記憶體中清除快取：<br>```"\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\""```<br>Dispatcher<br><ul><li>清除對應資料的類別頁面快取（包括其子類別頁面）</li><li>清除具有對應類別的所有PDP頁面</li><li>根據下列查詢清除快取：</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content,'{storePath}')<br>AND ((content.[categoryId] in ('category1','category2')<br>AND content.[categoryIdType] in ('uid'))<br>OR (content.[category] in ('category1','category2') AND content.[categoryType] in ('uid')))``` |
| `regexPatterns` | 如果您需要根據規則運算式模式清除GraphQL回應資料，請使用此選項。 | 陣列 | 否 | |
| `cacheNames` | 此值是在對應的CIF GraphQL使用者端設定工廠>>對應的StorePath GraphQL設定>> GraphQL快取設定下定義 | 陣列 | 否 | |
| `invalidateAll` | True或false | 布林值 | 是 | |

此表格顯示每個API呼叫中需要傳遞的強制屬性：

| 屬性 | 值 | 型別（陣列/字串/布林值） | 這是否會清除Dispatcher快取？ | 評論 |
|------------------------------|-------------------|---|---|---|
| `storePath` | 需要移除快取的網站路徑對應值（範例： `/content/venia/us/en`作為與venia專案的參考）。 | 字串 | 是 | 需要以`invalidateType.`的組合提供此專案 |

### 範例API請求

```
curl --location 'https://author-p10603-e145552-cmstg.adobeaemcloud.com/bin/cif/invalidate-cache' \
--header 'Content-Type: application/json' \
--header 'Authorization: ••••••' \
--header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
--data '{
"productSkus": ["VP01", "VT10"], // This will clear cache for the corresponding pages related with mentioned skus.
"categoryUids":["Mjk="], // This will clear cache for the corresponding pages related with mentioned categories.
"regexPatterns":["\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\"(Mjk=)\"", "\"sku\":\\s*\"(VP02|VP03)\""],
"cacheNames": ["venia/components/commerce/product"], // If this been added then it will clear respective caches for the corresponding storepath
"storePath": "/content/venia/us/en"
}'
```

## 擴展性 {#clear-cache-extensibility}

此功能不僅提供其核心功能，也提供擴充功能，讓開發人員可視需要建置及進一步自訂。

### 擴充現有屬性 {#existing-attribute}

如果需要清除目前未由現有屬性型功能（例如`categoryUids`）涵蓋的快取，您可以參考[此參考檔案](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/ExtendedCategoryUidInvalidation.java)來新增模式，並定義應從快取中清除的其他`invalidatePaths` （超出目前實作處理的範圍）。

### 新增自訂屬性 {#new-custom-attribute}

例如，如果您不想使用現有屬性來清除快取，則您可以彈性建立自己的屬性並定義其對應的功能。

* 如果您只需要從AEM的內部記憶體（graphql回應）清除快取，則您需要遵循[此參考](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomInvalidation.java)。
* 如果您需要從內部記憶體和Dispatcher快取中清除快取，則必須遵循[此參考](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomDispatcherInvalidation.java)。
  >[!NOTE]
  >
  > 您可以傳回`getPatterns()`方法的`null`，以忽略內部清除快取。

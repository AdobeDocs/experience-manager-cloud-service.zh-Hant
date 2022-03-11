---
title: Content Services的JSON導出器
description: Content Services旨在AEM將內容的描述和交付範圍從關注網AEM頁的範圍延伸出來。 它們使用可供任何客戶使用的標準化方法，將內AEM容交付到非傳統網頁的渠道。
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 5%

---

# Content Services的JSON導出器 {#json-exporter-for-content-services}

Content Services旨在AEM將內容的描述和交付範圍擴展到網頁AEM的焦點之外。

它們使用可供任何客戶使用的標準化方法，將內AEM容交付到非傳統網頁的渠道。 這些渠道可以包括：

* 單頁應用程式
* 本機移動應用程式
* 外部的其他通道和觸AEM點

使用使用結構化內容的內容片段，您可以通過使用JSON導出器以JSON資料模型格式傳遞(y)頁AEM的內容來提供內容服務。 這樣，您自己的應用程式就可以使用它。

## 包含內容片段核心元件的JSON導出器 {#json-exporter-with-content-fragment-core-components}

使用AEMJSON導出器，您可以以JSON資料模型格式AEM傳遞(y)頁的內容。 這樣，您自己的應用程式就可以使用它。

在交AEM貨中使用選擇器實現 `model` 和 `.json` 擴展。

`.model.json`

1. 例如，URL，如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. 將提供內容，如：

   ![WKND內容的JSON模型](assets/json-model-wknd.png)

或者，可以通過將結構化內容片段的內容指定為特定目標來傳遞該內容。

這是使用片段的整個路徑(通過 `jcr:content`);例如，帶有尾碼，如。

`.../jcr:content/root/container/container/contentfragment.model.json`

您的頁面可以包含單個內容片段或多種類型的多個元件。 也可以使用清單元件等機制自動搜索相關內容。

* 例如，URL，如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* 將提供內容，如：

   ![WKND內容片段的JSON模型](assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >你可以 [調整自己的元件](enabling-json-exporter.md) 訪問和使用此資料。

   >[!NOTE]
   >
   >雖然不是標準實施， [支援多個選擇器，](enabling-json-exporter.md#multiple-selectors) 但 `model` 肯定是第一個。

### 更多資訊 {#further-information}

另請參閱:

* Assets HTTP API
   * [資產HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling 模型:
   * [Sling Models — 將模型類與自130以來的資源類型關聯](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEMJSON:
   * [為元件啟用JSON導出](enabling-json-exporter.md)

## 相關文檔 {#related-documentation}

有關詳細資訊，請參閱：

* [資產使用手冊中的內容片段](/help/assets/content-fragments/content-fragments.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段創作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 和 [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

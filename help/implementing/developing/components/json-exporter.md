---
title: 內容服務的JSON匯出器
description: AEM Content Services的設計目的，是將AEM中／來自AEM的內容描述和傳送，從而延伸到網頁。 它們使用可供任何用戶端使用的標準化方法，將內容傳送至非傳統AEM網頁的頻道。
translation-type: tm+mt
source-git-commit: 02d95b7c45cb4d6d2fbfd9699690ecc1b80e1202
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 5%

---


# 內容服務的JSON匯出器 {#json-exporter-for-content-services}

AEM Content Services的設計目的，是將AEM中／來自網頁的內容描述和傳送概括化，使其超出網頁的重點。

它們使用可供任何用戶端使用的標準化方法，將內容傳送至非傳統AEM網頁的頻道。 這些渠道可以包括：

* 單頁應用程式
* 原生行動應用程式
* AEM外部的其他通道和觸點

透過使用結構化內容的內容片段，您可以使用JSON匯出器來提供內容服務，以JSON資料模型格式傳送(y)AEM頁面的內容。 然後，您自己的應用程式就可使用這個功能。

## 包含內容片段核心元件的JSON匯出器 {#json-exporter-with-content-fragment-core-components}

使用AEM JSON匯出器，您可以以JSON資料模型格式傳送(y)AEM頁面的內容。 然後，您自己的應用程式就可使用這個功能。

在AEM中，使用選擇器和擴充功能來 `model` 達成 `.json` 傳送。

`.model.json`

1. 例如，URL，例如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. 將提供內容，例如：

   ![WKND內容的JSON模型](/help/implementing/developing/introduction/assets/json-model-wknd.png)

您也可以透過明確定位結構化內容片段來提供內容。

這是使用片段的整個路徑(透過 `jcr:content`);例如，加上尾碼，如。

`.../jcr:content/root/container/container/contentfragment.model.json`

您的頁面可以包含單一內容片段或多種類型的元件。 您也可以使用清單元件等機制，自動搜尋相關內容。

* 例如，URL，例如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* 將提供內容，例如：

   ![WKND內容片段的JSON模型](/help/implementing/developing/introduction/assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >您可以 [調整自己的元件](enabling-json-exporter.md) ，以存取和使用此資料。

   >[!NOTE]
   >
   >雖然不是標準實作，但 [支援多個選擇器](enabling-json-exporter.md#multiple-selectors) , `model` 但必須是第一個。

### 更多資訊 {#further-information}

另請參閱:

* Assets HTTP API
   * [Assets HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling Models:
   * [Sling Models —— 將模型類別與自130以來的資源類型關聯](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM with JSON:
   * [為元件啟用JSON匯出](enabling-json-exporter.md)

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱：

* [資產使用指南中的內容片段](/help/assets/content-fragments/content-fragments.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段製作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 和內容 [片段元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

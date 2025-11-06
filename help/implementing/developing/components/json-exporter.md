---
title: 內容服務的 JSON 匯出工具
description: AEM Content Services的設計目的，是要概括AEM內/外部內容的說明和傳遞，而不只是關注網頁。 這些頻道使用任何使用者端都能使用的標準化方法，將內容傳送至非傳統AEM網頁的管道。
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 9%

---

# 內容服務的 JSON 匯出工具 {#json-exporter-for-content-services}

AEM Content Services的設計目的，是要概括AEM內/外部內容的說明與傳送，而不只是網頁的焦點。

這些頻道使用任何使用者端都能使用的標準化方法，將內容傳送至非傳統AEM網頁的管道。 這些管道可能包括：

* 單頁應用程式
* 原生行動應用程式
* AEM外部的其他管道和接觸點

使用結構化內容的內容片段中，您可以使用JSON匯出工具來傳送JSON資料模型格式的AEM頁面內容，進而提供內容服務。 然後，您自己的應用程式便可使用它。

## 包含內容片段核心元件的JSON匯出工具 {#json-exporter-with-content-fragment-core-components}

您可以使用AEM JSON匯出工具，以JSON資料模型格式傳送AEM頁面的內容。 然後，您自己的應用程式便可使用它。

在AEM中，傳遞是使用選擇器`model`和`.json`副檔名達成。

`.model.json`

1. 例如，URL，例如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. 將傳送下列內容：

   WKND內容的![JSON模型](assets/json-model-wknd.png)

或者，您可以特別鎖定結構化內容片段的目標，以傳遞其內容。

這是使用片段的整個路徑完成的（透過`jcr:content`）；例如，尾碼為。

`.../jcr:content/root/container/container/contentfragment.model.json`

您的頁面可包含單一內容片段或多個各種型別的元件。 您也可以使用清單元件等機制，自動搜尋相關內容。

* 例如，URL，例如：

  ```shell
  http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
  ```

* 將傳送下列內容：

  WKND內容片段的![JSON模型](assets/json-model-wknd-content-fragment.png)

  >[!NOTE]
  >
  >您可以[調整您自己的元件](enabling-json-exporter.md)以存取及使用此資料。

  >[!NOTE]
  >
  >雖然不是標準實作，但支援[多個選取器](enabling-json-exporter.md#multiple-selectors)，但`model`必須是第一個。

### 更多資訊 {#further-information}

* Assets HTTP API
   * [Assets HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling模型：
   * [Sling模型 — 自130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)起將模型類別與資源型別建立關聯
* AEM與JSON：
   * [為元件啟用 JSON 匯出](enabling-json-exporter.md)

## 相關檔案 {#related-documentation}

* [內容片段](/help/sites-cloud/administering/content-fragments/overview.md)
* [內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [使用內容片段製作](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)和[內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

---
title: 元件主控台
description: 「元件控制台」允許您瀏覽為實例定義的所有元件
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 18%

---


# 元件主控台 {#components-console}

「元件控制台」允許您瀏覽為實例定義的所有元件，並查看每個元件的關鍵資訊。

您可從「工具」->「一 **般」->「元件」** 存取它 ********。由於沒有元件的樹結構，因此只有清單視圖可用。

![元件主控台](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>「元件控制台」顯示系統中的所有元件。 「元 [件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 」顯示作者可使用的元件，並隱藏以句點( `.`)開頭的元件群組。

## 搜尋 {#search-field}

使用「 **僅內容****** 」圖示 (左上角)，您可以開啟「搜尋」面板以搜尋和/或篩選元件：

![在元件控制台中搜索](/help/sites-cloud/authoring/assets/components-console-search.png)

### 元件詳細資訊 {#component-details}

要查看有關特定元件的詳細資訊，請點選／按一下所需資源。 三個標籤提供：

* **屬性**

   ![元件控制台屬性](/help/sites-cloud/authoring/assets/components-console-properties.png)

   在「屬性」標籤上，您可以：

   * 查看元件的常規屬性。
      * 查看如何為元件定義表徵圖或縮寫。 <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * 按一下圖示的來源後，您就會前往該元件。
   * 查看組 **件的資源類** 型 **和資源超級類型** （如果已定義）。
      * 按一下「資源超級類型」(Resource Super Type)將帶您進入該元件。

   >[!NOTE]
   >
   >由於 `/apps` 在執行時期無法編輯元件主控台，因此是唯讀的。

* **原則**

   ![元件控制台策略](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **即時使用情況**

   ![即時使用元件](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >由於為此視圖收集的資訊的性質，可能需要一段時間才能進行整理／顯示。

* **文件**

   如果開發人員已提供元件的檔案，則會顯示在「檔案」 **標籤** 。 如果沒有可用的文檔，則不 **會顯示** 「文檔」頁籤。 <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![元件檔案](/help/sites-cloud/authoring/assets/components-console-documentation.png)

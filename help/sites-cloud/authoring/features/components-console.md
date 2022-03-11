---
title: 元件主控台
description: 「元件控制台」允許您瀏覽為實例定義的所有元件
exl-id: f4949331-5302-46d3-a004-b813bb95ec2f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 18%

---

# 元件主控台 {#components-console}

「元件控制台」允許您瀏覽為實例定義的所有元件並查看每個元件的關鍵資訊。

您可從「工具」->「一 **般」->「元件」** 存取它 ********。由於沒有元件的樹結構，因此只有清單視圖可用。

![元件控制台](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>「元件控制台」顯示系統中的所有元件。 的 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 顯示可供作者使用的元件，並隱藏以句點開頭的任何元件組( `.`)。

## 搜尋 {#search-field}

使用「 **僅內容****** 」圖示 (左上角)，您可以開啟「搜尋」面板以搜尋和/或篩選元件：

![在元件控制台中搜索](/help/sites-cloud/authoring/assets/components-console-search.png)

### 元件詳細資訊 {#component-details}

要查看有關特定元件點擊/按一下所需資源的詳細資訊。 三個頁籤提供：

* **屬性**

   ![元件控制台屬性](/help/sites-cloud/authoring/assets/components-console-properties.png)

   在「屬性」頁籤上，您可以：

   * 查看元件的常規屬性。
      * 查看如何為元件定義表徵圖或縮寫。 <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * 按一下表徵圖的源將帶您進入該元件。
   * 查看 **資源類型** 和 **資源超級類型** （如果定義）。
      * 按一下「資源超級類型」(Resource Super Type)將帶您進入該元件。

   >[!NOTE]
   >
   >因為 `/apps` 運行時不可編輯，元件控制台為只讀。

* **原則**

   ![元件控制台策略](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **即時使用情況**

   ![元件的即時使用](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >由於為此視圖收集的資訊的性質，可能需要一段時間才能進行整理/顯示。

* **文件**

   如果開發人員已為元件提供文檔，則它將出現在 **文檔** 頁籤。 如果沒有可用的文檔， **文檔** 頁籤。 <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![元件文檔](/help/sites-cloud/authoring/assets/components-console-documentation.png)

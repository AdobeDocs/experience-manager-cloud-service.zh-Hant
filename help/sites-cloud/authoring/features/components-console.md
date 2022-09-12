---
title: 元件主控台
description: 元件控制台可讓您瀏覽為執行個體定義的所有元件
exl-id: f4949331-5302-46d3-a004-b813bb95ec2f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 18%

---

# 元件主控台 {#components-console}

元件控制台可讓您瀏覽為執行個體定義的所有元件，並檢視每個元件的金鑰資訊。

您可從「工具」->「一 **般」->「元件」** 存取它 ********。由於沒有元件的樹結構，因此只有清單視圖可用。

![元件主控台](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>元件控制台顯示系統中的所有元件。 此 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 顯示可供作者使用的元件，並隱藏以句點( `.`)。

## 搜尋 {#search-field}

使用「 **僅內容****** 」圖示 (左上角)，您可以開啟「搜尋」面板以搜尋和/或篩選元件：

![在元件控制台中搜索](/help/sites-cloud/authoring/assets/components-console-search.png)

### 元件詳細資訊 {#component-details}

若要檢視特定元件的詳細資訊，請點選/按一下所需資源。 提供三個標籤：

* **屬性**

   ![元件控制台屬性](/help/sites-cloud/authoring/assets/components-console-properties.png)

   在「屬性」索引標籤上，您可以：

   * 查看元件的常規屬性。
      * 檢視如何為元件定義圖示或縮寫。 <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * 按一下圖示的來源即會將您導向該元件。
   * 檢視 **資源類型** 和 **資源超類型** （若已定義）。
      * 按一下「資源超類型」(Resource Super Type)會將您導向該元件。

   >[!NOTE]
   >
   >因為 `/apps` 在運行時無法編輯，元件控制台是只讀的。

* **原則**

   ![元件控制台原則](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **即時使用情況**

   ![元件的即時使用](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >由於為此檢視收集的資訊性質的緣故，可能需要一段時間才能加以整理/顯示。

* **文件**

   如果開發人員已提供元件的檔案，則會顯示在 **檔案** 標籤。 如果沒有可用的檔案，則 **檔案** 標籤。 <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![元件檔案](/help/sites-cloud/authoring/assets/components-console-documentation.png)

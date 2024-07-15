---
title: 元件主控台
description: 元件主控台可讓您瀏覽針對執行個體定義的所有元件
exl-id: f4949331-5302-46d3-a004-b813bb95ec2f
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 14%

---

# 元件主控台 {#components-console}

「元件主控台」可讓您瀏覽針對執行個體定義的所有元件，並檢視每個元件的關鍵資訊。

您可以從&#x200B;**工具>** **一般>** **元件**&#x200B;存取它。 由於沒有元件的樹結構，因此只有清單視圖可用。

![元件主控台](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>「元件主控台」會顯示系統中的所有元件。 [元件瀏覽器](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)顯示作者可用的元件，並隱藏任何以句點( `.`)開頭的元件群組。

## 搜尋 {#search-field}

使用「 **僅內容****** 」圖示 (左上角)，您可以開啟「搜尋」面板以搜尋和/或篩選元件：

![在元件主控台中搜尋](/help/sites-cloud/authoring/assets/components-console-search.png)

### 元件詳細資料 {#component-details}

若要檢視特定元件的詳細資訊，請選取所需資源。 三個索引標籤提供：

* **屬性**

  ![元件主控台屬性](/help/sites-cloud/authoring/assets/components-console-properties.png)

  在「屬性」標籤上，您可以：

   * 檢視元件的一般屬性。
      * 檢視元件圖示或縮寫的定義方式。<!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * 按一下圖示的來源會前往該元件。
   * 檢視元件的&#x200B;**資源型別**&#x200B;和&#x200B;**資源超級型別** （如果已定義）。
      * 按一下「資源超級型別」即可前往該元件。

  >[!NOTE]
  >
  >由於`/apps`在執行階段無法編輯，元件主控台是唯讀的。

* **原則**

  ![元件主控台原則](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **即時使用情況**

  ![元件的即時使用情況](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

  >[!CAUTION]
  >
  >由於為此檢視收集之資訊的性質，它可能需要一段時間才能整理/顯示。

* **文件**

  如果開發人員已提供元件的檔案，它將出現在&#x200B;**檔案**&#x200B;索引標籤上。 如果沒有可用的檔案，將不會顯示&#x200B;**檔案**&#x200B;標籤。<!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

  ![元件檔案](/help/sites-cloud/authoring/assets/components-console-documentation.png)

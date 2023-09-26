---
title: 元件概觀
description: 元件是模組化單元，可實現特定功能以在您的網站上展示您的內容
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 67%

---

# 元件概觀 {#components-overview}

此頁面概述了 Adobe Experience Manager (AEM) 元件，例如那些[用於頁面編寫](/help/sites-cloud/authoring/fundamentals/components.md) 的元件。

## 元件有哪些？ {#what-are-components}

* 一種模組化單元，可實現特定功能以在您的網站上展示您的內容。
* 可重複使用。
* 在存放庫的一個資料夾中開發為獨立單元。
* 沒有隱藏的設定檔案。
* 它們可以包含其他元件。
* 它們可以在任何AEM系統中的任何地方執行，並且也可以限製為在特定元件下執行。
* 具有標準化的使用者介面。
* 具有可以設定的編輯行為。
* 使用根據Granite UI元件的子元素建置的對話方塊。
* 開發環境使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html).
* 您可以開發這些元件，以建立可延伸預設功能的自訂元件。

因為元件是模組化的，所以您可以：

* 在您的本機執行個體上開發新元件。
* 將其部署到測試環境。
* 將其部署到即時編寫環境，作者和/或管理員可以在其中新增和設定內容。
* 將其部署到您的即時發佈環境，在那裡，它們用於呈現網站訪客的內容。

每個 AEM 元件：

* 是資源類型。
* 是完整實現特定功能的指令碼集合。
* 可以獨立運作，代表可以在 AEM 或入口網站中運作。

## AEM 核心元件 {#aem-core-components}

[AEM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 是適用於AEM的一組標準化網頁內容管理(WCM)元件，可加快開發時間並降低網站的維護成本。

核心元件隨 AEM as a Cloud Service 一起提供，[WKND 教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 說明如何實作和使用元件。這些元件隨附所有原始程式碼，可以按原狀使用，也可以做為修改或擴充元件的起點。

### 檢視可用元件 {#viewing-available-components}

如需AEM執行個體中所有可用元件的總覽，請使用 [元件主控台](/help/sites-cloud/authoring/features/components-console.md).

或者，您也可以使用 CRXDE Lite 取得存放庫中所有可用元件的清單。

1. 在 **[!UICONTROL CRXDE Lite]** 中，從工具列中選擇&#x200B;**[!UICONTROL 工具]**，然後選擇&#x200B;**[!UICONTROL 查詢]**，**[!UICONTROL 查詢]**&#x200B;索引標籤會隨即開啟。

1. 在&#x200B;**[!UICONTROL 查詢]**&#x200B;索引標籤中，選擇 `XPath` 作為 **[!UICONTROL 類型]**。

1. 在 **[!UICONTROL 查詢]** 輸入欄位，輸入下列字串：

   `//element(*, cq:Component)`

1. 按一下&#x200B;**[!UICONTROL 執行]**，元件隨即列出。

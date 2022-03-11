---
title: 元件概述
description: 元件是模組化單元，可實現在網站上顯示內容的特定功能
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 3%

---

# 元件概述 {#components-overview}

本頁概述Adobe Experience Manager(AEM)元件，如 [用於頁面創作](/help/sites-cloud/authoring/fundamentals/components.md)。

## 什麼是元件？ {#what-are-components}

中的組AEM件包括：

* 模組化單元，可實現特定功能以在網站上顯示您的內容。
* 可重用。
* 開發為儲存庫的一個資料夾中的自含單元。
* 沒有隱藏的配置檔案。
* 可以包含其他元件。
* 可以在任何系統內AEM的任何位置運行，也可以限制在特定元件下運行。
* 擁有標準化的用戶介面。
* 具有可配置的編輯行為。
* 使用基於Granite UI元件使用子元素構建的對話框。
* 使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hant)。
* 可以開發為建立擴展預設功能的定製元件。

由於元件是模組化的，因此您可以：

* 在本地實例上開發新元件。
* 將其部署到您的test環境。
* 將其部署到您的即時創作環境，使作者和/或管理員能夠在該環境中添加和配置內容。
* 將其部署到您的即時發佈環境中，這些環境用於為網站訪問者呈現內容。

每個AEM元件：

* 是資源類型。
* 是完全實現特定功能的指令碼集合。
* 可以獨立運行，即在門AEM戶內或門戶內。

## AEM 核心元件 {#aem-core-components}

[核心AEM元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 是一組標準化的Web內容管理(WCM)元件，AEM用於加快開發時間並降低網站的維護成本。

核心元件配AEM有as a Cloud Service [WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 說明了如何實施和使用元件。 這些元件提供了所有原始碼，可以按原樣或作為修改的或擴展的元件的起點。

### 查看可用元件 {#viewing-available-components}

有關實例中所有可用元件的概AEM覽，請使用 [元件控制台](/help/sites-cloud/authoring/features/components-console.md)。

或者，您也可以使用CRXDE Lite獲取儲存庫中所有可用元件的清單。

1. 在 **[!UICONTROL CRXDE Lite]**&#x200B;選中 **[!UICONTROL 工具]** 的 **[!UICONTROL 查詢]**&#x200B;的子菜單。 **[!UICONTROL 查詢]** 頁籤。

1. 在 **[!UICONTROL 查詢]** 頁籤 `XPath` 如 **[!UICONTROL 類型]**。

1. 在 **[!UICONTROL 查詢]** 輸入欄位，輸入以下字串：

   `//element(*, cq:Component)`

1. 按一下 **[!UICONTROL 執行]** 並列出元件。

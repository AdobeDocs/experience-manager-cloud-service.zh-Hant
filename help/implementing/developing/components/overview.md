---
title: 元件概觀
description: 元件是可實現特定功能的模組，可在您的網站上呈現您的內容
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 4%

---


# 元件概述{#components-overview}

本頁概述Adobe Experience Manager(AEM)元件，例如用於製作頁面的[元件。](/help/sites-cloud/authoring/fundamentals/components.md)

## 什麼是元件？{#what-are-components}

AEM中的元件包括：

* 可實現特定功能的模組，以在您的網站上呈現您的內容。
* 可重複使用。
* 開發為儲存庫的一個資料夾中的自含單元。
* 沒有隱藏的配置檔案。
* 可包含其他元件。
* 可在任何AEM系統內的任何位置執行，也可限制在特定元件下執行。
* 擁有標準化的使用者介面。
* 具有可設定的編輯行為。
* 使用以Granite UI元件為基礎的子元素所建立的對話方塊。
* 使用[HTL](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html)開發。
* 可開發來建立可擴充預設功能的自訂元件。

由於元件是模組化的，因此您可以：

* 在您的本機執行個體上開發新元件。
* 將它部署至您的測試環境。
* 將它部署至您的即時製作環境，讓作者和／或管理員可在其中新增及設定內容。
* 將它部署至即時發佈環境，以便用來為網站的訪客呈現內容。

每個AEM元件：

* 是資源類型。
* 是完全實現特定功能的指令碼集合。
* 可單獨運作，亦即在AEM或入口網站中運作。

## AEM 核心元件 {#aem-core-components}

[AEM核心元](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 件是一套適用於AEM的標準化網頁內容管理(WCM)元件，可加速開發時間並降低網站的維護成本。

「核心元件」隨附AEM做為雲端服務，[WKND Tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md)說明如何實作和使用元件。 這些元件提供了所有原始碼，可以按原樣使用，或作為修改或擴展元件的起點。

### 查看可用元件{#viewing-available-components}

如需AEM例項中所有可用元件的概觀，請使用[元件主控台](/help/sites-cloud/authoring/features/components-console.md)。

或者，您也可以使用CRXDE Lite來獲取儲存庫中所有可用元件的清單。

1. 在&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;中，從工具列中選擇&#x200B;**[!UICONTROL 工具]**，然後選擇&#x200B;**[!UICONTROL 查詢]**，以開啟&#x200B;**[!UICONTROL 查詢]**&#x200B;頁籤。

1. 在&#x200B;**[!UICONTROL Query]**&#x200B;標籤中，選擇`XPath`作為&#x200B;**[!UICONTROL 類型]**。

1. 在&#x200B;**[!UICONTROL Query]**&#x200B;輸入欄位中，輸入下列字串：

   `//element(*, cq:Component)`

1. 按一下&#x200B;**[!UICONTROL 執行]**&#x200B;並列出元件。


---
title: 元件概觀
description: 元件是模組化單元，可實現特定功能，以在您的網站上呈現您的內容
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 3%

---

# 元件概述{#components-overview}

本頁概略介紹Adobe Experience Manager(AEM)元件，例如用於頁面編寫的[元件。](/help/sites-cloud/authoring/fundamentals/components.md)

## 什麼是元件？{#what-are-components}

AEM中的元件包括：

* 模組化單元，可實現在網站上呈現您內容的特定功能。
* 可重複使用。
* 開發為存放庫一個資料夾內的獨立單位。
* 沒有隱藏的配置檔案。
* 可包含其他元件。
* 可在任何AEM系統內的任何位置執行，也可限制在特定元件下執行。
* 有標準化的使用者介面。
* 具有可設定的編輯行為。
* 使用根據Granite UI元件使用子元素建置的對話方塊。
* 使用[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hant)開發。
* 可開發以建立可擴充預設功能的自訂元件。

由於元件是模組化的，因此您可以：

* 在本機執行個體上開發新元件。
* 將其部署至您的測試環境。
* 將其部署至您的即時製作環境，讓作者和/或管理員可在其中新增和設定內容。
* 將其部署至您的即時發佈環境，以便用於呈現網站訪客的內容。

每個AEM元件：

* 是資源類型。
* 是完全實現特定功能的指令碼集合。
* 可單獨運作，亦即在AEM或入口網站內。

## AEM 核心元件 {#aem-core-components}

[AEM核心元](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 件是一組適用於AEM的標準化網頁內容管理(WCM)元件，可縮短開發時間並降低網站的維護成本。

核心元件以AEM as aCloud Service的形式提供，而[WKND教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)說明如何實作和使用元件。 這些元件提供了所有原始碼，可以按原樣使用，也可以作為修改或擴展元件的起始點。

### 查看可用元件{#viewing-available-components}

如需AEM例項中所有可用元件的概觀，請使用[元件主控台](/help/sites-cloud/authoring/features/components-console.md)。

或者，您也可以使用CRXDE Lite來取得存放庫中所有可用元件的清單。

1. 在&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;中，從工具欄中選擇&#x200B;**[!UICONTROL 工具]**，然後選擇&#x200B;**[!UICONTROL 查詢]**，開啟&#x200B;**[!UICONTROL 查詢]**&#x200B;頁簽。

1. 在&#x200B;**[!UICONTROL Query]**&#x200B;標籤中，選擇`XPath`作為&#x200B;**[!UICONTROL Type]**。

1. 在&#x200B;**[!UICONTROL Query]**&#x200B;輸入欄位中，輸入以下字串：

   `//element(*, cq:Component)`

1. 按一下「**[!UICONTROL 執行]**」並列出元件。

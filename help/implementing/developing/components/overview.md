---
title: 元件概觀
description: 元件是模組化單元，可實現特定功能以在您的網站上展示您的內容
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 100%

---

# 元件概觀 {#components-overview}

此頁面概觀了 Adobe Experience Manager (AEM) 元件，例如那些[用於頁面編寫](/help/sites-cloud/authoring/page-editor/components.md) 的元件。

## 元件有哪些？ {#what-are-components}

* 模組化單元，可實現特定功能以在您的網站上展示您的內容。
* 可重複使用。
* 在存放庫的一個資料夾中開發為獨立單元。
* 沒有隱藏的設定檔案。
* 這些單位可以包含其他元件。
* 這些單位可以在任何 AEM 系統內的任何位置執行，也可以限制在特定元件下執行。
* 具有標準化的使用者介面。
* 具有可以設定的編輯行為。
* 使用以子元素根據 Granite UI 元件建置的對話框。
* 這些單位是使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=zh-Hant) 來開發。
* 這單位可以開發並建立擴充預設功能的自訂元件。

因為元件是模組化的，所以您可以：

* 在您的本機執行個體上開發新元件。
* 將其部署到測試環境。
* 將其部署到即時編寫環境，作者和/或管理員可以在其中新增和設定內容。
* 將其部署到即時發佈環境，在這類環境中會來為您的網站訪客呈現內容。

每個 AEM 元件：

* 是資源類型。
* 是完整實現特定功能的指令碼集合。
* 可以獨立運作，代表可以在 AEM 或入口網站中運作。

## AEM 核心元件 {#aem-core-components}

[AEM 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 是一組適用於 AEM 的標準化網站內容管理 (WCM) 元件，可加快開發時間並降低網站的維護成本。

核心元件隨 AEM as a Cloud Service 一起提供，[WKND 教學課程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)說明如何實作和使用元件。這些元件隨附所有原始程式碼，可以按原狀使用，也可以做為修改或擴充元件的起點。

### 檢視可用元件 {#viewing-available-components}

如需 AEM 執行個體中所有可用元件的概觀，請使用[元件主控台](/help/sites-cloud/authoring/components-console.md)。

或者，您也可以使用 CRXDE Lite 取得存放庫中所有可用元件的清單。

1. 在 **[!UICONTROL CRXDE Lite]** 中，從工具列中選擇&#x200B;**[!UICONTROL 工具]**，然後選擇&#x200B;**[!UICONTROL 查詢]**，**[!UICONTROL 查詢]**&#x200B;索引標籤會隨即開啟。

1. 在&#x200B;**[!UICONTROL 查詢]**&#x200B;索引標籤中，選擇 `XPath` 作為 **[!UICONTROL 類型]**。

1. 在&#x200B;**[!UICONTROL 查詢]**&#x200B;輸入欄位，輸入以下字串：

   `//element(*, cq:Component)`

1. 按一下&#x200B;**[!UICONTROL 執行]**，元件隨即列出。

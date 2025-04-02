---
title: Adobe Experience Manager as a Cloud Service的微前端內容片段選擇器
description: 使用微前端內容片段選擇器來搜尋、尋找及擷取您應用程式的內容片段。
role: Admin, User
source-git-commit: 32e1b3cef768b420f32b70202ddadc80db2b74e8
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 11%

---


# 微前端內容片段選擇器 {#micro-frontend-content-fragment-selector}

微前端內容片段選擇器提供的使用者介面可輕鬆與Adobe Experience Manager (AEM) as a Cloud Service存放庫整合。 介面可讓您瀏覽或搜尋存放庫中的內容片段，並在您的應用程式中使用它們。

使用內容片段選擇器套件的應用程式提供Micro-Frontend使用者介面。 套件的任何更新都會自動匯入並載入您的應用程式中。

![微前端內容片段選擇器 — 概觀](/help/headless/assets/content-fragment-selector-overview.png)

內容片段選擇器具備許多優點，例如：

* 輕鬆與任何Adobe應用程式整合。
* 易於維護，因為內容片段選擇器套件的更新會自動部署至您的應用程式可用的內容片段選擇器。 這表示您的應用程式不需要採取動作來載入最新修改。
* 使用可控制應用程式內顯示內容片段選擇器的屬性，輕鬆自訂。
* 全文檢索搜尋加上可自訂的篩選器，可讓內容片段在製作體驗中快速導覽。
* 能夠切換IMS組織內的存放庫以進行內容片段選擇。
* 排序內容片段，並在您選取的檢視中檢視這些片段的功能。

## 先決條件 {#prerequisites}

### IMS驗證 {#ims-authentication}

如果您需要IMS驗證工作流程，您必須確保：

* 應用程式正在`HTTPS`上執行。
* 應用程式的URL在IMS使用者端允許的重新導向URL清單中。
* IMS 登入流程是使用網頁瀏覽器上的快顯視窗進行設定和轉譯。因此，應在目標瀏覽器上啟用或允許快顯視窗。

或者，如果您的應用程式已通過IMS工作流程驗證，您可以改為新增適當的IMS資訊。

## 安裝 {#installation}

使用`ContentFragmentSelector`元件。 有幾個安裝選項：

1. NPM登入(私人Adobe登入)

   * 將下列專案新增至`.npmrc`：

     ```html
     @aem-sites:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-aem-sites-release/
     ```

   * 然後安裝

     ```html
     npm install @aem-sites/content-fragment-selector
     ```

1. Git 存放庫

   * 將下列專案新增至`package.json`相依性：

     ```html
     "@aem-sites/content-fragment-selector": "git+https://github.com/adobe/<your-private-repo-url>.git#version"
     ```

## 使用內容片段選擇器 {#using-the-Content-Fragment-selector}

設定內容片段選擇器並驗證為可搭配您的AEM as a Cloud Service應用程式使用內容片段選擇器後，您可以選取內容片段或執行各種其他操作，以在存放庫中搜尋您的片段：

![內容片段選擇器](/help/headless/assets/content-fragment-selector-using.png)

* 透過右上角的&#x200B;**存放庫**&#x200B;選擇器，您可以選取要使用的存放庫
* 在最左側的面板中，您可以：
   * 從選取的存放庫隱藏或顯示資料夾
   * 選取特定資料夾以顯示該資料夾中的內容片段
* 在主面板中，您可以：
   * 選取內容片段
   * 搜尋內容片段
   * 根據不同的欄排序目前的清單；升序或降序
   * 檢視檢視格式指示器
   * 顯示、隱藏和指定篩選器

### 隱藏/顯示面板 {#hide-show-panel}

若要將資料夾隱藏在左側導覽中，請按一下&#x200B;**隱藏資料夾**&#x200B;圖示。要還原變更，請再按一下&#x200B;**隱藏資料夾**&#x200B;圖示。

### 存放庫切換器 {#repository-switcher}

內容片段選擇器可讓您選取要選取片段的存放庫。

您可以從位於主面板頂端的&#x200B;**存放庫**&#x200B;下拉式清單中選取您選擇的存放庫。

![內容片段選擇器](/help/headless/assets/content-fragment-repository-selector.png)

下拉清單中可用的存放庫選項是根據`repositoryId``index.html`檔案中定義的屬性。此屬性以目前登入之使用者存取之所選IMS組織的環境為基礎。

消費者可以傳遞偏好的`repositoryID`以從特定存放庫轉譯片段，並停止轉譯存放庫切換器。

### 內容片段資料夾 {#content-fragments-folders}

內容片段存放庫是內容片段資料夾的集合，可用來執行操作。

### 篩選條件 {#filters}

內容片段選擇器也提供立即可用的篩選選項，來縮小您的搜尋結果。 有多種篩選器可供使用，包括：

* **片段模型**
* **本地化**
* **狀態**：片段的目前狀態；`New`、`Draft`、`Published`、`Modified`、`Unpublished`
* 標記
* 使用者
* 時間和日期

![篩選器選項](/help/headless/assets/content-selector-filters.png)

您也可以建立預設的搜尋篩選器，以儲存以供日後使用。 若要為內容片段建立自訂搜尋篩選器，您可以使用`filterSchema`屬性。

### 搜尋列 {#search-bar}

內容片段選擇器可讓您在選取的存放庫中執行片段的全文搜尋。 例如，如果您在搜尋列中鍵入關鍵字`wave`，則會顯示任何中繼資料屬性中提及的所有含有`wave`關鍵字的片段。

### 排序 {#sorting}

您可以在「內容片段選擇器」中依各種屬性排序片段。 您也可以依遞增或遞減順序排序片段。

### 視圖類型 {#view-type}

內容片段選擇器可讓您在中檢視片段：

* **資料表檢視**

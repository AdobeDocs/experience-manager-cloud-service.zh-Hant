---
title: 開發人員模式
seo-title: Developer Mode
description: 開發人員模式會開啟側面板，其中包含數個標籤，為開發人員提供目前頁面的相關資訊
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
source-git-commit: b80aaa799e1652f7a981006925b50ffef43d7ab3
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# 開發人員模式 {#developer-mode}

在AEM中編輯頁面時，有數個[模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)可供使用，包括開發人員模式。 開發人員模式會開啟側面板，其中包含數個標籤，為開發人員提供目前頁面的技術資訊。

有兩個標籤：

* **[](#components)** 檢視結構和效能資訊的元件。
* **[](#errors)** 錯誤，無法查看發生的任何問題。

這些功能可協助開發人員：

* **** 探索頁面的撰寫方式。
* **除錯：** 發生在何處和何時，進而有助於解決問題。

>[!NOTE]
>
>開發人員模式：
>
>* 在行動裝置上或案頭上的小視窗上皆無法使用（因空間限制）。
>  * 當寬度小於1024px時即會發生此情況。
>* 僅對`administrators`組成員的用戶可用。


## 開啟開發人員模式 {#opening-developer-mode}

開發人員模式是作為側面板實作到頁面編輯器。 若要開啟面板，請從頁面編輯器工具列的模式選取器中選取&#x200B;**開發人員**:

![開啟開發人員模式](assets/developer-mode.png)

面板分為兩個標籤：

* **[元件](#components)**  — 這會顯示與作者內容樹狀結構 [類](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree) 似的元件樹
* **[錯誤](#errors)**  — 發生問題時，會顯示每個元件的詳細資訊。

### 元件標籤 {#components}

![元件索引標籤](assets/developer-mode-components-tab.png)

這會顯示元件樹，其中包含：

* 概述在頁面上呈現的元件和模板鏈。 樹可以展開，以顯示階層內的內容。
* 顯示轉譯元件所需的伺服器端計算時間。
* 允許您展開樹並在樹中選擇特定元件。 「選擇」提供對元件詳細資訊的訪問；例如：
   * 儲存庫路徑
   * 指令碼連結(以CRXDE Lite存取)
   * [元件控制台](/help/sites-cloud/authoring/features/components-console.md)中顯示的元件詳細資訊
* 樹中選取的元件在編輯器中以藍色邊框表示。

此元件標籤有助於：

* 決定並比較每個元件的轉譯時間。
* 請參閱並了解階層。
* 了解並改善頁面載入時間，方法是尋找緩慢的元件。

每個元件項目可能具有下列選項：

![開發人員模式元件範例](assets/developer-mode-component-example.png)

* **檢視詳細資料：** 顯示下列內容的清單連結：
   * 用於呈現元件的所有元件指令碼。
   * 此特定元件的儲存庫內容路徑。

      ![檢視詳情](assets/developer-mode-view-details.png)

* **編輯指令碼：** 在CRXDE Lite中開啟元件指令碼的連結。

* **檢視元件詳細資料：** 在元件控制台中開啟元件的 [詳細資料。](/help/sites-cloud/authoring/features/components-console.md)

點選或按一下>形箭號以展開元件項目，也可顯示：

    *所選元件內的階層。
    *單獨呈現所選元件、其內嵌的任何個別元件，以及合併總計的呈現時間。

### 「錯誤」頁簽 {#errors}

![錯誤索引標籤](assets/developer-mode-errors-tab.png)

希望&#x200B;**Errors**&#x200B;標籤始終為空（如上所示），但當出現問題時，可能會為每個元件顯示以下詳細資訊：

* 如果元件將項目寫入錯誤記錄，以及錯誤的詳細資訊，並將連結導向CRXDE Lite內的適當程式碼，則會發出警告。
* 元件開啟管理工作階段時出現警告。

例如，如果調用未定義的方法，則產生的錯誤將顯示在&#x200B;**Errors**&#x200B;頁簽中，而當發生錯誤時，**Components**&#x200B;頁簽樹中的元件條目也將標籤為指示符。

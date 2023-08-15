---
title: 開發人員模式
seo-title: Developer Mode
description: 開發人員模式會開啟一個側面板，其中包含數個標籤，為開發人員提供目前頁面的相關資訊
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
exl-id: fbf11c0f-dc6e-43f3-bcf2-080eacc6ba99
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 1%

---

# 開發人員模式 {#developer-mode}

在AEM中編輯頁面時，有數個 [模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) 都可使用，包括開發人員模式。 開發人員模式會開啟一個側面板，其中包含數個標籤，為開發人員提供有關目前頁面的技術資訊。

有兩個標籤：

* **[元件](#components)** 以檢視結構和效能資訊。
* **[錯誤](#errors)** 檢視發生的任何問題。

這些功能可協助開發人員：

* **探索** 頁面的構成方式。
* **偵錯：** 隨時隨地發生的狀況，進而協助解決問題。

>[!NOTE]
>
>開發人員模式:
>
>* 在行動裝置或桌上型電腦的小型視窗上無法使用（由於空間限制）。
>  * 當寬度小於1024畫素時，就會發生這種情況。
>* 僅適用於屬於下列成員的使用者： `administrators` 群組。

## 開啟開發人員模式 {#opening-developer-mode}

開發人員模式會實作為頁面編輯器的側面板。 若要開啟面板，請選取 **開發人員** 從頁面編輯器工具列的模式選取器：

![正在開啟開發人員模式](assets/developer-mode.png)

面板分為兩個標籤：

* **[元件](#components)**  — 這個選項會顯示元件樹，類似於 [內容樹狀結構](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree) 作者
* **[錯誤](#errors)**  — 發生問題時，會顯示每個元件的詳細資料。

### 元件標籤 {#components}

![元件標籤](assets/developer-mode-components-tab.png)

這會顯示符合下列條件的元件樹狀結構：

* 概述頁面上呈現的元件鏈和範本。 可展開樹狀結構以顯示階層內的前後關聯。
* 顯示呈現元件所需的伺服器端運算時間。
* 可讓您展開樹狀結構並選取樹狀結構中的特定元件。 選取範圍提供元件詳細資料的存取權，例如：
   * 存放庫路徑
   * 指令碼連結(在CRXDE Lite中存取)
   * 元件詳細資訊，如 [元件主控台](/help/sites-cloud/authoring/features/components-console.md)
* 在編輯器中選取的元件會以藍色邊框表示。

此元件標籤有助於：

* 決定並比較每個元件的演算時間。
* 檢視並瞭解階層。
* 找出緩慢的元件，瞭解並改善頁面載入時間。

每個元件專案都可能有以下選項：

![開發人員模式元件範例](assets/developer-mode-component-example.png)

* **檢視詳細資料：** 清單的連結，其中顯示：
   * 用於呈現元件的所有元件指令碼。
   * 此特定元件的存放庫內容路徑。

     ![檢視詳情](assets/developer-mode-view-details.png)

* **編輯指令碼：** 以CRXDE Lite開啟元件指令碼的連結。

* **檢視元件詳細資訊：** 在中開啟元件的詳細資訊。 [元件主控台](/help/sites-cloud/authoring/features/components-console.md).

點選或按一下>形箭號來展開元件專案也可顯示：

    *所選元件內的階層。
    *所選取元件的單獨呈現時間、巢狀內嵌的任何個別元件，以及合併總數。

### 錯誤標籤 {#errors}

![錯誤標籤](assets/developer-mode-errors-tab.png)

希望 **錯誤** 標籤一律空白（如上所述），但發生問題時，可能會顯示每個元件的下列詳細資料：

* 如果元件將專案寫入錯誤記錄檔，連同錯誤的詳細資訊以及指向CRXDE Lite內適當程式碼的直接連結，會出現警告。
* 如果元件開啟管理員工作階段，會出現警告。

例如，如果呼叫未定義的方法，則產生的錯誤會顯示在 **錯誤** 標籤與的樹狀結構中的元件專案 **元件** 索引標籤也會在錯誤發生時標示為指示器。

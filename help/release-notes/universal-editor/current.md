---
title: 通用編輯器 2024.12.02 發行說明
description: 這是通用編輯器 2024.12.02 版本的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 2aae8c63358680758e4f5324f38dea1bc2c47155
workflow-type: ht
source-wordcount: '300'
ht-degree: 100%

---


# 通用編輯器 2024.12.02 發行說明 {#release-notes}

這是通用編輯器 2024 年 12 月 2 日版本的發行說明。

>[!TIP]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **內容樹的鍵盤導覽**：位於側面板的[內容樹](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)現在可以完全透過鍵盤存取。
   * 作者可以使用標準鍵盤控制來導覽樹狀檢視項目及進行互動，符合 [WCAG 2.1 準則](/help/sites-cloud/authoring/page-editor/accessible-content.md)的無障礙標準。
   * 此增強功能確保樹狀結構中所有互動式元素均能透過鍵盤操作，藉此提高包容性，方便依賴鍵盤進行瀏覽的使用者。
* **取消選取可編輯元素**：作者現在可以取消選取頁面上先前選取的可編輯元素。
   * 當作者想要檢視頁面但不想看到使用中的選取邊框時，這項功能可以消除相關干擾。
* **片段選擇器**：在 AEM as a Cloud Service 執行個體上，片段參考現在開啟片段選擇器作為內容選擇器，能提供更好的功能，例如遵守允許的內容片段模型、搜尋內容片段，以及提升整體體驗。
   * 這與其他 Adobe 使用者介面保持一致並增強一致性。
   * [AEM 6.5 環境](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)仍繼續使用現有的內容選取器。
* **容器說明**：[屬性面板](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-panel-properties-rail)中用於參考內容的[容器元件](/help/implementing/universal-editor/field-types.md#container)，現在支援說明屬性，顯示於容器欄位上方。
   * 此新增功能為作者提供其正在編輯的分組欄位的背景資訊，讓相關內容更加清楚。

## 其他改良功能 {#other-improvements}

* **RTF 文字欄位同步**：屬性面板中 RTF 文字欄位內原始內容和呈現內容的同步有所改善，解決了 Edge Delivery Services 專案中 RTF 文字內容與呈現之表示方式有所不同的問題。
* **編輯模式事件**：通用編輯器現在能夠可靠地發出編輯模式事件，包括在重新載入遠端應用程式之後。

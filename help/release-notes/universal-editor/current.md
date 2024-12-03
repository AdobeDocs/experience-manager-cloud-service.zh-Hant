---
title: 通用編輯器 2024.12.02 發行說明
description: 此為通用編輯器 2024.12.02 版本的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 2aae8c63358680758e4f5324f38dea1bc2c47155
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 16%

---


# 通用編輯器 2024.12.02 發行說明 {#release-notes}

這些是2024年12月2日發行的Universal Editor的發行說明。

>[!TIP]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **內容樹狀結構的鍵盤導覽**： [可在側面板中使用的內容樹狀結構](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)，現在可透過鍵盤完整存取。
   * 作者可以使用標準鍵盤控制項，依循[WCAG 2.1指南](/help/sites-cloud/authoring/page-editor/accessible-content.md)的協助工具，導覽及互動樹狀檢視專案。
   * 此增強功能可確保樹狀結構中的所有互動式元素都可使用鍵盤操作，提高依賴鍵盤導覽的使用者的包容性。
* **取消選取可編輯專案**：作者現在可以取消選取頁面上先前選取的可編輯專案。
   * 當作者想要檢視沒有使用中選取範圍框線的頁面時，這可以消除干擾。
* **片段選擇器**：在AEM as a Cloud Service執行個體上，片段參考現在會開啟片段選擇器做為內容選擇器，提供改良的功能，例如遵循允許的內容片段模式、搜尋內容片段，以及改良的整體體驗。
   * 如此可與其他AdobeUI保持一致，並增強一致性。
   * [若是AEM 6.5環境，](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)現有的內容選擇器仍在使用中。
* **容器描述**： [在[屬性面板](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-panel-properties-rail)中用於參考內容的容器元件](/help/implementing/universal-editor/field-types.md#container)現在支援顯示在容器欄位上方的描述屬性。
   * 這項新增功能透過為作者提供他們正在編輯的群組欄位相關情境，強化了清晰度。

## 其他改良功能 {#other-improvements}

* **RTF欄位同步**：已改善屬性面板中RTF欄位內原始和演算內容的同步，解決RTF內容和演算後的表示方式可能不同的Edge Delivery Services專案問題。
* **編輯模式事件**：通用編輯器現在會可靠地發出編輯模式事件，包括在重新載入遠端應用程式之後。

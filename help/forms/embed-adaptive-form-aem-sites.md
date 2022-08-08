---
title: 在AEM Sites頁中嵌入自適應表單
seo-title: Hwo to add an Adaptive Form to an AEM Sites page?
description: 您可以使用AEM Forms集裝箱元件將自適應Forms添加到AEM Sites頁面，或將其嵌入到頁面中，以填寫和提交表單，而不需要離開AEM Sites頁面。
feature: Adaptive Forms
source-git-commit: dac38b2a90b2a1969e5332b8a658e8f1e0e5eccb
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---

# 將自適應表單嵌AEM入站點頁 {#embed-an-adaptive-form-to-aem-sites-page}

## 概觀 {#overview}

AEM Forms允許表單開發者將自適應表單無縫地嵌入到AEM Sites頁面或外部托管的網AEM頁中。 嵌入式自適應表單功能齊全，用戶無需離開頁面即可填寫和提交表單。 它幫助用戶保持在網頁上其他元素的上下文中並同時與表單交互。

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

在「AEM Sites」頁中，可以使用：

* **[AEM Forms集裝箱元件](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms提供了可添加到網站頁面的元件。 AEM Forms容器元件允許您嵌入自適應表單。

* **[資產瀏覽器](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
所有表單都可在「資產」下找到。 您可以將表單作為資產拖放到頁面上。

## 必備條件 {#prerequisites}

要在使用可編輯模板的AEM Sites頁中嵌入自適應表單，請確保AEM將Form元件配置為關聯模板中允許的元件。 有關詳細資訊，請參見 **策略和屬性（佈局容器）** 部分 [建立頁面模板](/help/sites-authoring/templates.md)。

如果「站點」頁使用靜態模板，則需要在站點頁的段落系統中配置它。 請參閱 [在設計模式下配置元件](/help/sites-authoring/default-components-designmode.md) 的子菜單。

## 嵌入自適應表單 {#af-component}

要使用AEM Forms容器元件嵌入自適應表單：

1. 在編AEM輯模式下開啟要嵌入自適應表單的站點頁。
1. 在「元件」瀏覽器面板中，拖放頁面上的「AEM Forms容器」元件。 或者，可以在「資產」瀏覽器中搜索「自適應表單」並將其拖放到「站點」頁。 它把形狀嵌在AEM Forms集裝箱裡。 可以建立和添加新的自適應表單或嵌入現有自適應表單。

   >[!NOTE]
   >
   >不支援頁面上的多個AEM Forms容器元件。

1. 要建立和嵌入新表單，請在元件工具欄上按一下 **建立窗體** 表徵圖 將開啟一個用於建立新窗體的窗口。

1. 在站點頁面中按一下嵌入的AEM Forms集裝箱元件，然後按一下 ![設定表徵圖](assets/settings_icon.png) 按鈕。 的 **[!UICONTROL 編輯AEM Forms容器]** 對話框。
1. 在「編輯AEM Forms容器」對話框中，指定以下內容。

   <!-- * **Asset Type:** Select the type of asset to embed. The options are Adaptive Form -->
   * **資產路徑**:瀏覽並選擇要嵌入的自適應表單。 如果從「資產」瀏覽器中刪除它，則會自動填充它。
   * **提交後** :選擇要在表單提交時觸發的操作。 您可以選擇顯示感謝信或感謝頁。

      * **謝謝留言**:使用富格文本編輯器編寫消息，以便在提交表單時顯示。 此選項僅在您選擇顯示感謝信時可用。
      * **謝謝頁**:瀏覽並選擇要在表單提交時顯示的頁面。 此選項僅在您選擇顯示感謝頁時可用。
         * **重定向至「感謝」頁**:啟用此選項可將包含嵌入式自適應表單的頁面替換為感謝頁。 否則，「感謝」頁面將替換AEM Forms容器中的「自適應表單」，而不刷新頁面的底層站點。 此選項僅在您選擇顯示感謝頁時可用。
   * **使用頁面語言**:使用AEM Sites頁的本地語言環境，而不是自適應窗體。
   * **將焦點設定在窗體上**:選擇以在「自適應表單」的第一個欄位上設定焦點。

   * **主題**:選擇一個主題，該主題為「自適應表單」的元件定義樣式。 樣式包括外觀屬性，如字型樣式、背景顏色、尺寸和對齊方式。
   * **高度**:指定容器的高度。 將其留空，以自動調整容器大小。
   * **CSS客戶端庫**:指定CSS客戶端庫的路徑。

1. 保存設定。 「自適應表單」現在嵌入到頁面中。

## 發佈嵌入式自適應表單 {#publishing-embedded-adaptive-form}

讓我們考慮在站點頁面中發佈嵌入式自適應表單AEM的以下情形：

* 如果您是首次發AEM布站點頁面，並且它包含嵌入式自適應表單，則發佈站點頁面和嵌入式資產。
* 如果僅修改了已發佈網站頁中的嵌入自適應表單，則發佈原始資產，而更改將反映在已發佈網站頁中。 發佈的網站頁面包括對資產的引用，並且不需要重新發佈該頁面。
* 如果修改了網站頁和嵌入的自適應表單，請重新發佈網站頁和嵌入的資產。

## 修改嵌入的自適應表單  {#modifying-embedded-adaptive-form}

「站AEM點」頁維護對「AEM Forms容器」中「自適應表單」的引用。 因此，在原始自適應表單中配置的所有配置和屬性（如主題、樣式和提交操作）都將保留在嵌入式自適應表單中。

要修改嵌入式自適應表單的任何配置或屬性，請執行以下操作之一。

* 在相應編輯器中以自適應表單開啟原始表單並修改它們。
* 在編輯模式下從網站頁中按一下「Adaptive Form（自適應表單）」 ，然後按一下 **[!UICONTROL 在新窗口中編輯]**。 原始窗體在可修改的編輯模式下開啟。

>[!NOTE]
>
>在原始自適應表單中所做的更改會自動反映在嵌入表單中。 但是，重新發佈「自適應表單」或網站頁以反映已發佈頁面中的更改。

## 考慮事項和最佳做法 {#considerations-and-best-practices}

在站點頁面中嵌入自適應表單時，請牢記AEM以下幾點：

* 原始表單中的頁眉和頁腳不包括在嵌入表單中。
* 在表單門戶的「草稿」和「已提交」Forms頁籤中，支援並可看到嵌入表單的用戶草稿和提交。
* 原始表單上配置的提交操作將保留在嵌入表單中。
* 在原始表單上配置的體驗目標和A/Btest在嵌入式表單中不起作用。 但是，您可以使用站點頁面上的體驗目標根據用戶配置檔案顯示不同的表單。
* 如果您為原始表單配置了Adobe Analytics，則嵌入表單的分析資料將在Adobe Analytics捕獲。 但是，表單分析報表中不提供它。

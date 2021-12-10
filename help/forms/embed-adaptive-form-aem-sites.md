---
title: '如何將適用性表單內嵌至AEM網站頁面？ '
description: 您可以將適用性Forms嵌入AEM網站頁面。 使用者無需離開網站頁面即可填寫及提交表單。
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---


# 在AEM網站頁面中內嵌適用性表單 {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

[!DNL AEM Forms] 可讓表單開發人員將適用性Forms流暢內嵌於AEM Sites頁面或托管於AEM以外位置的網頁中。 內嵌的適用性表單功能齊全，使用者無需離開頁面即可填寫及提交表單。 可協助使用者停留在網頁上其他元素的內容中，並同時與表單互動。

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

在AEM Sites頁面中，您可以使用下列方式新增最適化表單：

* **[[!DNL AEM Forms] 容器元件](#af-component)**
   [!DNL AEM Forms] 提供可新增至網站頁面的元件。 此 [!DNL AEM Forms] 容器元件可讓您內嵌適用性表單。

* **[資產瀏覽器](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
您建立的所有表單都可在「資產」下取得。 您可以拖放表單為頁面上的資產。

## 必備條件 {#prerequisites}

若要在使用可編輯範本的AEM網站頁面中內嵌適用性表單，請確定AEM表單元件已在相關範本中設定為允許的元件。 如需詳細資訊，請參閱 **策略和屬性（佈局容器）** 區段 [建立頁面範本](/help/sites-authoring/templates.md).

若「網站」頁面使用靜態範本，則需在網站頁面的段落系統中進行設定。 請參閱 [在設計模式中配置元件](/help/sites-authoring/default-components-designmode.md) 以取得更多資訊。

## 內嵌最適化表單  {#af-component}

若要內嵌適用性表單，請使用 [!DNL AEM Forms] 容器元件：

1. 在編輯模式中，開啟您要內嵌適用性表單的AEM網站頁面。
1. 從「元件」瀏覽器面板，拖放 [!DNL AEM Forms] 頁面上的容器元件。

   或者，您也可以在「資產」瀏覽器中搜尋適用性表單，並將其拖放至「網站」頁面。 它將表單嵌入 [!DNL AEM Forms] 容器。

   >[!NOTE]
   >
   >多個 [!DNL AEM Forms] 不支援頁面上的容器元件。

1. 點選內嵌的 [!DNL AEM Forms] 網站頁面中的容器元件，然後點選 ![settings_icon](assets/settings_icon.png) 在動作列上。 此 **[!UICONTROL 編輯AEM Forms容器]** 對話框開啟。
1. 在編輯 [!DNL AEM Forms] 容器對話方塊，指定下列項目。

   * **資產類型：** 選取要內嵌的資產類型。 選項為適用性表單
   * **資產路徑**:瀏覽並選取要內嵌的適用性表單。 如果您從「資產」瀏覽器中拖放，則會自動填入。
   * （僅限適用性表單） **貼文提交**:選取要在表單提交時觸發的動作。 您可以選擇顯示感謝訊息或感謝頁面。

      * **感謝訊息**:使用RTF編輯器撰寫訊息，以在表單提交時顯示。 只有在您選擇顯示感謝訊息時，才可使用此選項。
      * **感謝頁面**:瀏覽並選取要在表單提交時顯示的頁面。 只有在您選擇顯示感謝頁面時，才可使用此選項。
      * **提交時重新整理頁面**:啟用以重新整理包含內嵌適用性表單的頁面，以顯示感謝頁面。 否則，感謝頁面會取代 [!DNL AEM Forms] 容器，而不重新整理頁面。 只有在您選擇顯示感謝頁面時，才可使用此選項。
   * **主題**:選取定義最適化表單元件樣式的主題。 樣式包括外觀屬性，如字型樣式、背景顏色、尺寸和對齊方式。
   * **高度**:指定容器的高度。 保留為空白以自動調整容器大小。
   * **CSS用戶端程式庫**:指定CSS用戶端程式庫的路徑。


1. 儲存設定。 適用性表單現已內嵌於頁面中。

## 發佈內嵌適用性表單 {#publishing-embedded-adaptive-form}

在AEM網站頁面中發佈內嵌資產（適用性表單）時，請考量下列案例：

* 如果您是首次發佈AEM網站頁面，且其中包含內嵌的最適化表單，請發佈網站頁面和內嵌資產。
* 如果您只修改了已發佈網站頁面中的內嵌適用性表單，請發佈原始資產，而變更會反映在已發佈的網站頁面中。 已發佈的網站頁面包含對資產的參考，不需要重新發佈頁面。
* 如果您修改了網站頁面和內嵌適用性表單，請重新發佈網站頁面和內嵌資產。

## 修改內嵌適用性表單 {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM網站頁面會維護 [!DNL AEM Forms] 容器。 因此，在原始適用性表單中設定的所有設定和屬性（例如主題、樣式和提交動作）都會保留在內嵌適用性表單中。

要修改嵌入式適用性表單的任何配置或屬性，請執行以下操作之一。

* 在個別編輯器的適用性Forms中開啟原始表單並加以修改。
* 以編輯模式從網站頁麵點選最適化表單，然後點選 **[!UICONTROL 在新視窗中編輯]**. 原始表單會以可修改的編輯模式開啟。

>[!NOTE]
>
>原始適用性表單中所做的變更會自動反映在內嵌表單中。 不過，重新發佈適用性表單或網站頁面，以反映已發佈頁面中的變更。

## 考量事項和最佳實務 {#considerations-and-best-practices}

將適用性Forms內嵌至AEM網站頁面時，請謹記以下幾點：

* 原始表單中的頁首和頁尾不包含在嵌入表單中。
* 支援使用者草稿和提交內嵌表單，且可顯示在表單入口網站的「草稿」和「已提交Forms」標籤中。
* 原始表單上配置的提交操作將保留在嵌入式表單中。
* 在原始表單上設定的體驗鎖定目標和A/B測試在內嵌表單中無法運作。 不過，您可以使用網站頁面上的體驗鎖定目標，根據使用者設定檔呈現不同的表單。
* 如果您已為原始表單設定Adobe Analytics，則內嵌表單的分析資料會在Adobe Analytics中擷取。 不過，表單分析報表中無法使用。


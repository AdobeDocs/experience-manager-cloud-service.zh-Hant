---
title: 回應式版面
description: AEM可讓您為頁面建立互動式版面
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 7%

---


# 回應式版面 {#responsive-layout}

AEM可讓您使用「版面容器」元件，為頁面建立互動式 **版面** 。

這提供了段落系統，可讓您將元件定位在回應式格線中。 此格線可根據裝置／視窗大小和格式重新排列版面。 此元件與「版面」模式搭配使 [**用&#x200B;**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)，可讓您根據裝置建立和編輯回應式版面。

版面容器：

* 提供水準對齊格線的功能，以及將元件並排放在格線中，並定義元件何時應收合／重排的功能。
* 使用預先定義的中斷點（例如手機、平板電腦等） 可讓您定義相關裝置／方向之內容所需行為。
   * 例如，您可以自訂元件大小，或在特定裝置上是否可檢視元件。
* 可以巢狀內嵌，以允許欄控制。

然後，使用者就可以看到如何使用模擬器來呈現特定裝置的內容。

AEM使用多種機制組合，為您的頁面實現互動式版面配置：

* [**Layout Container **](#adding-a-layout-container-and-its-content-edit-mode)（版面容器）元件

   此元件可在元件瀏 [覽器中使用](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) ，並提供格點段落系統，讓您在回應式格點中新增和定位元件。 您也可以將其設為頁面上的預設段落系統。

* [**版面模式&#x200B;**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)

   一旦版面容器放置在您的頁面上，您就可以使用「版面 **** 」模式，將內容定位在回應式格線中。

* [**模擬器&#x200B;**](#selecting-a-device-to-emulate)這可讓您建立和編輯互動式網站，透過互動方式調整元件大小，以根據裝置／視窗大小重新排列版面。 然後，使用者就可以看到如何使用模擬器呈現內容。

有了這些互動式格點機制，您可以：

* 使用中斷點可根據裝置寬度（與裝置類型和方向相關）定義不同的內容版面。
* 使用這些相同的中斷點和內容版面，以確保您的內容能回應案頭上瀏覽器視窗的大小。
* 使用水準對齊格線，讓您將元件置入格線中、視需要調整大小，並定義元件何時應收合／重排並排或上／下。
* 隱藏特定裝置版面的元件。
* 實現列控制。

依您的專案而定，「版面容器」可能會用作您頁面的預設段落系統，或是可透過元件瀏覽器（或兩者）新增至頁面的元件。

>[!TIP]
>
>Adobe提供 [](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) GitHub檔案，說明互動式版面的參考內容，並提供給前端開發人員，讓他們在AEM外使用AEM格線，例如為未來的AEM網站建立靜態HTML模型時。

>[!NOTE]
>
>通過模板上的配置啟用上述機制的使用。 如需詳細資訊，請參閱設定互動式版面。 <!-- Use of the above mechanisms is enabled by configuration on the template. See [Configuring Responsive Layout](/help/sites-administering/configuring-responsive-layout.md) for further information.-->

## 版面定義、裝置模擬和中斷點 {#layout-definitions-device-emulation-and-breakpoints}

當您建立網站內容時，您需要確定顯示的內容與用來檢視該內容的裝置相符。

AEM可讓您根據裝置寬度來定義版面：

* 模擬器可讓您在多種裝置上模擬這些版面。 除了設備類型外，「旋轉設備」( **Rotate device** )選項選擇的方向還會影響寬度更改時選擇的斷點。
* 中斷點是分隔版面定義的點。
   * 它們使用特定版面有效地定義任何裝置的最大寬度（以像素為單位）。
   * 中斷點通常對於選擇的設備有效，取決於其顯示的寬度。
   * 斷點的範圍會向左延伸，直到下一個斷點。
   * 您無法具體選擇斷點，選擇設備和方向將自動選擇適當的斷點。

設備 **Desktop**（沒有特定寬度）與預設斷點（即上一個配置斷點上的所有內容）相關。

>[!NOTE]
>
>您可以為每個裝置定義中斷點，但這會大幅增加版面定義與維護的工作量。

使用模擬器時，選擇特定設備進行模擬和佈局定義，並將突出顯示相關斷點。 您所做的任何佈局更改都將適用於應用斷點的其它設備，即位於活動斷點標籤左側但位於下一個斷點標籤之前的任何設備。

例如，當您選取裝置 **iPhone 6 Plus** （定義寬度為540像素）進行模擬和版面配置時，也會啟動中斷點 **Phone** （定義為768像素）。 您對 **iPhone 6** 進行的任何版面變更，都適用於 **Phones** 中斷點下的其他裝置，例如 **iPhone 5** （定義為320像素）。

![模擬器](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## 選擇要模擬的設備 {#selecting-a-device-to-emulate}

1. 開啟所需的頁面進行編輯。 例如：

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. 從頂端工 **具列中** ，選取「模擬器」圖示：

   ![模擬器按鈕](/help/sites-cloud/authoring/assets/emulator.png)

1. 將會開啟模擬器工具欄。

   ![模擬器工具列](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   模擬器工具列會顯示其他版面配置選項：

   * **旋轉裝置** -可讓您將裝置從垂直（縱向）方向旋轉至水準（橫向）方向，反之亦然。
![旋轉裝置橫向按鈕](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![旋轉裝置縱向按鈕](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)   **選擇設備** -定義要從清單中模擬的特定設備（有關詳細資訊，請參閱下一步）

   * ![選擇設備按鈕](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

   ![要選擇要模擬的特定設備，您可以：](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. 使用「選取裝置」圖示並從下拉式選取器中選取。

   * 點選／按一下模擬器工具列中的裝置指示燈。
   * ![選擇裝置下拉式清單](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

   ![選擇特定設備後，您可以：](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. 請參閱所選裝置的作用中標籤，例如 **iPad。**

   * 請參閱適當斷點的作用中標 [記](#layout-definitions-device-emulation-and-breakpoints) ，例如 **Tablet。**
   * 藍色虛線代表所 *選裝置* (此處為橫向 **iPhone 6 Plus** )的折線。
   * ![折疊](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)****

   折頁也可視為內容的分頁符號(不要與分 [界點](#layout-definitions-device-emulation-and-breakpoints))。 此為顯示方便的項目，讓使用者在捲動之前，先在裝置上看到哪些內容。

   * 如果要模擬的裝置的高度高於螢幕大小，則不會顯示折線。[](#layout-definitions-device-emulation-and-breakpoints)
   * 為方便作者，會顯示折頁，而不會顯示在發佈的頁面上。
   * 新增版面容器及其內容 (編輯模式) {#adding-a-layout-container-and-its-content-edit-mode}


## 版 **面容器** (Layout Container)是一種段落系統，可：

包含其他元件。****

* 定義版面。
* 回應變更。
* [!NOTE]

>如果尚未提供，則必 **須針對段落系統** /頁面明確啟動「版面容器」。 <!-- If not already available, the **Layout Container** must be explicitly [activated for a paragraph system/page](/help/sites-administering/configuring-responsive-layout.md).-->
>
>「配 **置容器** 」是元件瀏覽器中的標準 [元件](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。從這裡，您可以將其拖曳至頁面上的必要位置，之後您將看到「拖曳元件至此處 **** 」預留位置。

1. 然後，您可以新增元件至版面容器。 這些元件將包含實際內容：****[](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)****
1. ![版面容器](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

   在版面容器上選取和採取動作（編輯模式） {#selecting-and-taking-action-on-a-layout-container-edit-mode}](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## 和其他元件一樣，您可以選取版面容器，然後對（剪下、複製、刪除）執行動作(在「編輯」模式 **中** ):

[!CAUTION]**

>[!CAUTION]由於版面容器是段落系統，刪除元件會同時刪除版面格線和容器內所有元件（及其內容）。
>
>如果您滑鼠或點選格線預留位置，就會顯示動作選單。

1. ![新增至版面容器](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   您需要選擇「父 **項** 」選項。

   ![父按鈕](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   如果版面元件是巢狀的，選取「父 **項** 」選項會顯示下拉式選項，讓您選取巢狀版面容器或其父項。

1. 當您將滑鼠移至下拉式清單中的容器名稱上方時，其外框會顯示在頁面上。****

   最低的巢狀版面容器將以藍色列出。

   * 每個容器都會變淡藍色。
   * ![巢狀容器](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

   這會反白顯示整個格線及其內容。 將顯示操作工具欄，您可從中選擇操作，如「刪 **除」。**

1. 定義版面（版面模式） {#defining-layouts-layout-mode}**

## [!NOTE]

>您可以為每個斷點定義單獨的 [佈局](#layout-definitions-device-emulation-and-breakpoints) （由模擬設備類型和方向確定）。
>
>若要設定使用「版面容器」實作之回應式格線的版面，您必須使用「版面 **」模式** 。

**版面** (Layout)模式可透過兩種方式啟動。

使用工具列 [中的模式選單](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) ，然後選擇「 **版面模式」**

* 選取「 **版面** 」模式，就像切換至「編輯 **」模式或「** 定位 **** 」模式。
   * **配置模式** (Layout **mode)會維持持續性，而且您必須先透過模式選取器** 選取其他模式，才能離開「配置」模式。****
   * 編輯 [個別元件時。](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout)****
* 使用元件快 **速動作選單中的** 「版面」選項，即可切換至「版 **面** 」模式。
   * **在編輯元件時** ，版面模式會持續存在，而且一旦焦點變更至其他元件， **就會回復** 「編輯」模式。
   * **在版面模式下，您可以對網格執行各種操作：******

使用藍點調整內容元件的大小。 調整大小將始終靠齊網格。 調整背景格線大小時，會顯示以協助對齊：

* ![調整元件大小](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

   [!NOTE]](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

   >調整元件（例如影像）的大小時，比例和比 **率會維持** 不變。
   >
   >在內容元件上按一下／點選，工具列可讓您：****

* **上層** -可讓您選取整個版面配置容器元件，以對整體採取動作。
   * **浮動至新行** -元件將移至新行，取決於網格中的可用空間。
   * **隱藏元件** -元件將變成不可見（可從版面容器的工具列還原）。
   * ![隱藏元件](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

   在「 **版面** 」模式中，您可以點選／按一下「拖曳元件至 **此處** 」以選取整個元件。 這將顯示此模式的工具欄。

* 工具列會根據版面元件的狀態和所屬的元件而有不同的選項。 例如：********

   **Parent** —— 選擇父元件。

   * ![父按鈕](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

      **顯示隱藏元件** -顯示所有或個別元件。 數字表示目前有多少個隱藏元件。 計數器顯示隱藏的元件數。

   * ![顯示隱藏的元件按鈕](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

      **恢復斷點佈局** -恢復為預設佈局。 這表示不會強加自訂版面。

   * ![「恢復斷點佈局」按鈕](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

      **浮點到新行** -如果間距允許，將元件向上移動。

   * ![浮動至新行按鈕](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

      **Hide component** —— 隱藏當前元件。

   * ![隱藏元件按鈕](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)

      [!NOTE]](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)
   >[!NOTE]在上述範例中，浮點和隱藏動作是可用的，因為此「版面容器」是巢狀內嵌在父「版面容器」中。
   >
   >**取消隱藏元**&#x200B;件選取父元件，使用「顯示隱藏元件」( **Show hidden components** )選項顯示動作工具列。 在此示例中，隱藏了兩個元件。

   * ![取消隱藏元件](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)
選取「顯 **示隱藏的元件** 」(Show hidden components)選項，會以藍色顯示目前隱藏在原始位置的元件。

      ![「恢復全部」按鈕](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)
   選擇「 **全部還原** 」將取消隱藏所有隱藏的元件。

   ![Restore all button](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

   Selecting **Restore all** will unhide all hidden components.

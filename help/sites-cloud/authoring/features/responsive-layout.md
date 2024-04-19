---
title: 回應式版面
description: AEM可讓您實現頁面的回應式版面
exl-id: 87202742-5bed-4e87-a427-456a1a0e72cc
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 5%

---

# 回應式版面 {#responsive-layout}

AEM可讓您透過使用 **配置容器** 元件。

如此可提供段落系統，讓您在回應式格線內放置元件。 此格線可根據裝置/視窗大小和格式重新排列版面。 此元件需與 [**版面** 模式](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)，可讓您根據裝置建立及編輯回應式版面。

配置容器：

* 提供水準貼齊格點，以及可並排將元件置入格點，並定義它們何時應摺疊/重排。
* 使用預先定義的中斷點（例如，手機、平板電腦等），讓您為相關裝置/方向定義內容的必要行為。
   * 例如，您可以自訂元件大小，或是否在特定裝置上可看見元件。
* 可巢狀化以允許欄控制項。

之後，使用者可以使用模擬器檢視特定裝置內容的呈現方式。

AEM使用一組機製為頁面實現回應式佈局：

* [**配置容器**](#adding-a-layout-container-and-its-content-edit-mode) 元件

  此元件位於 [元件瀏覽器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 並提供格線段落系統，讓您在回應式格線內新增及放置元件。 它也可以設定為您的頁面上的預設段落系統。

* [**佈局模式**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)

  將版面容器放置到頁面上後，您就可以使用 **版面** 在回應式格線內放置內容的模式。

* [**模擬器**](#selecting-a-device-to-emulate)
這可讓您建立及編輯回應式網站，這些網站會透過以互動方式調整元件大小，根據裝置/視窗大小重新安排版面。 之後，使用者可以使用模擬器檢視內容的呈現方式。

利用這些回應式格點機制，您可以：

* 根據裝置寬度（與裝置型別和方向相關），使用中斷點來定義不同的內容配置。
* 使用這些相同的中斷點和內容版面配置來確保您的內容會回應案頭上瀏覽器視窗的大小。
* 使用水準靠齊格點，讓您可以在格點中放置元件、視需要調整大小，以及定義它們何時應該摺疊/重排成並排或上下對齊/重排。
* 隱藏特定裝置配置的元件。
* 實現欄控制。

根據您的專案，可能會將「版面容器」用作頁面的預設段落系統，或用作可透過元件瀏覽器新增至頁面的元件（或同時用作兩者）。

>[!TIP]
>
>Adobe提供 [GitHub檔案](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) 回應式版面作為參考，前端開發人員可以參考該參考，以便在AEM之外使用AEM格線，例如在為未來的AEM網站建立靜態HTML模型時。

>[!NOTE]
>
>在範本上設定即可使用上述機制。 如需詳細資訊，請參閱設定回應式佈局。 <!-- Use of the above mechanisms is enabled by configuration on the template. See [Configuring Responsive Layout](/help/sites-administering/configuring-responsive-layout.md) for further information.-->

## 配置定義、裝置模擬和中斷點 {#layout-definitions-device-emulation-and-breakpoints}

建立網站內容時，您想要確保內容顯示方式適合用來檢視內容的裝置。

AEM可讓您根據裝置的寬度定義版面：

* 模擬器可讓您在多種裝置上模擬這些版面。 除了裝置型別、方向之外，還選取了 **旋轉裝置** 選項，可能會隨著寬度變更而影響所選取的中斷點。
* 中斷點是區分配置定義的點。
   * 它們實際上會定義任何使用特定版面配置之裝置的最大寬度（以畫素為單位）。
   * 中斷點通常適用於一系列選取的裝置，視其顯示器的寬度而定。
   * 中斷點的範圍會向左延伸，直到下一個中斷點為止。
   * 您無法明確地選取中斷點，選取裝置和方向將會自動選取適當的中斷點。

裝置 **案頭**，沒有特定寬度)與預設中斷點（亦即高於上次設定中斷點的所有內容）有關。

>[!NOTE]
>
>您可以為每個個別裝置定義中斷點，但這會大幅增加定義和維護版面配置所需的工作。

使用模擬器時，您可以選取特定裝置來模擬和定義版面，相關的中斷點也會反白顯示。 您所做的任何配置變更都適用於中斷點套用的其他裝置。 亦即，任何位於作用中中斷點標籤左側、但位於下一個中斷點標籤之前的裝置。

例如，當您選取裝置時 **iPhone 6 Plus** （定義寬度為540畫素）用於模擬和配置，中斷點 **電話** （定義為768畫素）也會啟動。 您為「 」所做的任何配置變更 **IPHONE 6** 適用於下的其他裝置 **電話** 中斷點，例如 **IPHONE 5** （定義為320畫素）。

![模擬器](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## 選取要模擬的裝置 {#selecting-a-device-to-emulate}

1. 開啟進行編輯所需的頁面。 例如：

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. 選取 **模擬器** 圖示從頂端工具列：

   ![「模擬器」按鈕](/help/sites-cloud/authoring/assets/emulator.png)

1. 模擬器工具列隨即開啟。

   ![模擬器工具列](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   模擬器工具列會顯示其他版面配置選項：

   * **旋轉裝置**  — 可讓您將裝置從垂直（縱向）方向旋轉至水準（橫向）方向，反之亦然。

   ![旋轉裝置橫向按鈕](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![旋轉裝置縱向按鈕](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)

   * **選取裝置**  — 從清單中定義要模擬的特定裝置（請參閱下一步以瞭解詳細資訊）

   ![選取裝置按鈕](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. 若要選取要模擬的特定裝置，您可以：

   * 使用「選取裝置」圖示，並從下拉式選取器選取。
   * 在模擬器工具列中選取裝置指示器。

   ![選擇裝置下拉式清單](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. 選取特定裝置後，您可以：

   * 檢視所選裝置的作用中標籤，例如 **iPad。**
   * 檢視適當的作用中標籤 [中斷點](#layout-definitions-device-emulation-and-breakpoints) 例如 **平板電腦。**
   * 藍色虛線代表 *摺疊* 針對選取的裝置(此處為 **iPhone 6 Plus** 橫向)。

   ![摺頁](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)

   * 摺頁也可以視為分頁符號(不要與 [中斷點](#layout-definitions-device-emulation-and-breakpoints))以取得詳細資訊。 這項顯示是為了方便使用者在捲動前在裝置上看到的內容部分。
   * 如果模擬的裝置高度高於熒幕大小，則不會顯示折線。
   * 顯示摺頁是為了方便作者使用，不會顯示在已發佈的頁面上。

## 新增版面容器及其內容（編輯模式） {#adding-a-layout-container-and-its-content-edit-mode}

A **配置容器** 是段落系統：

* 包含其他元件。
* 定義版面。
* 回應變更。

>[!NOTE]
>
>如果尚未提供，請使用 **配置容器** 必須為段落系統/頁面明確啟動。 <!-- If not already available, the **Layout Container** must be explicitly [activated for a paragraph system/page](/help/sites-administering/configuring-responsive-layout.md).-->

1. 「配 **置容器** 」是元件瀏覽器中的標準 [元件](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)。從這裡，您可以將其拖曳至頁面上的必要位置，之後您會看到 **將元件拖曳到這裡** 預留位置。
1. 然後，您可以將元件新增至版面容器。 這些元件將儲存實際內容：

   ![配置容器](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## 選取配置容器並對其執行動作（編輯模式） {#selecting-and-taking-action-on-a-layout-container-edit-mode}

與其他元件一樣，您可以選取「配置容器」(Layout Container)，然後對其執行剪下、複製、刪除等動作(當執行 **編輯** 模式)：

>[!CAUTION]
>
>由於版面容器是段落系統，刪除元件將會同時刪除版面格線以及容器內容納的所有元件（及其內容）。

1. 如果您將滑鼠移到格點預留位置上或選取該預留位置，則會顯示動作選單。

   ![新增到版面容器](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   您必須選取 **父級** 選項。

   ![父按鈕](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

1. 如果版面元件為巢狀，請選取 **父級** 選項會顯示下拉式選取專案，讓您選取巢狀配置容器或其父項。

   將滑鼠移至下拉式清單中的容器名稱上方時，其外框會顯示於頁面上。

   * 最低的巢狀配置容器外框為藍色。
   * 後續的每個容器都會以較淺的藍色外框標示。

   ![巢狀容器](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

1. 整個格線會以其內容反白顯示。 畫面會顯示動作工具列，您可在其中選取動作，例如 **刪除。**

## 定義版面（版面模式） {#defining-layouts-layout-mode}

>[!NOTE]
>
>您可以為每一個專案定義個別的配置 [中斷點](#layout-definitions-device-emulation-and-breakpoints) （由模擬的裝置型別和方向所決定）。

若要設定以「配置容器」實作的回應式格線的配置，您需要使用 **版面** 模式。

**版面** 啟動模式有兩種方式。

* 使用工具列 [中的模式選單](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) ，然後選擇「 **版面模式」**
   * 選取「 **版面** 」模式，就像切換至「編輯 **」模式或「** 定位 **** 」模式。
   * **配置模式** (Layout **mode)會維持持續性，而且您必須先透過模式選取器** 選取其他模式，才能離開「配置」模式。
* 時間 [編輯個別元件](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout).
   * 藉由使用 **版面** 元件快速動作選單中的選項，您可以切換至 **版面** 模式。
   * **版面** 編輯元件時模式會持續存在並恢復為 **編輯** 將焦點變更為另一個元件後所在的模式。

在版面模式中，您可以在格線上執行各種動作：

* 使用藍點調整內容元件的大小。 調整大小永遠靠齊格點。 調整大小時，背景格點會顯示，以協助對齊：

  ![調整元件大小](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

  >[!NOTE]
  >
  >當元件(如 **影像** 都會重新調整大小。

* 選取內容元件，工具列可讓您：
   * **父級**  — 可讓您選取整個配置容器元件，以便對整體執行動作。
   * **浮動至新行**  — 元件會移至新的一行，視格線內的可用空間而定。
   * **隱藏元件**  — 元件會設定為隱藏（可從配置容器的工具列還原）。

  ![隱藏元件](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

* 在 **版面** 模式您可以選取 **將元件拖曳到這裡** 以選取整個元件。 工具列會針對此模式顯示。

  根據配置元件及其所屬元件的狀態，工具列有不同的選項。 例如：

   * **父級**  — 選取父元件。

     ![父按鈕](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   * **顯示隱藏的元件**  — 顯示所有或個別元件。 數字表示目前有多少個隱藏的元件。 計數器顯示隱藏的元件數量。

     ![顯示隱藏的元件按鈕](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

   * **還原中斷點配置**  — 還原為預設版面。 不會強制使用自訂版面。

     ![還原中斷點配置按鈕](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

   * **浮動至新行**  — 如果間距允許，將元件向上移動一個位置。

     ![浮動至新行按鈕](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

   * **隱藏元件**  — 隱藏目前的元件。

     ![隱藏元件按鈕](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)

  >[!NOTE]
  >
  >在上述範例中，浮動和隱藏動作可供使用，因為此配置容器是巢狀內嵌於上層配置容器中。

   * **取消隱藏元件**
選取父元件以顯示包含「 」的動作工具列 **顯示隱藏的元件** 選項。 在此範例中，隱藏了兩個元件。

     ![取消隱藏元件](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)

  選取「顯 **示隱藏的元件** 」(Show hidden components)選項，會以藍色顯示目前隱藏在原始位置的元件。

  ![全部還原按鈕](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

  選取 **全部還原** 會取消隱藏所有隱藏的元件。

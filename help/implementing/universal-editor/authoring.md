---
title: 使用 Universal Editor 編寫內容
description: 了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: 481202760e0d22cde9c32e0b781dc99f67d463e4
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 69%

---


# 使用 Universal Editor 編寫內容 {#authoring}

了解內容作者使用 Universal Editor 建立內容有多簡單和直覺。

## 簡介 {#introduction}

Universal Editor 支援在任意實作中編輯任何方面的內容，以便提供卓越的體驗、提高內容速度並提供最先進的開發人員體驗。

為此，Universal Editor 為內容作者提供直觀的 UI，只需要最基本的培訓就能立即進入狀況並開始編輯內容。本文件說明了 Universal Editor 的編寫體驗。

>[!TIP]
>
>如需 Universal Editor 的更詳細介紹，請參閱 [Universal Editor 簡介](introduction.md)文件。

>[!NOTE]
>
>Universal Editor 仍處於開發階段。目前尚無法編輯所有內容類型。

## 準備應用程式 {#prepare-app}

為了使用 Universal Editor 編寫應用程式的內容，應用程式必須由開發人員進行檢測以支援編輯器。

>[!TIP]
>
>請參閱 [AEM 中 Universal Editor 快速入門](getting-started.md)，了解設定 AEM 應用程式以使用 Universal Editor 的範例。

## 登入 {#sign-in}

一旦檢測到應用程式與 Universal Editor 一起使用，您將需要登入 Universal Editor。您需要 Adobe ID 才能登入和[存取 Universal Editor。](getting-started.md#request-access)

登入後，請在[位置列中輸入您要編輯的頁面 URL。](#location-bar)這樣一來，您就可以開始編輯內容，例如[文字內容](#text-mode)或[媒體內容](#media-mode)。

## 了解 UI {#ui}

UI 分為五個主要區域。

* [Experience Cloud 標頭](#experience-cloud-header)
* [Universal Editor 標頭](#universal-editor-header)
* [模式邊欄](#mode-rail)
* [編輯器](#editor)
* [元件邊欄](#component-rail)

![Universal Editor UI](assets/ui.png)

### Experience Cloud 標頭 {#experience-cloud-header}

Experience Cloud 標頭會始終顯示在畫面頂端。這是一個錨點，說明您在 Experience Cloud 中的位置，並幫助您導覽到其他 Experience Cloud 應用程式。

![Experience Cloud 標頭](assets/experience-cloud-header.png)

#### Experience Manager {#experience-manager}

選取標頭左側的 Adobe Experience Cloud 連結，導覽至 Experience Manager 解決方案的根目錄，以存取 [Cloud Manager](/help/onboarding/cloud-manager-introduction.md)、[Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md) 和 [Software Distribution](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html) 等工具。

![全域導覽按鈕](assets/global-navigation.png)

#### 組織 {#organization}

這將顯示您目前登入的組織。如果您的 Adobe ID 與多個組織關聯，可點選或按一下以切換到另一個組織。

![組織指示器](assets/organization.png)

#### 解決方案 {#solutions}

點選或按一下解決方案切換器可讓您快速跳轉到其他 Experience Cloud 解決方案。

![解決方案切換器](assets/solutions.png)

#### 說明 {#help}

說明圖示可快速存取學習和支援資源。

![說明](assets/help.png)

#### 通知 {#notifications}

此圖示會標有目前已指派之未完成的[通知](/help/implementing/cloud-manager/notifications.md)數量。

![通知](assets/notifications.png)

#### 使用者屬性 {#user-properties}

點選或按一下代表您使用者的圖示以存取您的使用者設定。如果您沒有設定使用者圖片，則會隨機分配圖示。

![使用者屬性](assets/user-properties.png)

### Universal Editor 標頭 {#universal-editor-header}

Universal Editor 標頭始終顯示在畫面頂端，就在 [Experience Cloud 標頭下方。](#experience-cloud-header)它可讓您快速存取，以導覽到另一個頁面進行編輯和發佈目前的頁面。

![Universal Editor 標頭](assets/universal-editor-header.png)

#### 漢堡選單 {#hamburger-menu}

漢堡選單尚未實作。

![漢堡選單](assets/hamburger-menu.png)

#### 位置列 {#location-bar}

位置列會顯示您正在編輯頁面的網址。點選或按一下以輸入要編輯的其他頁面的網址。

![位置列](assets/location-bar.png)

>[!TIP]
>
>使用快速鍵 `L` 打開網址列。

>[!NOTE]
>
>您希望使用 Universal Editor 編輯的任何頁面都必須[經過檢測以支援 Universal Editor。](getting-started.md)

#### 模擬器設定 {#emulator}

點選或按一下模擬圖示可定義 Universal Editor 呈現頁面的方式。

![模擬器圖示](assets/emulator.png)

點選或按一下模擬圖示即可顯示選項。

![模擬選項](assets/emulation-options.png)

根據預設，編輯器將以桌面版面開啟，其中高度和寬度由瀏覽器自動定義。

您也可以選擇在 Universal Editor 中模擬行動裝置：

* 定義其方向
* 定義寬度和高度
* 變更方向

#### 開啟應用程式預覽 {#open-app-preview}

點選或按一下開啟的應用程式預覽圖示，可在頁面自己的瀏覽器標籤中開啟您目前編輯的頁面，無須使用編輯器即可預覽您的內容。

![開啟應用程式預覽](assets/open-app-preview.png)

>[!TIP]
>
>使用快速鍵 `O`(字母 O) 可開啟應用程式預覽。

#### 發佈 {#publish}

點選或按一下發佈按鈕，以便即時發佈內容變更以供讀者使用。

![發佈按鈕](assets/publish.png)

>[!TIP]
>
>如需有關使用 Universal Visual Editor 進行發佈的詳細資訊，請參閱[使用 Universal Visual Editor 發佈內容](publishing.md)文件。

### 模式邊欄 {#rail}

模式邊欄始終位於編輯器的左側。這樣可讓您在不同編輯模式間輕鬆切換編輯器。

![模式邊欄](assets/mode-rail.png)

#### 預覽模式 {#preview-mode}

在預覽模式下，在編輯器中呈現的頁面就是發佈服務所顯示的樣子。這可讓內容作者透過按一下連結等來導覽內容。

![預覽模式](assets/preview-mode.png)

>[!TIP]
>
>使用快速鍵 `P` 切換到預覽模式。

#### 文字模式 {#text-mode}

在文字模式中，內容作者可以按一下以選取文字內容。

![文字模式](assets/text-mode.png)

* 您可以 [編輯純文字](#editing-content) 就位。
* 您也可以 [編輯RTF文字](#editing-rich-text) 與其他格式選項一起顯示在元件邊欄中。

>[!TIP]
>
>使用快速鍵 `T` 切換到文字模式。

#### 媒體模式 {#media-mode}

在媒體模式中，內容作者可以按一下以選取媒體內容。

![媒體模式](assets/media-mode.png)

內容的詳細資訊會顯示在元件邊欄中，作者也可以 [編輯媒體內容。](#editing-media)

>[!TIP]
>
>使用快速鍵 `M` 可切換至媒體模式。

#### 元件模式 {#component-mode}

在元件模式中，內容作者可以按一下以選取 [內容片段。](/help/assets/content-fragments/content-fragments.md)

![元件模式](assets/component-mode.png)

當您選取內容片段時，其詳細資訊會顯示在元件邊欄中，您可以 [編輯內容片段。](#edit-content-fragment)

>[!TIP]
>
>使用快速鍵 `C` 可切換至元件模式。

#### 編輯 {#edit}

當在 [元件模式，](#component-mode) 如果您選取 [內容片段，](/help/assets/content-fragments/content-fragments.md) 「編輯」選項會出現在模式邊欄上。

![「編輯」圖示](assets/edit.png)

點選或按一下編輯按鈕會開啟 [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor) 在新標籤中，允許您存取內容片段編輯器的完整功能。

您也可以在以下位置編輯內容片段的詳細資訊： [元件欄](#edit-content-fragment) 視工作流程的需求而定。

>[!TIP]
>
>使用快速鍵 `E` 可編輯選取的元件。

### 編輯器 {#editor}

編輯器會佔據大部分視窗，而且是[位置列](#location-bar)中指定之頁面的呈現位置。

* 如果編輯器處於編輯模式，例如 [文字模式](#text-mode) 或 [媒體模式，](#media-mode) 內容將會可編輯，但您無法追蹤連結。
* 如果編輯器在[預覽模式，](#preview-mode)內容就會是可導覽，且您可以進入連結，但無法編輯內容。

![編輯器](assets/editor.png)

### 元件邊欄 {#component-rail}

元件邊欄一律位於編輯器的左側。視其模式而定，可能會顯示在內容或頁面內容之階層中選取的元件詳細資訊。

![元件邊欄](assets/component-rail.png)

#### 屬性模式 {#properties-mode}

在屬性模式下，邊欄會顯示編輯器中目前選取的元件屬性。載入頁面時，這就是元件邊欄的預設模式。

![屬性模式](assets/properties-mode.png)

根據您選取的元件型別，詳細資訊可在屬性邊欄中顯示和修改。

![元件詳細資訊](assets/component-details.png)

請注意，並非所有元件都有可顯示及/或編輯的詳細資料。

>[!TIP]
>
>使用快速鍵 `D` 可切換至屬性模式。

#### 內容樹模式 {#Content-tree-mode}

在內容樹模式下，邊欄會顯示頁面內容的階層。

![內容樹模式](assets/content-tree-mode.png)

在內容樹中選取一個項目時，編輯器會捲動到該內容並予以選取。

![內容樹](assets/content-tree.png)

>[!TIP]
>
>使用快速鍵 `F` 可切換至內容樹模式。


## 編輯內容 {#editing-content}

編輯內容很簡單又直覺。在編輯模式下 ([文字模式](#text-mode)、[媒體模式](#media-mode)和[元件模式](#component-mode))，將滑鼠指標停留於編輯器的內容時，系統會以藍色框醒目提示可編輯內容。

![可編輯的內容會用藍色框醒目顯示](assets/editable-content.png)

請注意，在編輯模式下，點選或按一下內容會選擇它進行編輯。如果您希望透過以下連結瀏覽您的內容，請切換到[預覽模式。](#preview-mode)

依據 [模式](#mode-rail) 您目前所在的位置以及您選取的內容，可能有不同的編輯選項，而且您可以使用來檢閱內容的其他屬性。 [元件欄。](#component-rail)

### 編輯純文字 {#edit-plain-text}

如果您在 [文字模式](#text-mode) 並選取純文字元件，即可就地編輯文字。

![編輯內容](assets/editing-content.png)

只需輸入即可更新內容。 按下Enter/Return鍵，或點選或按一下文字方塊外部以儲存變更。

### 編輯RTF文字 {#edit-rich-text}

如果您在 [文字模式](#text-mode) 並選取RTF文字元件，即可就地編輯文字。

只需輸入即可更新內容。 按下Enter/Return鍵，或點選或按一下文字方塊外部以儲存變更。

此外，元件邊欄中還提供格式化選項和文字的詳細資訊。

![編輯 RTF 文字元件](assets/rich-text-editing.png)

格式變更會自動儲存到您的內容。

### 編輯媒體 {#edit-media}

如果您在 [媒體模式](#media-mode) 如果選取影像，即可在元件邊欄中檢視其詳細資訊。

![編輯媒體](assets/ue-edit-media.png)

點選或按一下 **取代** 元件邊欄中選取影像預覽下方的按鈕，以使用資產資料庫中的另一個影像取代該影像。

1. 此 [資產選擇器](/help/assets/asset-selector.md#using-asset-selector) 視窗會開啟，供您選取資產。
1. 點選或按一下以選取新資產。
1. 點選或按一下 **選取** 以返回取代資產的元件邊欄。

變更會自動儲存至您的內容。

>[!TIP]
>
>使用快速鍵 `R` 以開啟資產選擇器來取代選取的影像。

### 編輯內容片段 {#edit-content-fragment}

如果您在 [元件模式](#component-mode) 然後選取 [內容片段，](/help/assets/content-fragments/content-fragments.md) 您可以在元件邊欄中編輯其詳細資訊。

![編輯內容片段](assets/ue-edit-cf.png)

在所選內容片段的內容模型中定義的欄位會在元件邊欄中顯示和編輯。

變更會自動儲存至您的內容。

如果您想在「 」中編輯內容片段 [內容片段編輯器](/help/assets/content-fragments/content-fragments-managing.md#opening-the-fragment-editor) 請改為按一下 [編輯按鈕](#edit) 在模式邊欄中。

## 預覽內容 {#previewing-content}

內容編輯完成後，您通常會希望瀏覽其內容，以查看它在其他頁面內容中的樣子。在[預覽模式](#preview-mode)中，您可以點選連結，像讀者一樣瀏覽您的內容。內容在編輯器中呈現的樣子就是將會發佈的樣子。

請注意，在預覽模式下，點選或按一下內容的回應與內容讀者的回應一樣。如果您想選取內容進行編輯，請切換至編輯模式，例如[文字模式](#text-mode)或[媒體模式。](#media-mode)

## 其他資源 {#additional-resources}

若要了解有關 Universal Editor 的詳細資訊，請參閱以下文件。

* [Universal Editor 簡介](introduction.md) - 了解 Universal Editor 如何在任意實作中編輯任何方面的內容，以便提供卓越的體驗、提高內容速度並提供最先進的開發人員體驗。
* [使用 Universal Editor 發佈內容](publishing.md) - 了解 Universal Visual Editor 如何發佈內容，和您的應用程式如何處理發佈的內容。
* [AEM 中 Universal Editor 快速入門](getting-started.md) - 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
* [Universal Editor 架構](architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
* [Universal Editor 驗證](authentication.md) - 了解 Universal Editor 如何進行驗證。

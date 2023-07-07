---
title: 使用 Universal Editor 編寫內容
description: 了解內容作者使用 Universal Editor 建立內容有多簡單和直觀。
exl-id: 15fbf5bc-2e30-4ae7-9e7f-5891442228dd
source-git-commit: c6ab2d9b01a3f1abedb06d1d413e7eceb8b1c031
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 49%

---

# 使用 Universal Editor 編寫內容 {#authoring}

了解內容作者使用 Universal Editor 建立內容有多簡單和直觀。

## 簡介 {#introduction}

通用編輯器可讓您編輯任何實作中任何內容的任何方面，因此您可以提供卓越的體驗、提高內容速度，並提供一流的開發人員體驗。

為此，Universal Editor為內容作者提供直覺式UI，只需最少的培訓，就能快速加入並開始編輯內容。

>[!TIP]
>
>如需 Universal Editor 的詳細介紹，請參閱文件[Universal Editor 簡介。](introduction.md)

>[!NOTE]
>
>Universal Editor 仍在開發中，目前無法編輯所有內容類型。

## 準備應用程式 {#prepare-app}

若要使用通用編輯器為應用程式編寫內容，應用程式必須由開發人員檢測以支援編輯器。

>[!TIP]
>
>另請參閱 [AEM中的通用編輯器快速入門](getting-started.md) 有關如何設定AEM應用程式以使用通用編輯器的範例。

## 登入 {#sign-in}

一旦檢測到應用程式與 Universal Editor 一起使用，您將需要登入 Universal Editor。您需要 Adobe ID 才能登入和[存取 Universal Editor。](getting-started.md#request-access)

登入後，請在中輸入您要編輯之頁面的URL [位置列。](#location-bar) 以便您開始編輯內容，例如 [文字內容](#text-mode) 或 [媒體內容。](#media-mode)

## 了解 UI {#ui}

UI分為五個主要區域。

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

這將顯示您目前登入的組織。如果您的 Adobe ID 與多個組織關聯，可點選或點擊以切換到另一個組織。

![組織指示器](assets/organization.png)

#### 解決方案 {#solutions}

點選或點擊解決方案切換器可讓您快速跳轉到其他 Experience Cloud 解決方案。

![解決方案切換器](assets/solutions.png)

#### 說明 {#help}

說明圖示可快速存取學習和支援資源。

![說明](assets/help.png)

#### 通知 {#notifications}

此圖示會加上目前指派的未完成專案之數目 [通知。](/help/implementing/cloud-manager/notifications.md)

![通知](assets/notifications.png)

#### 使用者屬性 {#user-properties}

點選或點擊代表您使用者的圖示以存取您的使用者設定。如果您未設定使用者圖片，則會隨機指派圖示。

![使用者屬性](assets/user-properties.png)

### Universal Editor 標頭 {#universal-editor-header}

Universal Editor 標頭始終顯示在畫面頂端，就在 [Experience Cloud 標頭下方。](#experience-cloud-header) 它可讓您快速導覽至其他頁面進行編輯，並發佈目前頁面。

![Universal Editor 標頭](assets/universal-editor-header.png)

#### 漢堡選單 {#hamburger-menu}

漢堡選單尚未實施。

![漢堡選單](assets/hamburger-menu.png)

#### 位置列 {#location-bar}

位置列會顯示您正在編輯頁面的網址。點選或點擊以輸入要編輯的其他頁面的網址。

![位置列](assets/location-bar.png)

>[!TIP]
>
>使用快速鍵 `L` 打開網址列。

>[!NOTE]
>
>您希望使用 Universal Editor 編輯的任何頁面都必須[經過檢測以支援 Universal Editor。](getting-started.md)

#### 模擬器設定 {#emulator}

點選或按一下模擬圖示，以定義Universal Editor轉譯頁面的方式。

![模擬器圖示](assets/emulator.png)

點選或按一下模擬圖示會顯示選項。

![模擬選項](assets/emulation-options.png)

依預設，編輯器會在瀏覽器自動定義高度和寬度的案頭版面中開啟。

您也可以選擇在Universal Editor中模擬行動裝置和設定：

* 定義其方向
* 定義寬度和高度
* 變更方向

#### 開啟應用程式預覽 {#open-app-preview}

點選或點擊開啟應用程式預覽圖示，以在其瀏覽器中打開您正在編輯的頁面，無需編輯器即可預覽變更。

![開啟應用程式預覽](assets/open-app-preview.png)

>[!TIP]
>
>使用快速鍵 `O` （字母O）以開啟應用程式預覽。

#### 發佈 {#publish}

點選或按一下「發佈」按鈕，這樣您就可以將變更發佈到即時內容，以供讀者使用。

![發佈按鈕](assets/publish.png)

>[!TIP]
>
>如需有關使用 Universal Visual Editor 進行發佈的詳細資訊，請參閱[使用 Universal Visual Editor 發佈內容](publishing.md)文件。

### 模式邊欄 {#rail}

模式邊欄永遠會出現在編輯器的左側。 它可讓您在不同的編輯模式之間輕鬆切換編輯器。

![模式邊欄](assets/mode-rail.png)

#### 預覽模式 {#preview-mode}

在預覽模式下，在編輯器中呈現的頁面就是發佈服務所顯示的樣子。這可讓內容作者透過點擊連結等來導覽內容。

![預覽模式](assets/preview-mode.png)

>[!TIP]
>
>使用快速鍵 `P` 切換到預覽模式。

#### 文字模式 {#text-mode}

在文字模式中，頁面會在編輯器中呈現，但內容作者可以按一下以選取文字內容來編輯頁面。 這是載入頁面時編輯器的預設模式。

![文字模式](assets/text-mode.png)

>[!TIP]
>
>使用快速鍵 `T` 以切換至文字模式。

#### 媒體模式 {#media-mode}

在媒體模式中，頁面會在編輯器中呈現，但內容作者可以按一下以選取媒體內容來編輯頁面。

![媒體模式](assets/media-mode.png)

>[!TIP]
>
>使用快速鍵 `M` 切換到媒體模式。

#### 元件模式 {#component-mode}

在元件模式中，頁面會在編輯器中呈現，但內容作者可以按一下以選取頁面元件。

![元件模式](assets/component-mode.png)

>[!TIP]
>
>使用快速鍵 `C` 以切換至元件模式。

>[!NOTE]
>
>元件模式仍在開發中，目前僅限於選取元件。

### 編輯器 {#editor}

編輯器會佔用大部分視窗，並且是中指定的頁面所在位置。 [位置列](#location-bar) 已呈現。

* 如果編輯器處於編輯模式，例如 [文字模式](#text-mode) 或 [媒體模式，](#media-mode) 內容將可編輯，且您無法關注連結。
* 如果編輯器位於 [預覽模式，](#preview-mode) 內容將可供導覽，您可以關注連結，但您無法編輯內容。

![編輯器](assets/editor.png)

### 元件邊欄 {#component-rail}

元件邊欄一律會沿著編輯器的左側顯示。 視其模式而定，它可以顯示內容或頁面內容階層中所選元件的詳細資訊。

![元件邊欄](assets/component-rail.png)

#### 屬性模式 {#properties-mode}

在屬性模式中，邊欄會顯示編輯器中目前所選元件的屬性。 這是載入頁面時元件邊欄的預設模式。

![屬性模式](assets/properties-mode.png)

所選元件的詳細資訊會顯示在邊欄中。 請注意，並非所有元件都有要顯示的詳細資訊。

![元件詳細資料](assets/component-details.png)

>[!TIP]
>
>使用快速鍵 `D` 以切換至屬性模式。

#### 內容樹模式 {#Content-tree-mode}

在內容樹狀結構模式中，邊欄會顯示頁面內容的階層。

![內容樹模式](assets/content-tree-mode.png)

在內容樹狀結構中選取專案時，編輯器會捲動至該內容並加以選取。

![內容樹](assets/content-tree.png)

>[!TIP]
>
>使用快速鍵 `F` 以切換至內容樹模式。


## 編輯內容 {#editing-content}

編輯內容很簡單又直觀。在編輯模式中([文字模式](#text-mode)， [媒體模式](#media-mode)、和 [元件模式](#component-mode))，將游標移至編輯器中的內容時，可編輯內容會以藍色方塊醒目提示。

![可編輯的內容會用藍色框醒目顯示](assets/editable-content.png)

只需點選或點擊藍色框中的內容即可啟動就地編輯器來進行變更。按 Enter 或返回以儲存變更。

![編輯內容](assets/editing-content.png)

請注意，在編輯模式下，點選或點擊內容會選擇它進行編輯。如果您希望透過以下連結瀏覽您的內容，請切換到[預覽模式。](#preview-mode)

根據您所在的模式和您選取的內容，您可能有不同的就地編輯選項。 此外，您或許可以使用檢閱內容的其他屬性。 [元件欄。](#component-rail)

## 預覽內容 {#previewing-content}

內容編輯完成後，您通常會希望瀏覽其內容，以查看它在其他頁面內容中的樣子。在[預覽模式](#preview-mode)中，您可以點選連結，像讀者一樣瀏覽您的內容。內容在編輯器中呈現的樣子就是將會發佈的樣子。

請注意，在預覽模式下，點選或點擊內容的回應與內容讀者的回應一樣。如果要選取要編輯的內容，請切換到編輯模式，例如 [文字模式](#text-mode) 或 [媒體模式。](#media-mode)

## 其他資源 {#additional-resources}

若要了解有關 Universal Editor 的詳細資訊，請參閱以下文件。

* [通用編輯器簡介](introduction.md)  — 瞭解通用編輯器如何讓您編輯任何實作中任何內容的任何方面，以便提供卓越的體驗、提高內容速度並提供一流的開發人員體驗。
* [使用 Universal Editor 發佈內容](publishing.md) - 了解 Universal Visual Editor 如何發佈內容，和您的應用程式如何處理發佈的內容。
* [AEM 中 Universal Editor 快速入門](getting-started.md) - 了解如何存取 Universal Editor，以及如何開始檢測您的第一個 AEM 應用程式以使用它。
* [Universal Editor 架構](architecture.md) - 了解 Universal Editor 的架構，以及資料如何在其服務和階層之間流動。
* [屬性和類型](attributes-types.md) - 了解 Universal Editor 需要的資料屬性和類型。
* [Universal Editor 驗證](authentication.md) - 了解 Universal Editor 如何進行驗證。

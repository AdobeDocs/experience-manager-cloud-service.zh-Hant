---
title: 了解製作基本知識
description: 了解使用內容片段為無頭CMS製作內容的概念和機制。
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: 60ddcb3f2fd2219b0b1672791703582920825e81
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 3%

---

# 使用AEM製作無頭的基本知識 {#author-headless-basics}

## 迄今為止的故事 {#story-so-far}

在 [AEM無頭內容製作歷程](overview.md) the [簡介](introduction.md) 涵蓋與無頭製作相關的基本概念和術語。

本文以這些為基礎，讓您了解如何為您的AEM無頭專案製作您自己的內容。

## 目標 {#objective}

* **對象**:入門者
* **目標**:介紹無頭式CMS製作的基本知識：
   * 使用AEMaaCS製作簡介
   * 內容片段簡介

## 基本處理 {#basic-handling}

在處理內容片段之前，請先快速介紹如何使用AEM....但沒有什麼能真正取代登入和嘗試使用系統的體驗。

### 製作和發佈 {#author-preview-publish}

AEM安裝通常至少包含兩個環境：

* 作者
* 發佈

您可登入，並使用製作環境產生內容。 準備就緒後，您就會發佈內容，以便可供使用。 對於無頭，這將是對其他應用程式，對於網頁，這將是對網頁上的讀者。

如需詳細資訊，請參閱製作概念。

### 登入 {#signing-in}

與大多數系統一樣，您需要登入。 作為作者，您將獲得：

* 用戶（帳戶）名稱
* 密碼
* 存取登入畫面的連結

您的帳戶將配置為您需要的任何權限。 若您有任何問題，建議您聯絡內部專案支援團隊。

### 導覽 {#navigation}

您首次登入小型線上教學課程時，將會強調使用者介面的部分主要功能。

然後，您就可以使用導覽面板來存取AEM的關鍵區域。 針對內容片段，您將使用 **內容片段** 主控台(對於某些動作，您也會使用 **資產** 控制台)。

您可以選取左上角的Adobe圖示，接著選取小羅盤圖示，以開啟「導覽面板」。

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>雖然內容片段是AEM的功能 **網站**，則會儲存為 **資產**. 這是不應影響您的技術詳細資訊，但可能有助於了解。

在主控台中，您可以選取左側面板中的資料夾，以導覽至您的內容片段。 您也可以篩選和/或搜尋。

![內容片段主控台](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

### 操作，選擇，查看 {#actions-selecting-viewing}

在 **內容片段** console工具列中的內容片段可使用一系列動作：

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **在資產中開啟**
* **建立**
* 此 **引用者** 欄也提供顯示該片段所有上層參考的直接連結；包括參考內容片段、體驗片段和頁面。
* 將滑鼠游標暫留在資料夾名稱上會顯示JCR路徑。

選取片段後，所有適當的動作皆可使用：

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **開啟**
* **發佈** (和 **取消發佈**)
* **複製**
* **移動**
* **重新命名**
* **刪除**

>[!NOTE]
>
>「發佈」、「取消發佈」、「刪除」、「移動」、「重新命名」、「複製」等動作會觸發非同步作業。 可透過AEM非同步作業UI監控該作業的進度。

<!--
The **Assets** console has dedicated **Action Toolbars**, and **Quick Actions** that you can use after selecting a resource (for example, a folder or content fragment).

The Quick Actions are available for a single resource, see **Basel** in the example below:

![Quick Actions](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

The Actions Toolbar provides access to the full range of actions - applicable for the current scenario. The actions available can change; for example, dependent on your location, or whether you have selected multiple resources:

![Action Toolbar](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

You can select the format for viewing your resources with the View Selector:

![View Selector](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

You can view additional information about items using the Rail Selector. This also gives access to additional actions.

![Left Rail](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)
-->

## 製作內容片段 {#authoring-content-fragments}

因此，這是AEM使用者介面(UI)的簡介，但希望您有機會試用。 現在，我們開始關注您真正的興趣 — 無頭的內容片段。

我們必須從頭到尾逐步處理，但您的執行個體可能已建立資料夾和/或片段，且這些可能位於不同位置。 原則是一樣的。

### 組織和導覽 {#organizing-and-navigating}

除非您有很少的內容片段，否則您會想要加以整理，以便您（和其他人）能再次找到這些片段。

#### 建立資料夾 {#creating-folder}

您可以在內建立一系列資料夾，以完成此操作 **檔案** 區段 **資產** 控制台。 選取 **建立** 選項（右上角），後跟 **資料夾**:

![建立資料夾選項](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

將會開啟一個對話方塊，您可在其中輸入詳細資訊，然後使用 **建立**:

![建立資料夾對話方塊](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### 使用路徑和標籤來限制資料夾中可用的內容片段模型 {#tags-paths-for-models-in-folder}

本節稍微更進階。 如果你只是開始嘗試，你並不需要它，但是 *very* 當您有許多片段時很實用。 所以，即使你還沒用到它，也很好。

您的內容架構師會建立目前專案所需的所有內容片段模型，可能也會建立其他專案。 為協助您和其他作者將事情簡單明瞭，您可以限制特定資料夾可用的模型清單。

建立資料夾後，您可以開啟資料夾 **屬性**. 此處提供各種標籤，其中包含資料夾的相關資訊和設定詳細資訊。 尤其是內容片段，您可以使用 **原則** 標籤來定義此資料夾的特定路徑和/或標籤。 這會限制資料夾中可用的內容片段模型，因為這表示內容片段模型必須先符合這些需求，才能用來在此資料夾中產生片段。

![建立資料夾屬性 — 策略](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>您可以在「內容片段模型 — 允許資產資料夾中的內容片段模型」下閱讀更多詳細資訊。

接著，您可導覽這些資料夾以建立和編輯您的內容片段。

#### 以防萬一 — 資料夾Cloud Services設定 {#cloud-services-folder}

以防萬一……

您可能會獲得一個初始資料夾，可在其中建立資料夾。 這就是某些配置詳細資訊必須（通常由開發人員或系統管理員）應用到根資料夾的情況。 您可能不會因此而感興趣，但如有需要，您可以檢查 **設定** 在 **Cloud Services** 的 **屬性**:

![建立資料夾屬性 — 配置](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>您可以在「將設定套用至資產資料夾」下閱讀更多資訊。

### 建立內容片段 {#creating-fragment}

在 **內容片段** 您可以使用 **建立** 開啟 **新內容片段** 對話框：

![內容片段主控台 — 建立新片段](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

指定：

* **位置**
* **內容片段模型**
* **標題**
* **名稱**
* **說明**

然後使用 **建立** 或 **建立和開啟**.

<!--
Creating a Content Fragment is very similar - you just use the **Content Fragment** option instead:

![Create Content Fragment option](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

This time a wizard opens. The first step is to select the Content Fragment Model that your fragment will be based on:

![Create Content Fragment - select Model](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

After continuing with **Next** you can supply the details (**Basic** and **Advanced**) for your fragment:

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirm with **Create** and you can then **Open** your fragment in the editor.
-->

### 編輯片段 {#editing-fragment}

您可以在建立片段後立即開啟片段，或從「內容片段」主控台（也可從「資產」主控台）選取片段。

編輯器首次開啟時，您會看到：

* 左側的圖示清單 — 這可讓您存取各種功能。 編輯器隨即在 **變異** 頁簽，即可進行大部分編輯。 您可能也對 **註解** 和 **中繼資料** 標籤。

* 標題，包含片段的相關資訊以及各種動作的存取權。

* 主要編輯區域 — 這取決於用來建立片段的模型。

例如：

* 僅需要多個資訊片段，部分資訊具有特定類型。 對於無頭式內容，參考是關鍵，您稍後將在歷程中了解這些內容。

   ![內容片段編輯器 — 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* 可讓您撰寫長區段文字的片段。 此處提供管理和格式化文字的其他選項。 您甚至可以在全螢幕編輯器中開啟個別的文字欄位（使用右側的類似螢幕的小型圖示）

   ![內容片段編輯器 — Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>若要協助作者詳細說明如何成功完成某些欄位，可能需要專案特定檔案。
>
>如需一般詳細資訊，請參閱內容片段模型 — 資料類型和屬性。

使用 **儲存** 或 **儲存並關閉**.

>[!NOTE]
>
>如需詳細資訊，您可以閱讀變體 — 編寫內容片段。

#### 你（也許）不用擔心 {#what-you-probably-do-not-need-to-worry-about}

好，這看起來可能有點奇怪，但一旦您開啟內容片段編輯器並開始探索，就會看到各種選項（可能）不適用於您作為內容作者的無頭歷程。 所以，這只是一個簡短的提醒，說明在無頭的環境中，你應該能夠忽略的事情：

* **內容片段模型**

   您會在編輯器頂端看到內容片段模型的名稱，緊接在片段名稱下方。 這也是帶您前往模型編輯器的連結。
內容片段模型實際上對您的內容片段至關重要，因為它們定義了您使用的結構。 不過，建立和編輯這些角色（通常）是其他角色（內容架構師）的責任。

   >[!NOTE]
   >
   >如果您想深入了解，可以閱讀AEM Headless Content Architect歷程。

* **相關聯的內容**

   這個很明顯，因為是編輯的標籤。

   AEM中有相當多版本的內容片段可用。 原本在編寫頁面時可供「傳統」使用…….而它們仍被用在這個背景中。 這可能涉及關聯資產（例如影像），雖然這些資產不內嵌於片段中，但製作頁面時需要供作者使用。

* **預覽**

   這是編輯器中的另一個標籤，提供技術檢視，主要供開發人員使用。

* **更新頁面參考**

   此動作可從 **...** （點）下拉式清單。 無頭作者對此並不感興趣，因為它與頁面編寫相關。

### 發佈 {#publishing}

<!-- needs more details -->

完成片段後，您可以 **發佈** 這樣，它就可供無頭應用程式使用。

發佈動作可在編輯器中使用(或位於 **內容片段** 主控台或 **資產** 控制台):

![內容片段編輯器 — 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## 下一步 {#whats-next}

現在您已了解基本知識，下一步就是 [了解參考資料](references.md). 這將介紹並討論各種可用的參照，以及如何使用片段參考（無頭創作的關鍵部分）建立結構層級。

## 其他資源 {#additional-resources}

* [製作概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 此頁面主要根據 **網站** 主控台，但有許多/大部分功能也與製作相關 **內容片段** 在 **資產** 控制台。

   * [導覽面板](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [標題](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [動作工具列](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [檢視及選取資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [邊欄選取器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

   * 發佈

      * [快速發佈](/help/assets/manage-publication.md#quick-publish)

      * [管理發佈](/help/assets/manage-publication.md#manage-publication)

* [使用內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [管理內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

      * [將設定套用至資產資料夾](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [建立內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [變化 — 編寫內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [內容片段模型 — 資料類型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [內容片段模型 — 屬性](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [內容片段模型 — 允許資產資料夾上的內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* 快速入門手冊
   * [建立資產資料夾無頭設定](/help/headless/setup/create-assets-folder.md)

* AEM無頭式內容架構者歷程

* AEM無頭翻譯歷程

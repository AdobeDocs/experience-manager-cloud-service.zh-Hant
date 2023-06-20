---
title: 了解編寫基本知識
description: 了解使用內容片段為 Headless CMS 編寫內容的概念和機制。
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 97%

---

# AEM Headless 編寫基本知識 {#author-headless-basics}

## 到目前為止 {#story-so-far}

在[AEM Headless 內容作者歷程](overview.md)的一開始，[簡介](introduction.md)部分介紹了和無周邊內容編寫相關的基本概念和術語。

本文以這些內容為基礎，以便您了解如何為 AEM 無周邊專案編寫您自己的內容。

## 目標 {#objective}

* **對象**：初學者
* **目標**：介紹 Headless CMS 編寫的基本知識：
   * 使用 AEMaaCS 編寫簡介
   * 內容片段簡介

## 基本處理 {#basic-handling}

在您掌握內容片段之前，對於如何使用 AEM，這裡有 (非常) 快速的介紹......但沒有什麼能真正取代登入和嘗試使用系統的體驗。

### 作者、預覽和發佈 {#author-preview-publish}

AEM 安裝通常至少包含三個環境：

* 作者
* 發佈
* 預覽

登入並使用作者環境來產生您的內容。準備好內容後，就可以發佈，使其普遍可用。對於無周邊，這將針對其他應用程式，對於網頁，這將針對網路讀者。

如需詳細資訊，請參閱編寫概念。

在發佈之前，您還可以從&#x200B;**內容片段**&#x200B;主控台發佈至&#x200B;**預覽服務**，以進行測試和預覽。請參閱「發佈和預覽片段」。

### 登入 {#signing-in}

和大多數系統一樣，您需要登入。 身為作者，您會獲得：

* 使用者 (帳戶) 名稱
* 密碼
* 存取登入畫面的連結

您的帳戶將設定成具有任何您需要的權限。如果您有任何問題，建議聯絡您的內部支援團隊。

### 導覽 {#navigation}

首次登入小型線上教學課程，將會重點介紹使用者介面的一些主要功能。

然後，您可以使用導覽面板存取 AEM 的關鍵區域。對於內容片段，請使用 **內容片段** 主控台(針對某些動作，您也會使用 **資產** 主控台)。

可以透過選擇左上角的 Adobe 圖示，然後選擇小羅盤圖示來開啟導覽面板。

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>雖然內容片段是 AEM **Sites** 的功能，但它們也另存為&#x200B;**資產**。這個技術細節不會影響您的操作，但了解它可能會有用。

在主控台中，您可以在左側面板中選擇資料夾以導覽至您的內容片段。您還可以篩選和/或搜尋。

![內容片段主控台](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

### 動作、選擇、檢視 {#actions-selecting-viewing}

在&#x200B;**內容片段**&#x200B;主控台中，工具列中有一系列動作可用於您的內容片段：

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **在 Assets 中開啟**
* **建立**
* **參考者**&#x200B;欄也提供直接連結以顯示該片段的所有父參考；包括參考內容片段、體驗片段和頁面。
* 將游標停留在資料夾名稱上將顯示 JCR 路徑。

選擇您的片段後，所有適當的動作都可用：

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **開啟**
* **發佈** (和&#x200B;**取消發佈**)
* **複製**
* **移動**
* **重新命名**
* **刪除**

>[!NOTE]
>
>發佈、取消發佈、刪除、移動、重新命名、複製等動作觸發非同步作業。可以透過 AEM 非同步作業 UI 監視該作業的進度。

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

## 編寫內容片段 {#authoring-content-fragments}

所以，這是對 AEM 使用者介面 (UI) 的非常快速介紹，但希望您有機會嘗試一下。現在我們開始討論您真正感興趣的部分 - Headless 內容片段。

我們必須從頭到尾說明所有事情，但是您的執行個體可能已經建立了資料夾和/或片段，並且它們可能位於不同的位置。原理是一樣的。

### 組織和導覽 {#organizing-and-navigating}

除非您的內容片段很少，否則您會想要加以組織，以便您 (和其他人) 可以再次找到它們。

#### 建立資料夾 {#creating-folder}

為此，您可以在&#x200B;**資產**&#x200B;主控台的&#x200B;**檔案**&#x200B;區段內，建立一系列的資料夾。選擇&#x200B;**建立**&#x200B;選項 (右上角)，然後選擇&#x200B;**資料夾**：

![建立資料夾選項](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

對話框隨即開啟，您可以在其中輸入詳細資料，然後使用&#x200B;**建立**&#x200B;加以確認：

![建立資料夾對話框](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### 使用路徑和標記限制資料夾中可用的內容片段模型 {#tags-paths-for-models-in-folder}

本章節的技術稍微進階一些。如果您才剛開始嘗試，您並不需要它，但是當您有很多片段時，它就&#x200B;*非常*&#x200B;實用。所以了解它是件好事 - 即使您還沒有使用它。

您的內容架構師將建立您目前專案所需的所有內容片段模型，一些其他專案可能也需要。為了協助您和其他作者簡化作業，您可以對特定資料夾的可用模型清單加以限制。

建立資料夾後，您可以開啟&#x200B;**屬性**&#x200B;資料夾。這裡有各種索引標籤，其中包含有關資料夾的資訊和設定詳細資料。特別是對於內容片段，您可以使用&#x200B;**原則**&#x200B;索引標籤為此資料夾定義特定路徑和/或標記。這限制了可在資料夾中使用的內容片段模型，因為這表示內容片段模型必須滿足這些要求才能用來在此資料夾中產生片段。

![建立資料夾屬性 - 原則](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>您可以在「內容片段模型 - 允許在資產資料夾中使用內容片段模型」下閱讀更多詳細資訊。

然後瀏覽這些資料夾以建立和編輯您的內容片段。

#### 以防萬一 - 資料夾雲端服務設定 {#cloud-services-folder}

以防萬一...

您可能會得到一個初始資料夾，您可以在其中建立資料夾。這是因為一些設定細節必須套用 (通常由開發人員或系統管理員執行) 到根資料夾。您可能對此不感興趣，但如果有必要，您可以查看&#x200B;**屬性**&#x200B;資料夾中&#x200B;**雲端服務**&#x200B;的&#x200B;**設定**：

![建立資料夾屬性 - 設定](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>您可以在「將設定套用到資產資料夾」下閱讀更多資訊。

### 建立內容片段 {#creating-fragment}

在&#x200B;**內容片段**&#x200B;主控台，您可以使用&#x200B;**建立**&#x200B;來開啟&#x200B;**新的內容片段**&#x200B;對話框：

![內容片段主控台 - 建立新片段](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

指定：

* **位置**
* **內容片段模型**
* **標題**
* **名稱**
* **說明**

然後使用&#x200B;**建立**&#x200B;或&#x200B;**建立並開啟**&#x200B;加以確認。

<!--
Creating a Content Fragment is very similar - you just use the **Content Fragment** option instead:

![Create Content Fragment option](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

This time a wizard opens. The first step is to select the Content Fragment Model that your fragment is based on:

![Create Content Fragment - select Model](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

After continuing with **Next** you can supply the details (**Basic** and **Advanced**) for your fragment:

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirm with **Create** and you can then **Open** your fragment in the editor.
-->

### 編輯片段 {#editing-fragment}

您可以在建立片段後立即開啟它，或者從內容片段主控台 (也可以從資產主控台) 中選擇它以開啟。

編輯器首次開啟時，您會看到：

* 左側有一列圖示 - 可讓您存取各個功能區域。編輯器會在&#x200B;**變化**&#x200B;索引標籤中開啟，這是大部分編輯進行的地方。您可能也對&#x200B;**附註**&#x200B;和&#x200B;**中繼資料**&#x200B;索引標籤感興趣。

* 包含片段資訊的標頭，以及對各種動作的存取。

* 主編輯區域 - 這取決於用於建立片段的模型。

例如：

* 只需要多個資訊的片段，其中一些具有特定類型。對於無周邊內容，參考是關鍵，歷程的後續部分將會說明。

  ![內容片段編輯器 - 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* 允許您編寫一長段文字的片段。這裡有用於管理和格式化文字的其他選項。您甚至可以在全螢幕編輯器中開啟各個文字欄位 (使用右側外觀像螢幕的小圖示)

  ![內容片段編輯器 - Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>可能需要專案特定文件來協助作者詳細了解如何成功完成某些欄位。
>
>如需一般詳細資訊，請參閱內容片段模型 - 資料類型和屬性。

使用&#x200B;**儲存**&#x200B;或&#x200B;**儲存並關閉**&#x200B;確認您的更新。

>[!NOTE]
>
>如需更多詳細資訊，您可以閱讀「變化 - 編寫內容片段」。

#### 你 (可能) 不需要擔心的事情 {#what-you-probably-do-not-need-to-worry-about}

好的，這部分可能看起來有點奇怪，但是一旦您開啟內容片段編輯器並開始探索，您就會看到各種選項 (可能) 不適用於您作為內容作者的無周邊歷程。所以這只是在快速提示無周邊情境中你可忽略的東西：

* **內容片段模型**

  您將在編輯器頂端看到內容片段模型的名稱 - 就在片段名稱下方。這也是一個將您帶到模型編輯器的連結。
內容片段模型實際上對您的內容片段至關重要，因為它們定義了您使用的結構。然而，建立和編輯模型 (通常) 是另一個角色的責任，即內容架構師。

  >[!NOTE]
  >
  >如果想進一步了解，請參閱「AEM Headless 內容架構師歷程」。

* **相關聯的內容**

  這個非常明顯，因為它是編輯器中的索引標籤。

  內容片段已在多個版本的 AEM 中使用。最初，它們在編寫頁面時可用於「傳統」用途……並且它們仍用於此種情況。這可能涉及關聯資產 (影像)，這些資產雖然未嵌入片段中，但作者在編寫頁面時仍需要使用。

* **預覽**

  這是編輯器中的另一個索引標籤，提供技術檢視，主要供開發人員使用。

* **更新頁面參考**

  **...** (省略符號) 下拉式清單可提供此動作。對於無周邊作者來說這並不有趣，因為它與頁面編寫有關。

### 發佈 {#publishing}

<!-- needs more details -->

完成片段後，您可以&#x200B;**發佈**&#x200B;以供無周邊應用程式使用。

可在編輯器中使用發佈動作：

![內容片段編輯器 - 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>您還可以從&#x200B;**資產**&#x200B;或者&#x200B;**內容片段**&#x200B;主控台發佈片段。

## 下一步 {#whats-next}

現在您已經了解基本知識，下一步是[了解參考](references.md)。這將介紹和討論可用的各種參考，以及如何建立片段參考的結構階層，這是無周邊內容編寫的關鍵部分。

## 其他資源 {#additional-resources}

* [編寫概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md) - 此頁面主要根據&#x200B;**Sites** 主控台，但許多/大部分功能也和編寫 **Assets** 主控台下的&#x200B;**內容片段**&#x200B;相關。

   * [導覽面板](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [標頭](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [動作工具列](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [檢視和選擇資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [邊欄選擇器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

* [使用內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [管理內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

   * [套用設定到資產資料夾](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

   * [建立內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [變化 - 編寫內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * 發佈

      * 從編輯器，或&#x200B;**資產**&#x200B;主控台

         * [快速發佈](/help/assets/manage-publication.md#quick-publish)

         * [管理發佈](/help/assets/manage-publication.md#manage-publication)

      * 從&#x200B;**內容片段**&#x200B;主控台

         * [發佈和預覽內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-previewing-a-fragment)

   * [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [內容片段模型 - 資料類型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [內容片段模型 - 屬性](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [內容片段模型 - 允許內容片段模型在資產資料夾上](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* 快速入門指南
   * [建立資產資料夾 - Headless 設定](/help/headless/setup/create-assets-folder.md)

* AEM Headless 內容架構師歷程

* AEM Headless 翻譯歷程

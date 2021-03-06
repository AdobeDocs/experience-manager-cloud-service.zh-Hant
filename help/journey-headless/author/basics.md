---
title: 瞭解創作基礎知識
description: 瞭解使用內容片段為無頭CMS創作內容的概念和機制。
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: 60ddcb3f2fd2219b0b1672791703582920825e81
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 3%

---

# 無頭創作基礎知AEM識 {#author-headless-basics}

## 到目前為止的故事 {#story-so-far}

在 [無AEM頭內容作者之旅](overview.md) 這樣 [導言](introduction.md) 介紹了與無頭創作相關的基本概念和術語。

本文以這些為基礎，以便您瞭解如何為無頭項目編寫自己AEM的內容。

## 目標 {#objective}

* **觀眾**:初學者
* **目標**:介紹無頭CMS創作的基礎知識：
   * AEMaCS創作簡介
   * 內容片段簡介

## 基本處理 {#basic-handling}

在您開始處理內容片段之前，請快速介紹使用AEM...。但沒有什麼能真正取代登錄和嘗試使用系統的體驗。

### 作者和發佈 {#author-preview-publish}

安AEM裝通常至少包括兩個環境：

* 作者
* 發佈

您登錄並使用作者環境生成內容。 準備好後，您將發佈內容，以便其可以正常使用。 對於無頭的應用，對於網頁，這對於網上的讀者。

有關詳細資訊，請參閱創作概念。

### 登錄 {#signing-in}

與大多數系統一樣，您需要登錄。 作為作者，您將獲得：

* 用戶（帳戶）名稱
* 密碼
* 訪問登錄螢幕的連結

您的帳戶將配置為您需要的任何權限。 如果您有任何問題，我們建議您與內部項目支援團隊聯繫。

### 導覽 {#navigation}

首次登錄小型線上教程時，將突出介紹用戶介面的一些主要功能。

然後，可以使用「導航面板」訪問的關鍵AEM區域。 對於內容片段，您將使用 **內容片段** 控制台(對於某些操作，您還將使用 **資產** 控制台)。

通過選擇左上角的Adobe表徵圖，然後是小羅盤表徵圖，可以開啟導航面板。

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>儘管內容片段是 **站點**，它們被保存為 **資產**。 這是一個技術細節，不應影響您，但可能對您有幫助。

在控制台中，您可以在左側面板中選擇資料夾以導航到內容片段。 您還可以過濾和/或搜索。

![內容片段控制台](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

### 操作，選擇，查看 {#actions-selecting-viewing}

在 **內容片段** 控制台工具欄中的內容片段提供了一系列操作：

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **在資產中開啟**
* **建立**
* 的 **引用者** 列還提供了顯示該片段的所有父引用的直接連結；包括引用內容片段、體驗片段和頁面。
* 懸停在資料夾名稱上將顯示JCR路徑。

選擇片段後，所有相應操作都可用：

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **開啟**
* **發佈** (和 **取消發佈**)
* **複製**
* **移動**
* **重新命名**
* **刪除**

>[!NOTE]
>
>諸如「發佈」、「取消發佈」、「刪除」、「移動」、「更名」、「複製」等操作會觸發非同步作業。 可以通過非同步作業UI監AEM視該作業的進度。

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

## 創作內容片段 {#authoring-content-fragments}

因此，這是一個非常快的用戶介面(AEMUI)簡介，但希望您有機會試用它。 現在，我們談談您真正的興趣 — 無頭內容的內容片段。

我們必須從頭到尾都要完成一些操作，但您的實例可能已建立了資料夾和/或碎片，這些資料夾和/或碎片可能位於不同的位置。 原則是一樣的。

### 組織和導航 {#organizing-and-navigating}

除非您的內容片段非常少，否則您將希望組織這些內容片段 — 以便您（和其他人）可以再次找到它們。

#### 建立資料夾 {#creating-folder}

可以通過在 **檔案** 的下界 **資產** 控制台。 選擇 **建立** 選項（右上），後跟 **資料夾**:

![「建立資料夾」選項](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

將開啟一個對話框，您可以在其中輸入詳細資訊，然後使用 **建立**:

![「建立資料夾」對話框](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### 使用路徑和標籤限制資料夾中可用的內容片段模型 {#tags-paths-for-models-in-folder}

此部分稍高一些。 如果你只是開始嘗試，你並不需要它，但是 *非常* 當你有很多碎片時很有用。 所以，即使你還沒用它，瞭解它也是件好事。

您的內容架構師將建立當前項目所需的所有內容片段模型，可能還會建立其他項目。 為了幫助您和其他作者保持簡單，您可以限制特定資料夾可用的模型清單。

建立資料夾後，您可以開啟該資料夾 **屬性**。 這裡有各種頁籤，其中包含有關資料夾的資訊和配置詳細資訊。 特別是對於內容片段，您可以使用 **策略** 頁籤，以定義此資料夾的特定路徑和/或標籤。 這將限制可在資料夾中使用的內容片段模型，因為這意味著內容片段模型必須滿足這些要求，才能用於在此資料夾中生成片段。

![建立資料夾屬性 — 策略](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>您可以在「內容片段模型 — 允許在資產資料夾上使用內容片段模型」下閱讀更多詳細資訊。

然後，在這些資料夾中導航以建立和編輯內容片段。

#### 以防萬一 — 資料夾Cloud Services配置 {#cloud-services-folder}

以防萬一……

您可能會得到一個初始資料夾，您可以在其中建立資料夾。 這是因為必須將某些配置詳細資訊（通常由開發人員或系統管理員）應用到根資料夾。 這可能不會引起您的興趣，但如有必要，您可以檢查 **配置** 的 **Cloud Services** 資料夾 **屬性**:

![建立資料夾屬性 — 配置](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>您可以在Apply the Configuration to your Assets Folder（將配置應用於資產資料夾）下閱讀更多內容。

### 建立內容片段 {#creating-fragment}

在 **內容片段** 控制台可使用 **建立** 開啟 **新內容片段** 對話框：

![內容片段控制台 — 建立新片段](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

指定：

* **位置**
* **內容片段模型**
* **標題**
* **名稱**
* **說明**

然後，通過 **建立** 或 **建立並開啟**。

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

您可以在建立片段後立即開啟它，或從「內容片段」控制台（也從「資產」控制台）中選擇它。

當編輯器首次開啟時，您將看到：

* 左側的表徵圖清單 — 允許您訪問各個功能區域。 編輯器將在 **變體** 的子菜單。 你可能也對 **注釋** 和 **元資料** 頁籤。

* 包含有關片段的資訊以及對各種操作的訪問權限的標頭。

* 主編輯區域 — 這取決於用於建立片段的模型。

例如：

* 只需要多條資訊的片段，有些資訊具有特定類型。 對於無頭內容，參考是關鍵，您稍後將在旅途中瞭解這些內容。

   ![內容片段編輯器 — 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* 允許您寫入長段文本的片段。 此處提供了用於管理和格式化文本的其他選項。 您甚至可以在全屏編輯器中開啟各個文本欄位（使用右側的小螢幕樣表徵圖）

   ![內容片段編輯器 — Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>可能需要項目特定文檔來幫助作者詳細瞭解如何成功完成某些欄位。
>
>有關一般詳細資訊，請參閱內容片段模型 — 資料類型和屬性。

使用以下任一項確認更新 **保存** 或 **保存並關閉**。

>[!NOTE]
>
>有關詳細資訊，請閱讀變體 — 創作內容片段。

#### 你（可能）不需要擔心的 {#what-you-probably-do-not-need-to-worry-about}

好，這似乎有點奇怪，但一旦您開啟內容片段編輯器並開始探索，您就會看到各種選項（可能）不適用於您作為內容作者的無頭旅行。 因此，這只是你在無頭環境中應該忽略的問題的一個簡單提示：

* **內容片段模型**

   您將在編輯器頂部看到內容片段模型的名稱 — 直接在片段名稱下。 這也是指向模型編輯器的連結。
內容片段模型在定義您使用的結構時對內容片段實際上至關重要。 但是，建立和編輯它們（通常）是另一個角色（內容架構師）的責任。

   >[!NOTE]
   >
   >如果您想瞭解更多資訊，可以閱讀「無頭內AEM容架構師之旅」。

* **相關聯的內容**

   這個很明顯，因為它是編輯器中的一個頁籤。

   Content Fragments已在中提供AEM，可用於許多版本。 最初，在創作頁面時，它們可供「傳統」使用……。在這個背景下，它們仍然被使用。 這可能涉及關聯資產（例如影像），這些資產雖然未嵌入到片段中，但在創作頁面時，作者需要提供。

* **預覽**

   這是編輯器中的另一個頁籤，它提供了技術視圖，主要面向開發人員。

* **更新頁面參考**

   此操作可從 **...** （橢圓）下拉。 對於無頭作者來說，這並不有趣，因為它與頁面創作相關。

### 發佈 {#publishing}

<!-- needs more details -->

完成碎片後，您可以 **發佈** 使其可用於無頭應用。

發佈操作可在編輯器中(或從 **內容片段** 控制台或 **資產** 控制台):

![內容片段編輯器 — 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## 下一步 {#whats-next}

既然你已經學到了基本知識，下一步就是 [瞭解有關引用的資訊](references.md)。 這將介紹和討論各種可用參照，以及如何使用「片段參照」(Fragment References)建立結構的級別 — 這是無頭創作的關鍵部分。

## 其他資源 {#additional-resources}

* [製作概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 本頁主要基於 **站點** 控制台，但許多/大多數功能也與創作相關 **內容片段** 下 **資產** 控制台。

   * [導航面板](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [標題](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [動作工具列](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [快速動作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [查看和選擇資源](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [軌道選擇器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

   * 發佈

      * [快速發佈](/help/assets/manage-publication.md#quick-publish)

      * [管理發佈](/help/assets/manage-publication.md#manage-publication)

* [使用內容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [管理內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

      * [將配置應用到您的資產資料夾](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [建立內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [變體 — 創作內容片段](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [內容片段模型 — 資料類型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [內容片段模型 — 屬性](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [內容片段模型 — 允許在資產資料夾上建立內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* 入門指南
   * [建立資產資料夾無頭設定](/help/headless/setup/create-assets-folder.md)

* 無AEM頭內容架構師旅程

* 無AEM頭翻譯之旅

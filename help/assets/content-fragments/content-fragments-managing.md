---
title: 管理內容片段
description: 瞭解如何使用Assets主控台來管理您的AEM內容片段，這是您無頭內容的基礎。
feature: 內容片段
role: 業務從業人員
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
translation-type: tm+mt
source-git-commit: 114b38142f01b56652a7b840501f7420fdc25562
workflow-type: tm+mt
source-wordcount: '1748'
ht-degree: 9%

---

# 管理內容片段 {#managing-content-fragments}

瞭解如何使用Assets主控台來管理您的AEM內容片段，這是您無頭內容的基礎。

定義[內容片段模型](#creating-a-content-model)後，您可使用這些模型來建立內容片段](#creating-a-content-fragment)。[

[內容片段編輯器](#opening-the-fragment-editor)提供各種[模式](#modes-in-the-content-fragment-editor)，讓您能夠：

* [編輯內容](#editing-the-content-of-your-fragment) 並管 [理變數](#creating-and-managing-variations-within-your-fragment)
* [為片段加上註解](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [將內容與片段建立關聯](#associating-content-with-your-fragment)
* [設定中繼資料](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [查看結構樹](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [預覽JSON表示法](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>可使用內容片段：
>
>* 網頁製作時；請參閱[使用內容片段編寫頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md)。
>* 用於使用含GraphQL](/help/assets/content-fragments/content-fragments-graphql.md)的內容片段進行無頭內容傳送。[


>[!NOTE]
>
>內容片段會儲存為&#x200B;**Assets**，因此主要是從&#x200B;**Assets**&#x200B;主控台管理。

## 建立內容片段{#creating-content-fragments}

### 建立內容模型{#creating-a-content-model}

[在使用結](/help/assets/content-fragments/content-fragments-models.md) 構化內容建立內容片段之前，可啟用並建立內容片段模型。

### 建立內容片段{#creating-a-content-fragment}

建立內容片段的方法為：

1. 導覽至您 **要建立** 片段的「資產」檔案夾。
1. 依序選 **擇「建立**」、「 **內容片段** 」以開啟精靈。
1. 嚮導的第一步要求您指定新片段的基礎。

   * [模型](/help/assets/content-fragments/content-fragments-models.md) -用於建立需要結構化內容的片段；例如，保守 **** 模型

      * 將顯示所有可用的型號。

   選擇後，使用&#x200B;**Next**&#x200B;繼續。

   ![片段基礎](assets/cfm-managing-01.png)

1. 在「屬 **性** 」步驟中指定：

   * **基本**

      * **標題**

         片段標題。

         必要.

      * **說明**

      * **標記**
   * **進階**

      * **名稱**

         姓名；將用於形成URL。

         強制；將會自動從標題衍生，但可以更新。


1. 選擇 **Create**  (建立) 以完成操作，然後選擇 **Open** the fragment for editing (開啟片段以進行編輯) 或返回控制 **台完成**。

   >[!NOTE]
   >在控制台的&#x200B;**清單**&#x200B;模式中，您可以更新&#x200B;**查看設定**&#x200B;以啟用&#x200B;**內容片段模型**&#x200B;列。

## 資產控制台{#actions-for-a-content-fragment-assets-console}中內容片段的動作

在&#x200B;**Assets**&#x200B;主控台中，您的內容片段可使用一系列動作：

* 從工具列；在選擇片段後，所有適當的動作都可供使用。
* 作為[快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions);個別片段卡可用動作的子集。

![動作](assets/cfm-managing-02.png)

選取片段以顯示包含適用動作的工具列：

* **重新處理資產**
* **建立**
* **下載**

   * 將片段儲存為ZIP檔案；您可以定義是否要包含元素、變數、中繼資料。

* **結帳**
* **屬性**

   * 可讓您檢視和／或編輯片段的中繼資料。

* **編輯**

   * 可讓您[開啟片段，以編輯內容](/help/assets/content-fragments/content-fragments-variations.md)及其元素、變化、相關內容和中繼資料。

* **快速發佈**
* **管理發佈**
* **管理標記**
* **至集合**
* **複製** (和 **貼上**)
* **移動**
* **刪除**

>[!NOTE]
>
>其中許多是[ Assets](/help/assets/manage-digital-assets.md)和／或[案頭應用程式AEM](https://helpx.adobe.com/tw/experience-manager/desktop-app/aem-desktop-app.html)的標準動作。

## 開啟片段編輯器{#opening-the-fragment-editor}

要開啟片段進行編輯：

>[!CAUTION]
>
>若要編輯內容片段，您需要[適當的權限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions)。 如果您遇到問題，請與系統管理員聯繫。

>[!CAUTION]
>
>若要編輯內容片段，您需要適當的權限。 如果您遇到問題，請與系統管理員聯繫。

1. 使用&#x200B;**Assets**&#x200B;主控台瀏覽至內容片段的位置。
1. 開啟片段以供編輯，方法為：

   * 按一下／點選片段連結（這取決於控制台檢視）。
   * 選擇片段，然後從工具欄中選擇&#x200B;**編輯**。

1. 片段編輯器將會開啟。 視需要進行變更：

   ![片段編輯器](assets/cfm-managing-03.png)

1. 進行更改後，根據需要使用&#x200B;**Save**、**Save &amp; close**&#x200B;或&#x200B;**Close**。

   >[!NOTE]
   >
   >**「儲存」下** 拉式清單可供您 **** 儲存並關閉。

   >[!NOTE]
   >
   >**儲存與關閉**&#x200B;和&#x200B;**關閉**&#x200B;都會退出編輯器——請參閱[儲存、關閉和版本](#save-close-and-versions)以取得內容片段各種選項運作的完整資訊。

## 內容片段編輯器{#modes-actions-content-fragment-editor}中的模式和動作

「內容片段編輯器」提供多種模式和動作。

### 內容片段編輯器{#modes-in-the-content-fragment-editor}中的模式

使用側面板中的圖示，在各種模式中導覽：

* 變化：[編輯內容](#editing-the-content-of-your-fragment)和[管理變數](#creating-and-managing-variations-within-your-fragment)

* [註解](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [相關聯的內容](#associating-content-with-your-fragment)
* [中繼資料](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [樹狀結構](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [預覽](/help/assets/content-fragments/content-fragments-json-preview.md)

![模式](assets/cfm-managing-04.png)

### 內容片段編輯器{#toolbar-actions-in-the-content-fragment-editor}中的工具列動作

頂端工具列中的某些功能可從多種模式使用：

![模式](assets/cfm-managing-top-toolbar.png)

* 當內容頁面上已參考片段時，會顯示訊息。 您可以&#x200B;**關閉**&#x200B;訊息。

* 使用&#x200B;**切換側面板**&#x200B;圖示可隱藏／顯示側面板。

* 在片段名稱下方，您可以看到用於建立當前片段的[內容片段模型](/help/assets/content-fragments/content-fragments-models.md)的名稱：

   * 名稱也是一個將開啟模型編輯器的連結。

* 查看碎片的狀態；例如，有關建立、修改或發佈時間的資訊。 狀態也會以色碼標示：

   * **新增**:灰色
   * **草稿**:藍色
   * **已發佈**:綠色
   * **已修改**:橘子
   * **已停用**:紅色

* **「保** 存」提供對「保存 **和關閉」** 選項的訪問。

* 三個點(**...**)下拉式清單可存取其他動作：
   * **更新頁面參考**
      * 這會更新任何頁面參考。
   * **[快速發佈](#publishing-and-referencing-a-fragment)**
   * **[管理發佈](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## 保存、關閉和版本{#save-close-and-versions}

>[!NOTE]
>
>版本也可以從時間軸](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)建立、比較和回復。[

編輯器有各種選項：

* **儲** 存並 **儲存並關閉**

   * **保存** 將保存最新更改並保留在編輯器中。
   * **儲存並關** 閉會儲存最新變更並退出編輯器。

   >[!CAUTION]
   >
   >若要編輯內容片段，您需要[適當的權限](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions)。 如果您遇到問題，請與系統管理員聯繫。

   >[!NOTE]
   >
   >在儲存之前，可以先保留在編輯器中，進行一系列變更。

   >[!CAUTION]
   >
   >除了簡單地保存更改外，這些操作還會更新任何引用，並確保Dispatcher按需刷新。 這些變更可能需要時間處理。 因此，對於大型／複雜／重負載系統，效能可能會受到影響。
   >
   >使用&#x200B;**儲存並關閉**，然後快速重新輸入片段編輯器以進行並儲存進一步變更時，請記住這一點。

* **關閉**

   將退出編輯器，而不保存最新的更改（即自最後&#x200B;**Save**&#x200B;以來所做的更改）。

編輯內容片段時，會自AEM動建立版本，以確保在您取消變更時（使用&#x200B;**Close**&#x200B;而不儲存），可還原先前的內容：

1. 當開啟內容片段進行編輯時AEM，會檢查是否存在Cookie型Token，指出&#x200B;*編輯工作階段*&#x200B;是否存在：

   1. 如果找到代號，則片段會視為現有編輯工作階段的一部分。
   2. 如果代號是&#x200B;*not*，且使用者開始編輯內容，則會建立版本，並傳送此新編輯工作階段的代號給用戶端，並儲存在Cookie中。

2. 雖然有&#x200B;*active*&#x200B;編輯工作階段，但所編輯的內容會每600秒自動儲存一次（預設）。

   >[!NOTE]
   >
   >使用`/conf`機制可配置自動保存間隔。
   >
   >預設值，請參閱：
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果使用者取消編輯，則會還原在編輯工作階段開始時建立的版本，並移除Token以結束編輯工作階段。
4. 如果用戶選擇「保存」編輯，則更新的元素／變化將被保存，並且標籤被移除以結束編輯會話。****

## 編輯片段{#editing-the-content-of-your-fragment}的內容

開啟片段後，您就可以使用[Valuas](/help/assets/content-fragments/content-fragments-variations.md)標籤來製作內容。

## 在片段{#creating-and-managing-variations-within-your-fragment}中建立和管理變化

建立主版內容後，您就可以建立並管理該內容的[Valuas](/help/assets/content-fragments/content-fragments-variations.md)。

## 將內容與片段{#associating-content-with-your-fragment}關聯

您也可以[將內容](/help/assets/content-fragments/content-fragments-assoc-content.md)與片段關聯。 這提供了一種連接，使得資產（即影像）在添加到內容頁面時可（可選）與片段一起使用。

## 查看和編輯片段{#viewing-and-editing-the-metadata-properties-of-your-fragment}的元資料（屬性）

您可以使用[中繼資料](/help/assets/content-fragments/content-fragments-metadata.md)標籤來檢視和編輯片段的屬性。

## 內容片段時間軸{#timeline-for-content-fragments}

除了標準選項外，[Timeline](/help/assets/manage-digital-assets.md#timeline)還提供內容片段的特定資訊和動作：

* 檢視版本、注釋和註解的相關資訊
* 版本動作

   * **[還原為此版本](#reverting-to-a-version)** （選擇現有片段，然後選擇特定版本）

   * **[與目前比較](#comparing-fragment-versions)** （選擇現有片段，然後選擇特定版本）

   * 新增&#x200B;**Label**&#x200B;和／或&#x200B;**Comment**（選取現有片段，然後選取特定版本）

   * **另存為版本** （選擇現有片段，然後選擇時間軸底部的向上箭頭）

* 注釋操作

   * **刪除**

>[!NOTE]
備注如下：
* 所有資產的標準功能
* 在時間軸中製作
* 與片段資產相關

註解（適用於內容片段）包括：
* 在片段編輯器中輸入
* 特定於片段內選取的文字區段



例如：

![時間軸](assets/cfm-managing-05.png)

## 比較片段版本{#comparing-fragment-versions}

在您選擇特定版本後，**Timeline](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)的[「比較目前**」動作可從Timeline使用。

此選項將開啟：

* **Current**（最新）版本（左）

* 所選版本&#x200B;**v&lt;*x.y*>**（右）

它們將並排顯示，其中：

* 會反白顯示任何差異

   * 已刪除的文字——紅色
   * 插入的文本——綠色
   * 已取代文字——藍色

* 全螢幕圖示可讓您自行開啟任一版本；然後切換回平行檢視
* 您可以&#x200B;**將**&#x200B;還原為特定版本
* **Donewill** return you to the console

>[!NOTE]
比較片段時，無法編輯片段內容。

![比較](assets/cfm-managing-06.png)

## 還原為{#reverting-to-a-version}版本

您可以回復到特定版本的片段：

* 直接從[時間軸](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

   選擇所需的版本，然後選擇&#x200B;**恢復到此版本**&#x200B;操作。

* 當[比較版本與當前版本](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)時，您可以&#x200B;**將**&#x200B;還原為選定版本。

## 發佈和引用片段{#publishing-and-referencing-a-fragment}

>[!CAUTION]
如果您的片段是以模型為基礎，則應確定[模型已發佈](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)。
如果您發佈模型尚未發佈的內容片段，則選擇清單會指出此點，而模型將會隨片段一起發佈。

必須發佈內容片段才能在發佈環境中使用。 可發佈：

* 建立後；使用「資產」控制台](#actions-for-a-content-fragment-assets-console)中可用的[動作。
* 從[內容片段編輯器](#toolbar-actions-in-the-content-fragment-editor)。
* 當您[發佈使用片段](/help/sites-cloud/authoring/fundamentals/content-fragments.md#publishing)的頁面時；片段將列在頁面參考中。

>[!CAUTION]
發佈和／或參考片段後，當作AEM者開啟片段以進行重新編輯時，會顯示警告。 這會警告對片段所做的變更也會影響參照的頁面。

## 刪除片段{#deleting-a-fragment}

要刪除片段：

1. 在&#x200B;**Assets**&#x200B;主控台中，導覽至內容片段的位置。
2. 選擇片段。

   >[!NOTE]
   **Delete**&#x200B;動作不提供快速動作。

3. 從工具欄中選擇&#x200B;**Delete**。
4. 確認&#x200B;**Delete**&#x200B;動作。

   >[!CAUTION]
   如果片段已在頁面中參考，您會看到警告訊息，並需要確認您要繼續執行強制刪 **除**。片段及其內容片段元件將會從任何內容頁面中刪除。

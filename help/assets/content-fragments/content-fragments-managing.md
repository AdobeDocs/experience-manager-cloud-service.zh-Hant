---
title: 管理內容片段（資產 — 內容片段）
description: 瞭解如何使用Assets主控台來管理您的AEM內容片段，作為Headless內容或頁面編寫的基礎。
exl-id: 333ad877-db2f-454a-a3e5-59a936455932
feature: Content Fragments
role: User, Admin
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 7%

---

# 管理內容片段 {#managing-content-fragments}

瞭解如何使用Assets主控台來管理您的AEM內容片段，作為Headless內容或頁面編寫的基礎。

定義您的 [內容片段模型](#creating-a-content-model) 您可以使用這些來 [建立您的內容片段](#creating-a-content-fragment).

此 [內容片段編輯器](#opening-the-fragment-editor) 提供各種 [模式](#modes-in-the-content-fragment-editor) 若要讓您：

* [編輯內容](#editing-the-content-of-your-fragment) 和 [管理變數](#creating-and-managing-variations-within-your-fragment)
* [為片段加上註釋](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [將內容與片段相關聯](#associating-content-with-your-fragment)
* [設定中繼資料](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [檢視結構樹](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [預覽JSON表示法](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>可以使用內容片段：
>
>* 編寫頁面時；請參閱 [使用內容片段編寫頁面](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* 的 [搭配GraphQL使用內容片段的Headless內容傳送](/help/assets/content-fragments/content-fragments-graphql.md).

>[!NOTE]
>
>內容片段是 Sites 的一項功能，但儲存為&#x200B;**資產**。
>
>他們現在主要透過 **[內容片段](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)** 主控台，但仍可從 **資產** 主控台。 本節涵蓋以下專案的管理： **資產** 主控台。
>
>編寫內容片段有兩個編輯器。 本節介紹原始編輯器，主要透過以下網址存取： **資產** 主控台。 請參閱網站檔案， [內容片段 — 製作](/help/sites-cloud/administering/content-fragments/authoring.md)，以取得新編輯器的詳細資訊(主要透過以下網址存取： **內容片段** 主控台)。 兩個編輯器在頂部工具欄中都有一個切換開關，用於提供對另一個編輯器的快速存取。

## 建立內容片段 {#creating-content-fragments}

### 建立內容模型 {#creating-a-content-model}

[內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 可以在使用結構化內容建立內容片段之前啟用和建立。

### 建立內容片段 {#creating-a-content-fragment}

建立內容片段的方法是：

1. 導覽至您 **要建立** 片段的「資產」檔案夾。
1. 依序選 **擇「建立**」、「 **內容片段** 」以開啟精靈。
1. 嚮導的第一步要求您指定新片段的基礎。

   * [模型](/help/assets/content-fragments/content-fragments-models.md)  — 用來建立需要結構化內容的片段；例如 **冒險** 模型

      * 所有可用的模型都會顯示。

   選取後，使用 **下一個** 以繼續進行。

   ![選取內容片段模型](assets/cfm-managing-01.png)

1. 在「屬 **性** 」步驟中指定：

   * **基本**

      * **標題**

        片段標題。

        強制。

      * **說明**

      * **標籤**

   * **進階**

      * **名稱**

        名稱；用於組成URL。

        必要；自動從標題衍生，但可以更新。

1. 選擇 **Create**  (建立) 以完成操作，然後選擇 **Open** the fragment for editing (開啟片段以進行編輯) 或返回控制 **台完成**。

   >[!NOTE]
   >在 **清單** 控制檯模式，您可以更新 **檢視設定** 以啟用 **內容片段模型** 欄。

## Assets控制檯中內容片段的動作 {#actions-for-a-content-fragment-assets-console}

在 **資產** 主控台您的內容片段可使用的一系列動作，包括：

* 從工具列；選擇片段後，所有適當的動作都可使用。
* 作為 [快速動作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)；可用於個別片段卡片之動作的子集。

![工具列中的動作](assets/cfm-managing-02.png)

選取片段以顯示包含適用動作的工具列：

* **重新處理資產**
* **建立**
* **下載**

   * 將片段儲存為ZIP檔案；您可以定義是否包含元素、變數、中繼資料。

* **簽出**
* **屬性**

   * 可讓您檢視、編輯（或兩者）片段的中繼資料。

* **編輯**

   * 可讓您 [開啟片段以編輯內容](/help/assets/content-fragments/content-fragments-variations.md) 及其元素、變數、關聯內容和中繼資料。

* **快速發佈**
* **管理發佈**
* **管理標籤**
* **至集合**
* **複製** (和 **貼上**)
* **移動**
* **刪除**

>[!NOTE]
>
>其中許多是 [資產的標準動作](/help/assets/manage-digital-assets.md) 和/或 [AEM案頭應用程式](https://helpx.adobe.com/tw/experience-manager/desktop-app/aem-desktop-app.html).

## 開啟片段編輯器 {#opening-the-fragment-editor}

若要開啟片段進行編輯：

>[!CAUTION]
>
>若要編輯內容片段，您需要 [適當的許可權](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 如果您遇到問題，請聯絡您的系統管理員。

1. 使用 **資產** 控制檯以導覽至您的內容片段位置。
1. 透過以下任一方式開啟片段進行編輯：

   * 按一下/點選片段或片段連結（這取決於主控台檢視）。
   * 選取片段，然後 **編輯** 工具列中的。

1. 片段編輯器隨即開啟。 視需要進行變更：

   ![片段編輯器](assets/cfm-managing-03.png)

1. 進行變更後，請使用 **儲存**， **儲存並關閉** 或 **關閉** 視需要。

   >[!NOTE]
   >
   >**儲存並關閉** 可透過 **儲存** 下拉式清單。

   >[!NOTE]
   >
   >兩者 **儲存並關閉** 和 **關閉** 將退出編輯器 — 請參閱 [儲存、關閉和版本](#save-close-and-versions) 以取得有關各種選項如何為內容片段運作的完整資訊。

## 內容片段編輯器中的模式和動作 {#modes-actions-content-fragment-editor}

內容片段編輯器提供各種模式和動作。

### 內容片段編輯器中的模式 {#modes-in-the-content-fragment-editor}

使用側面板中的圖示導覽各種模式：

* 變數： [編輯內容](#editing-the-content-of-your-fragment) 和 [管理您的變數](#creating-and-managing-variations-within-your-fragment)

* [註解](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [相關聯的內容](#associating-content-with-your-fragment)
* [中繼資料](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [樹狀結構](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [預覽](/help/assets/content-fragments/content-fragments-json-preview.md)

![內容片段編輯器中的模式](assets/cfm-managing-04.png)

### 內容片段編輯器中的工具列動作 {#toolbar-actions-in-the-content-fragment-editor}

頂端工具列中的某些功能可以從多種模式使用：

![各種模式中可用的工具列動作](assets/cfm-managing-top-toolbar.png)

* 當內容頁面上已參考片段時，會顯示訊息。 您可以 **關閉** 訊息。

* 您可以使用來隱藏/顯示側面板 **切換側面板** 圖示。

* 在片段名稱下方，您可以看到 [內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 用於建立目前的片段：

   * 該名稱也是開啟模型編輯器的連結。

* 檢視片段的狀態；例如，建立、修改或發佈時間的相關資訊。 狀態也以色彩標示：

   * **新增**：灰色
   * **草稿**：藍色
   * **已發佈**：綠色
   * **已修改**：橙色
   * **已停用**：紅色

* 按鈕可讓您 **嘗試新的編輯器**，直接開啟 *新* [內容片段編輯器](/help/sites-cloud/administering/content-fragments/authoring.md) 可透過 [內容片段主控台](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).

  >[!WARNING]
  >
  >新編輯器即會在相同標籤中開啟。 不建議同時開啟兩個編輯器。

* **儲存** 提供對的存取 **儲存並關閉** 選項。

* 三個點(**...**)下拉式清單提供其他動作的存取權：
   * **更新頁面參考**
      * 這會更新任何頁面引用。
   * **[快速發佈](#publishing-and-referencing-a-fragment)**
   * **[管理發佈](#publishing-and-referencing-a-fragment)**

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. -->

## 儲存、關閉和版本 {#save-close-and-versions}

>[!NOTE]
>
>版本也可為 [從時間軸建立、比較和還原](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

編輯器有各種選項：

* **儲存** 和 **儲存並關閉**

   * **儲存** 會儲存最新變更並保留在編輯器中。
   * **儲存並關閉** 將會儲存最新變更並退出編輯器。

  >[!CAUTION]
  >
  >若要編輯內容片段，您需要 [適當的許可權](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 如果您遇到問題，請聯絡您的系統管理員。

  >[!NOTE]
  >
  >在儲存之前，您可以保留在編輯器中進行一系列變更。

  >[!CAUTION]
  >
  >除了僅儲存您的變更，這些動作也會更新任何參考，並確保Dispatcher會依需求排清。 這些變更可能需要一些時間才能處理。 因此，大型/複雜/過載系統可能會受到效能影響。
  >
  >使用時，請牢記此程式 **儲存並關閉** 然後快速重新進入片段編輯器以進行和儲存更多變更。

* **關閉**

  將退出編輯器，而不儲存最新變更（即自上次更新以來進行的變更） **儲存**)。

在編輯您的內容片段時，AEM會自動建立版本，以確保如果您取消變更(使用 **關閉** 而不儲存)：

1. 開啟內容片段以編輯AEM時，會檢查是否存在Cookie型權杖並指出 *編輯工作階段* 存在：

   1. 如果找到Token，則會將片段視為現有編輯工作階段的一部分。
   2. 如果代號為 *非* 可使用且使用者開始編輯內容，接著會建立版本，並將此新編輯工作階段的Token傳送至使用者端，並儲存在Cookie中。

2. 當有 *主要* 編輯工作階段，正在編輯的內容每600秒自動儲存一次（預設）。

   >[!NOTE]
   >
   >自動儲存間隔可使用以下設定 `/conf` 機制。
   >
   >預設值，請參閱：
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. 如果使用者取消編輯，則會還原在編輯工作階段開始時建立的版本，並移除Token以結束編輯工作階段。
4. 如果使用者選擇 **儲存** 會保留編輯、更新的元素/變數並移除Token以結束編輯工作階段。

## 編輯片段的內容 {#editing-the-content-of-your-fragment}

開啟片段後，您可以使用 [變數](/help/assets/content-fragments/content-fragments-variations.md) 標籤以編寫您的內容。

## 建立和管理片段中的變數 {#creating-and-managing-variations-within-your-fragment}

建立主要內容後，您就可以建立和管理 [變數](/help/assets/content-fragments/content-fragments-variations.md) 內容的。

## 將內容與片段建立關聯 {#associating-content-with-your-fragment}

您也可以 [關聯內容](/help/assets/content-fragments/content-fragments-assoc-content.md) 含片段。 這提供了連線，以便在將資產（即影像）新增到內容頁面時，可以（選擇性）與片段搭配使用。

## 檢視和編輯片段的中繼資料（屬性） {#viewing-and-editing-the-metadata-properties-of-your-fragment}

您可以使用檢視和編輯片段的屬性。 [中繼資料](/help/assets/content-fragments/content-fragments-metadata.md) 標籤。

## 內容片段的時間軸 {#timeline-for-content-fragments}

除了標準選項外， [時間表](/help/assets/manage-digital-assets.md#timeline) 提供內容片段的特定資訊和動作：

* 檢視有關版本、註釋和註解的資訊
* 版本動作

   * **[還原為此版本](#reverting-to-a-version)** （選取現有片段，然後選取特定版本）

   * **[與目前專案比較](#comparing-fragment-versions)** （選取現有片段，然後選取特定版本）

   * 新增 **標籤** 和/或 **註解** （選取現有片段，然後選取特定版本）

   * **另存為版本** （選取現有片段，然後選取時間軸底部的向上箭頭）

* 註解動作

   * **刪除**

>[!NOTE]
>
>註解包括：
>
>* 所有資產的標準功能
>* 在時間軸中製作
>* 與片段資產相關
>
>註解（適用於內容片段）包括：
>
>* 在片段編輯器中輸入
>* 特定於片段中選取的文字區段
>

例如：

![時間表](assets/cfm-managing-05.png)

## 比較片段版本 {#comparing-fragment-versions}

此 **與目前專案比較** 動作可從 [時間表](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) 在您選取特定版本之後。

這將會開啟：

* 此 **目前** （最新）版本（左）

* 選取的版本 **v&lt;*x.y*>** （右）

它們會並排顯示，其中：

* 任何差異都會反白顯示

   * 刪除的文字 — 紅色
   * 插入的文字 — 綠色
   * 取代的文字 — 藍色

* 全熒幕圖示可讓您自行開啟任一版本，然後切換回平行檢視
* 您可以 **回覆** 至特定版本
* **完成** 將帶您返回主控台

>[!NOTE]
>
>比較片段時無法編輯片段內容。

![比較變數](assets/cfm-managing-06.png)

## 回覆至某個版本  {#reverting-to-a-version}

您可以還原到片段的特定版本：

* 直接從 [時間表](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

  選取所需的版本，然後 **還原為此版本** 動作。

* 當 [比較版本與目前版本](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) 您可以 **回覆** 至選取的版本。

## 發佈和參考片段 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>如果您的片段以模型為基礎，則您應確保 [模型已發佈](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
>如果您發佈的內容片段尚未發佈模型，選擇清單會指出這一點，模型會與片段一起發佈。

必須發佈內容片段才能在發佈環境中使用。 這是使用標準資產功能來完成：

* [快速發佈](/help/assets/manage-publication.md#quick-publish)
* [管理發佈](/help/assets/manage-publication.md#manage-publication)

此檔案可存取：

* 建立後；使用 [Assets控制檯中的可用動作](#actions-for-a-content-fragment-assets-console).
* 從 [內容片段編輯器](#toolbar-actions-in-the-content-fragment-editor).

此外，當您 [發佈使用片段的頁面](/help/sites-cloud/authoring/fragments/content-fragments.md#publishing)；片段會列在頁面參考中。

>[!CAUTION]
>
>片段發佈和/或參考後，當作者再次開啟片段進行編輯時，AEM會顯示警告。 這是為了警告，片段的變更也會影響參照的頁面。

## 刪除片段 {#deleting-a-fragment}

若要刪除片段：

1. 在 **資產** 主控台導覽至內容片段的位置。
2. 選取片段。

   >[!NOTE]
   >
   >此 **刪除** 動作無法當作快速動作使用。

3. 選取 **刪除** 工具列中的。
4. 確認 **刪除** 動作。

   >[!CAUTION]
   >
   >如果片段已在頁面中參考，您會看到警告訊息，並需要確認您要繼續執行強制刪 **除**。片段及其內容片段元件會從任何內容頁面中刪除。

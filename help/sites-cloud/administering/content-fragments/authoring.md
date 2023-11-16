---
title: 編寫內容片段
description: 瞭解如何為內容片段製作內容，然後根據用途建立該內容的變體。 這為Headless傳送和頁面製作增加了靈活性。
feature: Content Fragments
role: User, Developer, Architect
exl-id: a2f2b617-3bdf-4a22-ab64-95f2c65adc82
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '2252'
ht-degree: 7%

---

# 編寫內容片段 {#authoring-content-fragments}

編寫您的內容片段時同時注重Headless傳送和頁面編寫。

有兩個編輯器可用於內容片段。 本節所述的編輯器：

* 已針對headless內容傳送開發（儘管可用於所有情境）
* 可從以下網址取得： **內容片段** 主控台

此編輯器提供：

* [自動儲存](#saving-autosaving)，以防止編輯意外遺失。
* [以內容參考的方式內嵌上傳資產](#reference-images)，無需先將它們上傳至資產DAM。
* [預覽](#preview-content-fragment) 內容片段提供的呈現體驗數量。
* 能夠 [發佈](#publish-content-fragment) 和 [取消發佈](#unpublish-content-fragment) 從編輯器中。
* 能夠 [檢視並開啟相關的語言副本](#view-language-copies) 在編輯器中。
* 能夠 [檢視版本詳細資料](#view-version-history) 在編輯器中。 您也可以還原至選取的版本。
* 能夠 [檢視和開啟父參照](#view-parent-references).
* 內容片段及其參考的階層式檢視，使用 [樹狀結構](#structure-tree).

>[!WARNING]
>
>本節所述的編輯器為 *僅限* 可在 *線上* Adobe Experience Manager (AEM)as a Cloud Service。

## 內容片段編輯器 {#content-fragment-editor}

第一次開啟內容片段編輯器時，您會看到四個主要區域：

* 頂端工具列：用於關鍵資訊和動作
   * 內容片段主控台的連結 (首頁圖示)
   * 有關模型和檔案夾的資訊
   * 連結至 [預覽（如果為模型設定了「預設預覽URL模式」）](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-fragment-model-properties)
   * [發佈](#publish-content-fragment)、和 [取消發佈](#unpublish-content-fragment) 動作
   * 顯示全部&#x200B;**父參考內容**&#x200B;的選項 (連結圖示)
   * **[狀態](/help/sites-cloud/administering/content-fragments/managing.md#statuses-content-fragments)**&#x200B;片段，以及最後儲存的資訊
   * 用來切換至原始 (以資產為主) 編輯器的切換開關

     >[!WARNING]
     >
     >原始編輯器會在相同標籤中開啟。 不建議同時開啟兩個編輯器。

* 左面板：顯示內容片段的&#x200B;**[變數](#variations)**&#x200B;及其&#x200B;**欄位**：
   * 這些連結可用於 [導覽內容片段結構](#navigate-structure)
* 右側面板：顯示索引標籤 [顯示屬性（中繼資料）和標籤](#view-properties-tags)，此資訊關於 [版本記錄](#view-version-history)，以及與任何專案相關的資訊 [語言副本](#view-language-copies)
   * 在「**屬性**」標籤中，您可以更新片段的「**標題**」和「**說明**」，或者更新「**變數**」
* 中央面板：顯示所選變數的實際欄位和內容
   * 允許您編輯內容
   * 如果「**標籤預留位置**」欄位是在此處所示模型中定義，那麼這些欄位可用於導覽；它們會水準顯示或作為下拉式清單顯示

![內容片段編輯器 — 概觀](assets/cf-authoring-overview.png)

## 導覽內容片段結構 {#navigate-structure}

單一內容片段；

* 包含兩個層級：

   * **[變數](#variations)** 內容片段的
   * **欄位**  — 由內容片段模型定義，並供每個變數使用

* 可以包含各種參照。

### 變數和欄位 {#variations-and-fields}

在左側面板中，您可以看到：

* 清單 **[變數](#variations)** 已針對此片段建立的：
   * **主要** 是最初建立內容片段時顯示的變數，您稍後可以新增其他變數
   * 您可以選取並開啟變數進行編輯
   * 您也可以 [建立變數](#create-variation)
* 此 **欄位** 在片段及其變數內：
   * 圖示會指出 [資料型別](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)
   * 文字是欄位名稱
   * 這些共同提供了中央面板中欄位內容的直接連結（適用於目前的變數）

### 追蹤連結 {#follow-links}

在編輯器的各個部分中，您可以看到連結圖示。 這可用來開啟顯示的專案；例如內容片段模型、父參考或正在參考的片段：

![內容片段編輯器 — 連結圖示](assets/cf-authoring-link-icon.png)

### 樹狀結構 {#structure-tree}

開啟 **樹狀結構** 標籤以顯示內容片段的階層結構及其參考。 使用連結圖示導覽至參照。

![內容片段編輯器 — 結構樹](assets/cf-authoring-structure-tree.png)

>[!NOTE]
>
>另請參閱 [分析內容片段結構 — 結構樹](/help/sites-cloud/administering/content-fragments/analysis.md#structure-tree) 以取得更多詳細資料。

## 儲存和自動儲存 {#saving-autosaving}

<!-- CHECK: cannot be saved, no undo, redo -->

每次進行更新後，內容片段都會自動儲存。 上次儲存的時間會顯示在頂端工具列中。

## 變化 {#variations}

[變數](/help/sites-cloud/administering/content-fragments/overview.md#main-and-variations) 是AEM內容片段的一項重要功能。 它們可讓您建立並編輯 **主要** 用於特定頻道和情境的內容，讓headless內容傳送和頁面製作更加靈活。

從編輯器中，您可以：

* [建立變數](#create-variation) 的 **主要** 內容

* 選取編輯內容所需的變數

* [重新命名變數](#rename-variation)

* [刪除變數](#delete-variation)

### 建立變數 {#create-variation}

若要建立內容片段的變數：

1. 在左側面板中，選取 **加號** (**建立變數**)的右側 **變數**.

   >[!NOTE]
   >
   >建立第一個變數後，現有的變數將會列在相同面板中。

   ![內容片段編輯器 — 建立您的第一個變數](assets/cf-authoring-create-variation-01.png)

1. 在對話方塊中，輸入 **標題** ，以及 **說明** 如有需要：

   ![內容片段編輯器 — 「建立變數」對話方塊](assets/cf-authoring-create-variation-02.png)

1. **建立** 變數。 它會出現在清單中。

### 重新命名變數 {#rename-variation}

若要重新命名 **變數**：

1. 選取所需的變數。

1. 開啟 **屬性** 標籤。

1. 更新變數 **標題**.

1. 按下 **傳回** 或移至另一個欄位以自動儲存變更。 標題會在 **變數** 面板顯示。


### 刪除變數 {#delete-variation}

若要刪除內容片段的變數：

>[!NOTE]
>
>您無法刪除 **主要**.

1. 選取變數。

1. 在 **變數** 面板，選取刪除圖示（垃圾桶）：

   ![內容片段編輯器 — 刪除變數圖示](assets/cf-authoring-delete-variation.png)

1. 對話方塊隨即開啟。 選取 **刪除** 以確認動作。

## 編輯多行文字欄位 — 純文字或Markdown {#edit-multi-line-text-fields-plaintext-markdown}

**[多行文字](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)** 欄位可以有下列三種格式之一：

* 純文字
* [Markdown](/help/sites-cloud/administering/content-fragments/markdown.md)
* [RTF](#edit-multi-line-text-fields-rich-text)

定義為純文字或Markdown的欄位具有簡單的文字方塊，不含（熒幕上）格式選項：

![內容片段編輯器 — 多行文字 — 全熒幕](assets/cf-authoring-multilinetext-plaintext-markdown.png)

## 編輯多行文字欄位 — Rtf {#edit-multi-line-text-fields-rich-text}

的 **[多行文字](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)** 定義為 **RTF文字**，提供各種功能：

* 編輯內容：
   * 還原/取消復原
   * 貼上/貼上成文字
   * 複製
   * 選取段落格式
   * 建立/管理表格
   * 文字格式；粗體、斜體、底線、顏色
   * 設定段落對齊方式
   * 建立/管理清單；專案符號、編號
   * 縮排文字；減少、增加
   * 清除目前的格式
   * 插入連結
   * 選取並插入影像資產的參照
   * 新增特殊字元
* [全熒幕編輯器](#full-screen-editor-rich-text)  — 在全熒幕和流量之間切換
* [統計資料](#statistics-rich-text)
* [比較與同步](#compare-and-synchronize-rich-text)

例如：

![內容片段編輯器 — 多行文字 — 全熒幕切換](assets/cf-authoring-multilinetext-fullscreen-toggle.png)

>[!NOTE]
>
>多行文字欄位也由適當的欄位表示 [圖示](#fields-datatypes-icons) 在 **欄位** 面板。

### 全熒幕編輯器 — RTF {#full-screen-editor-rich-text}

全熒幕編輯器提供與內嵌相同的編輯選項，但提供更多空間給文字。

例如：

![內容片段編輯器 — 多行文字 — 全熒幕](assets/cf-authoring-multilinetext-fullscreen.png)

### 統計資料 — RTF文字 {#statistics-rich-text}

動作 **統計資料** 在多行欄位中顯示一系列文字相關資訊。

例如：

![內容片段編輯器 — 統計資料](assets/cf-authoring-multilinetext-statistics.png)

### 比較和同步 — RTF {#compare-and-synchronize-rich-text}

動作 **比較** 當您有多行欄位時，可使用 **變數** 開啟。

這會在全熒幕中開啟多行欄位，並且：

* 顯示兩者的內容 **主要** 和目前的 **變數** 同時，會強調任何差異

* 差異以顏色表示：

   * 綠色表示已新增內容（至變數）
   * 紅色表示內容已移除（從變數中）
   * 藍色表示取代的文字

* 提供 **同步** 動作，會從以下位置同步內容： **主要** 至目前的變數

   * 如果 **主要** 已更新，則這些變更將會轉移至變數
   * 如果已更新變數，則這些變更將由以下變數的內容覆寫： **主要**

  >[!CAUTION]
  >
  >同步僅可用於複製變更 *從&#x200B;**主要**至變數*.
  >
  >正在傳輸變更 *從變數到&#x200B;**主要*** 不提供選項。

例如，案例中的變化內容已完全重寫，因此同步將會以來自的內容取代該新內容 **主要**：

![內容片段編輯器 — 比較和同步](assets/cf-authoring-multilinetext-compare.png)

## 管理引用 {#manage-references}

### 片段參考 {#fragment-references}

[片段參考](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#fragment-reference-nested-fragments) 可用於：

* [建立現有內容片段的參考](#create-reference-existing-content-fragment)
* [建立內容片段，然後參考它](#create-reference-content-fragment)

#### 建立現有內容片段的參考 {#create-reference-existing-content-fragment}

若要建立現有內容片段的參考：

1. 選取欄位。
1. 選取 **新增現有片段**.
1. 從片段選擇器中選取所需的片段。

   >[!NOTE]
   >
   >您一次只能選取一個片段。

#### 建立內容片段和參考 {#create-reference-content-fragment}

或者，您可以 [選取 **建立新片段** 以開啟 **建立** 對話方塊](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment). 建立後，將參考此片段。

### 內容參考 {#content-references}

[內容參照](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference) 用於參考其他AEM內容型別，例如影像、頁面和體驗片段。

#### 參考影像 {#reference-images}

在 **內容參考** 欄位您可以：

* 已存在於存放庫中的參考資產
* 將它們直接上傳到欄位；這樣就不需要使用 **資產** 要上傳的主控台

  >[!NOTE]
  >
  >若要直接將影像上傳至 **內容參考** 欄位，it **必須**：
  >
  >* 具有 **根路徑** 已定義(在 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#content-reference))。 這會指定影像的儲存位置。
  >* 包含 **影像** 在接受內容型別清單中

若要新增資產，您可以：

* 直接將新的資產檔案（例如，從您的檔案系統）拖放到 **內容參考** 欄位
* 使用 **新增資產** 動作，然後選取 **瀏覽資產** 或 **上傳** 若要開啟適當的選取器以供您使用：

  ![內容片段編輯器 — 新增資產選項](assets/cf-authoring-add-asset-options.png)

#### 參考頁面 {#reference-pages}

若要新增對AEM頁面、體驗片段或其他內容型別的參照：

1. 選取 **新增內容路徑**.

1. 在輸入欄位中新增必要路徑。

1. 確認 **新增**.

### 檢視父參照 {#view-parent-references}

選取頂端工具列中的連結圖示，會開啟所有父參照的清單。

例如：

![內容片段編輯器 — 顯示參考](assets/cf-authoring-show-references-link.png)

隨即開啟一個視窗，列出所有相關參照。 若要開啟參照，請選取名稱或標題，或連結圖示。

例如：

![內容片段編輯器 — 顯示參考](assets/cf-authoring-show-references.png)

## 檢視屬性和標籤 {#view-properties-tags}

在右側面板的屬性標籤中，可檢視屬性（中繼資料）和標籤。 屬性可以是：

* 針對 **內容片段**  — 如果 **主要** 目前已選取
* 針對特定 **變數**

![內容片段編輯器 — 屬性](assets/cf-authoring-properties.png)

### 編輯屬性和標籤 {#edit-properties-tags}

在「屬性」標籤（右側面板）中，您也可以編輯：

* **標題**
* **說明**
* **標籤**：使用下拉式清單或選取範圍對話方塊

  ![內容片段編輯器 — 管理標籤](assets/cf-authoring-edit-tags.png)

### 開啟內容片段模型 {#open-content-fragment-model}

當您有 **主要** 選取後，屬性區段中會顯示基礎內容片段模型的名稱。 選取連結圖示，在單獨的標籤中開啟模型。

例如：

![內容片段編輯器 — 開啟內容片段模型](assets/cf-authoring-open-model.png)

## 檢視版本記錄 {#view-version-history}

在 **版本記錄** 標籤中，會顯示目前和先前版本的詳細資料：

>[!NOTE]
>
>發佈內容片段時會建立新版本。

![內容片段編輯器 — 版本記錄概觀](assets/cf-authoring-version-history-overview.png)

### 還原為版本 {#revert-version}

您可以還原成任何版本。

還原至特定版本：

1. 選取版本旁的三點圖示。

1. 選取 **回覆**.

![內容片段編輯器 — 版本記錄回覆](assets/cf-authoring-version-history-revert.png)

## 檢視語言副本 {#view-language-copies}

在 **語言屬性** 任何相關語言副本的標籤詳細資訊都會顯示。 選取連結圖示，即可在個別標籤中開啟副本。

例如：

![內容片段編輯器 — 開啟語言副本](assets/cf-authoring-open-language-copies.png)

>[!NOTE]
>
>如需有關翻譯內容片段和建立語言副本的詳細資訊，請參閱 [AEM Headless翻譯歷程](/help/journey-headless/translation/overview.md).


## 預覽您的片段 {#preview-content-fragment}

內容片段編輯器為作者提供在外部前端應用程式中預覽其編輯的選項。

若要使用此功能，您首先需要：

* 與您的IT團隊合作，設定外部前端應用程式，該應用程式會透過使用其JSON輸出來呈現內容片段。
* 設定外部前端應用程式後， **預設預覽URL模式** 需要定義為 [適當內容片段模型的屬性](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties).

定義URL後， **預覽** 按鈕作用中。 您可以選取此按鈕來啟動外部應用程式（在單獨的索引標籤中）以呈現內容片段。

## 發佈您的片段 {#publish-content-fragment}

您可以 **發佈** 您的片段成為：

* 預覽例項
* 發佈執行個體

您可以從編輯器或控制檯發佈您的片段。 另請參閱 [發佈和預覽片段](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) 以取得完整詳細資訊。

## 取消發佈您的片段 {#unpublish-content-fragment}

您也可以 **取消發佈** 您的片段，來自：

* 預覽例項
* 發佈執行個體

您可以從編輯器或控制檯取消發佈您的片段。 另請參閱 [取消發佈片段](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) 以取得完整詳細資訊。

## 欄位、資料型別和圖示 {#fields-datatypes-icons}

此 **欄位** 面板會列出內容片段中的所有欄位。 圖示會指出 **[資料型別](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)**：

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><p><b>單行文字</b></p> </td>
   <td><p> <img src="assets/cf-authoring-single-line-text-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>多行文字</b></p> </td>
   <td><p> <img src="assets/cf-authoring-multi-line-text-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>數字</b></p> </td>
   <td><p> <img src="assets/cf-authoring-number-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>布林值</b></p> </td>
   <td><p> <img src="assets/cf-authoring-boolean-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>日期和時間</b></p> </td>
   <td><p> <img src="assets/cf-authoring-date-time-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>列舉</b></p> </td>
   <td><p> <img src="assets/cf-authoring-enumeration-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>標記</b></p> </td>
   <td><p> <img src="assets/cf-authoring-tags-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>內容參考</b></p> </td>
   <td><p> <img src="assets/cf-authoring-content-reference-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>片段參考</b></p> </td>
   <td><p> <img src="assets/cf-authoring-fragment-reference-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>JSON 物件</b></p> </td>
   <td><p> <img src="assets/cf-authoring-json-icon.png"> </p></td>
  </tr>
  <tr>
   <td><p><b>標籤預留位置</b></p><p>雖然不是以實際圖示表示，但 <b>索引標籤預留位置</b> 即會顯示在左側面板中。 <br>它也會在中央面板中呈現(水準顯示或下拉式清單（當有太多無法水準顯示時）。</p> </td>
   <td><p> <img src="assets/cf-authoring-tab-icon.png"> </p></td>
  </tr>
 </tbody>
</table>

## 很高興知道 {#good-to-know}

此外：

* 若要編輯內容片段，您需要 [適當的許可權](/help/implementing/developing/extending/content-fragments-customizing.md#asset-permissions). 如果您遇到問題，請聯絡您的系統管理員。

  例如，如果您沒有 `edit` 許可權：編輯器將是唯讀的。

* 內容片段模型通常可以定義資料欄位，名為 **標題** 和 **說明**. 如果這些欄位存在，則為使用者定義的欄位，並且可以在以下欄位中更新： *中央面板* 編輯片段時。

  內容片段及其變化也有稱為的中繼資料欄位（變化屬性） **標題** 和 **說明**. 這些欄位是任何內容片段不可或缺的一部分，並在片段時最初定義。 它們可以在以下位置更新： *右側面板* 編輯片段時。

* 如需詳細資訊，請參閱資產檔案 [原始內容片段編輯器](/help/assets/content-fragments/content-fragments-variations.md)  — 您可透過 **資產** 主控台與 **內容片段** 主控台。

* 您的專案團隊可視需要自訂編輯器。 另請參閱 [自訂內容片段控制檯和編輯器](/help/implementing/developing/extending/content-fragments-console-and-editor.md) 以取得更多詳細資料。

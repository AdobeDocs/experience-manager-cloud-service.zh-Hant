---
title: 變化 - 編寫片段內容
description: 變數可讓您為片段製作內容，然後根據用途建立該內容的變數（如有需要）。
translation-type: tm+mt
source-git-commit: 972d242527871660d55b9a788b9a53e88d020749
workflow-type: tm+mt
source-wordcount: '2186'
ht-degree: 13%

---


# 變化 - 編寫片段內容{#variations-authoring-fragment-content}

[變](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 數是內容片段的重要功能，可讓您建立和編輯主要內容的復本，以用於特定頻道和／或藍本。

從&#x200B;**Valuations**&#x200B;標籤中，您可以：

* [輸入片](#authoring-your-content) 段的內容，
* [建立並管理](#managing-variations) Mastercontent的 **** 變數，

根據正在編輯的資料類型執行一系列其他操作；例如：

* [將視覺資產插入您的片段](#inserting-assets-into-your-fragment) （影像）

* 在[富格文本](#rich-text)、[純文字檔案](#plain-text)和[標籤](#markdown)之間選擇以進行編輯

* [上傳內容](#uploading-content)

* [檢視關鍵統計](#viewing-key-statistics) （關於多行文字）

* [摘要文字](#summarizing-text)

* [使變化與主版內容同步](#synchronizing-with-master)

>[!CAUTION]
>
>發佈和／或參考片段後，當作者開啟片段以進行重新編輯時，AEM會顯示警告。 這會警告對片段所做的變更也會影響參照的頁面。

## 編寫您的內容{#authoring-your-content}

當您開啟內容片段進行編輯時，預設會開啟&#x200B;**Valuations**&#x200B;標籤。 您可以在這裡為「主版」或您擁有的任何變體製作內容。 結構化片段包含在內容模型中定義的各種資料類型的欄位。

您可以：

* 直接在&#x200B;**Valuations**&#x200B;標籤中編輯

   * 每種資料類型提供不同的編輯選項

* 對於&#x200B;**多行文本**&#x200B;欄位，您也可以將[全屏編輯器](#full-screen-editor)開啟為：

   * 選擇[格式](#formats)
   * 檢視更多編輯選項（適用於[Rich Text](#rich-text)格式）
   * 訪問[操作](#actions)的範圍

例如：

![全螢幕編輯器](assets/cfm-variations-02.png)

### 全螢幕編輯器{#full-screen-editor}

編輯多行文字欄位時，可以開啟全螢幕編輯器；點選或按一下實際文字，然後選取下列動作圖示：

![全螢幕編輯器圖示](assets/cfm-variations-03.png)

這將開啟全屏文本編輯器：

![全螢幕編輯器](assets/cfm-variations-fullscreentexteditor.png)

全螢幕文字編輯器提供：

* 存取各種[動作](#actions)
* 視[format](#formats)，其他格式選項([Rich Text](#rich-text))

### 動作 {#actions}

當全螢幕編輯器（即多行文字）開啟時，也可使用下列動作（適用於所有[formats](#formats)）:

* 選擇[format](#formats)([Rich Text](#rich-text)、[Plain Text、](#plain-text)[Markdown](#markdown))

* [上傳內容](#uploading-content)

* [顯示文本統計資訊](#viewing-key-statistics)

* [與主版同步](#synchronizing-with-master) （編輯變數時）

* [摘要文字](#summarizing-text)

### 格式{#formats}

編輯多行文本的選項取決於所選格式：

* [RTF](#rich-text)
* [純文字](#plain-text)
* [Markdown](#markdown)

當全螢幕編輯器時，可選取格式。

### RTF {#rich-text}

豐富式文字編輯可讓您設定格式：

* 粗體
* 斜體
* 底線
* 對齊：左，中，右
* 項目符號清單
* 編號清單
* 縮排：增加，減少
* 建立／中斷超連結
* 貼上文字／從Word
* 插入表格
* 段落樣式：第1/2/3段
* [插入資產](#inserting-assets-into-your-fragment)
* 開啟全螢幕編輯器，其中提供下列格式選項：
   * 搜尋
   * 尋找/取代
   * 拼字檢查器
   * [註解](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [插入內容片段](#inserting-content-fragment-into-your-fragment);當您的「多行」 **文字欄** 位設定為「允許片段 **參考」時可用**。

從全螢幕編輯器也可以存取[actions](#actions)。

### 純文字 {#plain-text}

純文字可讓您快速輸入內容，毋需格式化或標注資訊。 您也可以開啟全螢幕編輯器，以進一步瞭解[actions](#actions)。

>[!CAUTION]
>
>如果您選取「純 **文字** 」 **，可能會遺失您已插入「豐富文字」或「標籤文字」的任何格式、標籤和/或資產******。

### Markdown {#markdown}

>[!NOTE]
>
>如需完整資訊，請參閱[Markdown](/help/assets/content-fragments/content-fragments-markdown.md)檔案。

這可讓您使用標籤下載來格式化文字。 您可以定義：

* 標題
* 段落和分行
* 連結
* 影像
* 塊引號
* 清單
* 強調
* 程式碼區塊
* 反斜線轉義

您也可以開啟全螢幕編輯器，以進一步瞭解[actions](#actions)。

>[!CAUTION]
>
>如果您在 **Rich Text** 和 **** Markdown之間切換，可能會在區塊引號和程式碼區塊中遇到意外的效果，因為這兩種格式在處理方式上可能會有差異。

### 片段參考{#fragment-references}

如果內容片段模型包含片段參考，則您的片段作者可能有其他選項：

* [編輯內容片段](#fragment-references-edit-content-fragment)
* [新內容片段](#fragment-references-new-content-fragment)

![片段參考](assets/cfm-variations-12.png)

#### 編輯內容片段{#fragment-references-edit-content-fragment}

將會開啟「編輯內容片段&#x200B;**」選項
新的瀏覽器標籤，內容片段會在內容片段編輯器中開啟。**

#### 新內容片段 {#fragment-references-new-content-fragment}

選項&#x200B;**新內容片段**&#x200B;可讓您建立全新片段。 為了達到此目的，將在編輯器中開啟建立內容片段嚮導的變化。

然後，您可以通過以下方式建立新片段：

1. 導覽至，並選取所需的檔案夾。
1. 選擇&#x200B;**Next**。
1. 指定屬性；例如&#x200B;**Title**。
1. 選擇&#x200B;**建立**。
1. 最後：
   1. **Donewill** return(to the original fragment) and reference the new fragment.
   1. **Open將** 參考新片段，並在新的瀏覽器標籤中開啟新片段以進行編輯。

### 查看關鍵統計資訊{#viewing-key-statistics}

當全螢幕編輯器開啟時，「文字統計 **資料** 」動作會顯示一系列有關文字的資訊。

例如：

![統計](assets/cfm-variations-04.png)

### 上傳內容{#uploading-content}

若要簡化內容片段的製作程式，您可以上傳在外部編輯器中準備的文字，並直接將它加入片段。

### 摘要文字{#summarizing-text}

摘要文字旨在協助使用者將文字長度縮短為預先定義的字數，同時保留關鍵點和整體意義。

>[!NOTE]
>
>在更技術性的層次上，系統根據特定算法保持其評分的句子，以提供資訊密度和唯一性的&#x200B;*最佳比例。*

>[!CAUTION]
>
>內容片段必須有有效的語言資料夾（ISO程式碼）做為祖先；這可用來決定要使用的語言模型。
>
>例如，`en/`如下列路徑所示：
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
英文是現成可用的。
其他語言則可從Package Share中取得：
* [French(fr)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-fr)
* [German(de)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-de)
* [Italian(it)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-it)
* [Spanish(es)](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/smartcontent-model-es)



1. 選擇&#x200B;**Master**&#x200B;或所需的變化。
1. 開啟全螢幕編輯器。

1. 從工具欄中選擇&#x200B;**摘要文本**。

   ![總結](assets/cfm-variations-05.png)

1. 指定目標字數，然後選擇&#x200B;**開始**:
1. 原始文本與建議的總結並排顯示：

   * 任何要刪除的句子都會以紅色強調顯示，並加上刪除。
   * 按一下任何反白顯示的句子，將它保留在摘要內容中。
   * 按一下任何未反白顯示的句子，即可將其刪除。

1. 選擇&#x200B;**摘要**&#x200B;以確認更改。

1. 原始文本與建議的總結並排顯示：

   * 任何要刪除的句子都會以紅色強調顯示，並加上刪除。
   * 按一下任何反白顯示的句子，將它保留在摘要內容中。
   * 按一下任何未反白顯示的句子，即可將其刪除。

   ![總結比較](assets/cfm-variations-06.png)

### 為內容片段{#annotating-a-content-fragment}加上註解

要注釋片段：

1. 選擇&#x200B;**Master**&#x200B;或所需的變化。

1. 開啟全螢幕編輯器。

1. 頂端工具列提供&#x200B;**Annotate**&#x200B;圖示。 您可以視需要選取一些文字。

   ![註解](assets/cfm-variations-07.png)

1. 對話方塊將會開啟。 您可以在這裡輸入注釋。

   ![註解](assets/cfm-variations-07a.png)

1. 在對話框中選擇&#x200B;**Apply**。

   ![註解](assets/cfm-variations-annotations-apply-icon.png)

   如果注釋已應用到選定文本，則該文本將保持高亮顯示。

   ![註解](assets/cfm-variations-07b.png)

1. 關閉全螢幕編輯器，註解仍會反白顯示。 如果選中此選項，則會開啟一個對話框，以便您能夠進一步編輯注釋。

1. 選擇&#x200B;**保存**。

1. 關閉全螢幕編輯器，註解仍會反白顯示。 如果選中此選項，則會開啟一個對話框，以便您能夠進一步編輯注釋。

   ![註解](assets/cfm-variations-07c.png)

### 查看、編輯、刪除注釋{#viewing-editing-deleting-annotations}

註解:

* 在編輯器的全螢幕和一般模式下，都會以文字上的反白顯示來指示。 然後，只要按一下反白顯示的文字，即可檢視、編輯和／或刪除註解的完整詳細資訊，如此就會重新開啟對話方塊。

   >[!NOTE]
   如果已將多個註解套用至一個文字，則提供下拉式選取器。

* 刪除應用注釋的整個文本時，注釋也會被刪除。

* 通過選擇片段編輯器中的&#x200B;**Annotations**&#x200B;頁籤，可以列出和刪除。

   ![附註](assets/cfm-variations-08.png)

* 可在[時間軸](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)中檢視和刪除所選片段。

### 將資產插入片段{#inserting-assets-into-your-fragment}

若要簡化製作內容片段的程式，您可以直接將[Assets](/help/assets/manage-digital-assets.md)（影像）新增至片段。

這些文字將加到片段的段落序列中，不需任何格式；當頁面](/help/sites-cloud/authoring/fundamentals/content-fragments.md)上使用／參考[片段時，可執行格式設定。

>[!CAUTION]
這些資產無法在參考頁面上移動或刪除，這必須在片段編輯器中完成。
但是，必須在[頁面編輯器](/help/sites-cloud/authoring/fundamentals/content-fragments.md)中完成資產的格式化（例如大小）。 片段編輯器中資產的表示純粹是為了製作內容流程。

>[!NOTE]
有各種方法可將[images](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)新增至片段和／或頁面。

1. 將游標置於要添加影像的位置。
1. 使用「插 **入資產** 」圖示開啟搜尋對話方塊。

   ![插入資產圖示](assets/cfm-variations-09.png)

1. 在對話方塊中，您可以：

   * 導覽至DAM中的必要資產
   * 在DAM中搜尋資產

   找到後，按一下縮圖以選取所需的資產。

1. 使用 **「選取** 」將資產新增至目前位置之內容片段的段落系統。

   >[!CAUTION]
   如果新增資產後，您將格式變更為：
   * **純文字檔案**:資產將完全從碎片中丟失。
   * **Markdown**:資產將不可見，但當您返回 **Rich Text時，資產仍會存在**。


### 將內容片段插入您的片段{#inserting-content-fragment-into-your-fragment}

若要簡化內容片段的製作程式，您也可以將另一個內容片段新增至片段。

它們將作為參考添加到片段的當前位置。

>[!NOTE]
當您的&#x200B;**多行文字**&#x200B;配置了&#x200B;**允許片段參考**&#x200B;時，此選項可用。

>[!CAUTION]
這些資產無法在參考頁面上移動或刪除，這必須在片段編輯器中完成。
但是，必須在[頁面編輯器](/help/sites-cloud/authoring/fundamentals/content-fragments.md)中完成資產的格式化（例如大小）。 片段編輯器中資產的表示純粹是為了製作內容流程。

>[!NOTE]
有各種方法可將[images](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)新增至片段和／或頁面。

1. 將游標置於要添加片段的位置。
1. 使用&#x200B;**插入內容片段**&#x200B;圖示來開啟搜尋對話方塊。

   ![插入內容片段圖示](assets/cfm-variations-13.png)

1. 在對話方塊中，您可以：

   * 導覽至「資產」檔案夾中的必要片段
   * 搜尋片段

   找到後，按一下縮圖以選取所需的片段。

1. 使用&#x200B;**Select**&#x200B;將對所選內容片段的引用添加到當前內容片段（位於當前位置）。

   >[!CAUTION]
   如果在將引用添加到另一個片段後，將格式更改為：
   * **純文字檔案**:這個參考將完全從碎片中遺失。
   * **Markdown**:參考將保留。


## 管理變數{#managing-variations}

### 建立變數{#creating-a-variation}

變化可讓您取用&#x200B;**Master**&#x200B;內容，並視需要加以變更。

要建立新變化，請執行以下操作：

1. 開啟您的片段，並確保側面板可見。
1. 從側面板的表徵圖欄中選擇&#x200B;**Valuations**。
1. 選擇&#x200B;**建立變化**。
1. 將會開啟對話方塊，指定新變 **數的****「標題」(Title)和「說明」(Description** )。
1. 選擇 **添加**;片段 **Master** 將會複製到新的變數，現在會開啟供編 [輯](#editing-a-variation)。

   >[!NOTE]
   建立新變化時，複製的始終是&#x200B;**Master**，而不是當前開啟的變化。

### 編輯變數{#editing-a-variation}

您可以在下列任一項後，變更變更內容：

* [建立變數](#creating-a-variation)。
* 開啟現有片段，然後從側面板選取所需的變數。

![編輯變數](assets/cfm-variations-10.png)

### 更名變數{#renaming-a-variation}

要更名現有變數：

1. 開啟片段，然後從側面板中選擇&#x200B;**Valuations**。
1. 選擇所需的變化。
1. 從&#x200B;**操作**&#x200B;下拉清單中選擇&#x200B;**更名**。

1. 在產生的對 **話方塊中** ，輸入新的「 **** 標題」和/或「說明」。

1. 確認&#x200B;**Rename**&#x200B;動作。

>[!NOTE]
這只會影響變化&#x200B;**Title**。

### 刪除變數{#deleting-a-variation}

要刪除現有變數，請執行以下操作：

1. 開啟片段，然後從側面板中選擇&#x200B;**Valuations**。
1. 選擇所需的變化。
1. 從&#x200B;**操作**&#x200B;下拉清單中選擇&#x200B;**刪除**。

1. 確認對話方塊中的&#x200B;**Delete**&#x200B;動作。

>[!NOTE]
您無法刪除&#x200B;**Master**。

### 與主{#synchronizing-with-master}同步

**** Masteris是內容片段的完整部分，根據定義，它包含內容的主版本，而變數則包含該內容的個別更新及自訂版本。更新主版時，這些更改可能也與變化有關，因此需要傳播到它們。

在編輯變數時，您可以存取動作，以便將變數的目前元素與「主版」同步。 這可讓您自動將對「主版」所做的變更複製到所需的變更。

>[!CAUTION]
同步僅可用於將更改從 *主&#x200B;**版複製**到變化*。
只有變更的當前元素將同步。
同步只適用於多 **行文本** -資料類型。
將變 *更從變更傳輸&#x200B;**至Master*** ，不提供選項。

1. 在片段編輯器中開啟您的內容片段。 確保&#x200B;**Master**&#x200B;已編輯。

1. 選擇特定的變化，然後從以下任一項中選擇適當的同步操作：

   * **動作**&#x200B;下拉式選取器- **與master**&#x200B;同步目前元素

      ![與主版同步](assets/cfm-variations-11a.png)

   * 全螢幕編輯器的工具列- **與master**&#x200B;同步

      ![與主版同步](assets/cfm-variations-11b.png)

1. 主版和變數會並排顯示：

   * 綠色表示已新增（至變數）的內容
   * 紅色表示內容已移除（從變數中）
   * 藍色表示已取代的文字

   ![與主版同步](assets/cfm-variations-11c.png)

1. 選擇&#x200B;**同步**，將更新並顯示變化。

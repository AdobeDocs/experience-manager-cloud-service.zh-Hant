---
title: 搜尋
description: 透過完整的搜尋更快找到您的內容
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 7%

---

# 搜尋 {#search-feature}

AEM的製作環境提供多種搜尋內容的機制，視資源型別而定。

## 搜尋基本資訊 {#search-basics}

可從頂端工具列使用搜尋：

![搜尋圖示](/help/sites-cloud/authoring/assets/search-icon.png)

使用搜尋邊欄，您可以：

* 搜尋特定的關鍵字、路徑或標籤
* 根據資源特定條件進行篩選，例如修改日期、頁面狀態、檔案大小等。
* 根據上述條件定義並使用[儲存的搜尋](#saved-searches)

>[!NOTE]
>
>只要看到搜尋邊欄，也可以使用快速鍵`/` （正斜線）叫用搜尋。

## 搜尋和篩選 {#search-and-filter}

若要搜尋並篩選資源：

1. 開啟&#x200B;**搜尋** （使用工具列中的放大鏡）並輸入搜尋字詞。 提出建議並可加以選取：

   ![搜尋字詞](/help/sites-cloud/authoring/assets/search-term.png)

   依預設，搜尋結果僅限於您目前的位置（即主控台和相關資源型別）：

   ![搜尋位置](/help/sites-cloud/authoring/assets/search-term-location.png)

1. 如有必要，您可以移除位置篩選器（在您要移除的篩選器上選取&#x200B;**X**），以搜尋所有主控台/資源型別。
1. 將顯示結果，並根據控制檯和相關資源型別分組。

   您可以選取特定資源（以供後續動作），或透過選取所需的資源型別向下展開；例如，**檢視所有網站**：

   ![搜尋結果](/help/sites-cloud/authoring/assets/search-results.png)

1. 如果您想要進一步向下展開，請選取「邊欄」符號（左上方）以開啟側面板&#x200B;**篩選器和選項**。

   ![邊欄按鈕](/help/sites-cloud/authoring/assets/rail-button.png)

   根據資源型別，搜尋將顯示預先定義的搜尋/篩選條件選項。

   側面板可讓您選取：

   * 已儲存的搜尋
   * 搜尋目錄
   * 標記
   * 搜尋條件，例如修改日期、Publish狀態、即時副本狀態

   >[!NOTE]
   >
   >搜尋條件可能有所不同：
   >
   >* 視您選取的資源型別而定；例如，Assets和Communities條件可理解為專門化。
   >* 您可以自訂執行個體(適用於AEM內的位置)，以作為「搜尋Forms」。

<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![搜尋側面板](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 您也可以新增其他搜尋詞。

1. 使用 **X** (右上方 **** )關閉搜尋。

>[!NOTE]
>
>在搜尋結果中選取專案時，會持續使用搜尋條件。
>
>當您在搜尋結果頁面上選取專案時，當使用瀏覽器返回按鈕後返回搜尋頁面時，搜尋條件會保留。

## 已儲存的搜尋 {#saved-searches}

除了依範圍廣泛的Facet進行搜尋外，您也可以儲存特定的搜尋組態，以供擷取及稍後階段使用：

1. 定義搜尋條件並選取&#x200B;**儲存**。

   ![儲存搜尋](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 指派名稱，然後使用&#x200B;**儲存**&#x200B;確認：

   ![正在儲存名稱為](/help/sites-cloud/authoring/assets/search-save-name.png)的搜尋

1. 您儲存的搜尋可在您下次存取搜尋面板時從選擇器取得：

   ![已儲存搜尋](/help/sites-cloud/authoring/assets/saved-searches.png)

1. 儲存後，您可以：

   * 使用&#x200B;**x** （針對已儲存搜尋的名稱）來開始新的查詢（不會刪除已儲存的搜尋本身）。
   * **編輯已儲存的搜尋**，變更搜尋條件，然後再次&#x200B;**儲存**。

通過選擇保存的搜索並按一下搜索面板底部的「編 **輯保存的搜索** 」(Edit Saved Search)，可以修改保存的搜索。

![正在修改儲存的搜尋](/help/sites-cloud/authoring/assets/saved-searches-modify.png)

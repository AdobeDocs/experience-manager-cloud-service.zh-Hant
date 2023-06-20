---
title: 搜尋
description: 透過完整的搜尋更快找到您的內容
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 8%

---

# 搜尋 {#search-feature}

AEM的製作環境提供多種搜尋內容的機制，視資源型別而定。

## 搜尋基本需知 {#search-basics}

可從頂端工具列搜尋專案：

![搜尋圖示](/help/sites-cloud/authoring/assets/search-icon.png)

您可以使用搜尋邊欄來：

* 搜尋特定的關鍵字、路徑或標籤
* 根據資源特定條件進行篩選，例如修改日期、頁面狀態、檔案大小等。
* 定義並使用 [已儲存的搜尋](#saved-searches)  — 根據上述條件

>[!NOTE]
>
>也可以使用快速鍵叫用搜尋 `/` （正斜線）。

## 搜尋和篩選 {#search-and-filter}

若要搜尋和篩選資源：

1. 開啟 **搜尋** （使用工具列中的放大鏡）並輸入搜尋字詞。 提出建議並可加以選取：

   ![搜尋期限](/help/sites-cloud/authoring/assets/search-term.png)

   依預設，搜尋結果僅限於您目前的位置（即主控台和相關資源型別）：

   ![搜尋位置](/help/sites-cloud/authoring/assets/search-term-location.png)

1. 如有需要，您可以移除位置篩選器(選取 **X** ，以搜尋所有主控台/資源型別。
1. 將顯示結果，並根據控制檯和相關資源型別分組。

   您可以選取特定資源（供後續動作使用），或透過選取所需的資源型別向下展開；例如 **檢視所有網站**：

   ![搜尋結果](/help/sites-cloud/authoring/assets/search-results.png)

1. 如果您想要進一步向下切入，請選取「邊欄」符號（左上方）以開啟側面板 **篩選和選項**.

   ![邊欄按鈕](/help/sites-cloud/authoring/assets/rail-button.png)

   根據資源型別，搜尋將顯示預先定義的搜尋/篩選條件選擇。

   側面板可讓您選取：

   * 已儲存的搜尋
   * 搜尋目錄
   * 標記
   * 搜尋條件，例如修改日期、發佈狀態、即時副本狀態

   >[!NOTE]
   >
   >搜尋條件可能有所不同：
   >
   >* 根據您選取的資源型別，例如Assets和Communities條件具有專業化是可以理解的。
   >* 您可以自訂執行個體(當作「搜尋Forms」) (適用於AEM內的位置)。

<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![搜尋側面板](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 您也可以新增其他搜尋詞。

1. 使用 **X** (右上方 **** )關閉搜尋。

>[!NOTE]
>
>在搜尋結果中選取專案時，搜尋條件會持續存在。
>
>當您在搜尋結果頁面上選取專案時，當使用瀏覽器返回按鈕後返回搜尋頁面時，搜尋條件會保留。

## 已儲存的搜尋 {#saved-searches}

除了依各種Facet進行搜尋外，您也可以儲存特定的搜尋設定以供擷取，並用於後續階段：

1. 定義搜尋條件並選取 **儲存**.

   ![儲存搜尋](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 指派名稱，然後使用 **儲存** 確認：

   ![使用名稱儲存搜尋](/help/sites-cloud/authoring/assets/search-save-name.png)

1. 您下次存取搜尋面板時，可以從選擇器使用已儲存的搜尋：

   ![已儲存搜尋](/help/sites-cloud/authoring/assets/saved-searches.png)

1. 儲存後，您可以：

   * 使用 **x** （針對已儲存搜尋的名稱）以開始新查詢（不會刪除已儲存搜尋本身）。
   * **編輯已儲存的搜尋**，變更搜尋條件，然後 **儲存** 再來一次。

通過選擇保存的搜索並按一下搜索面板底部的「編 **輯保存的搜索** 」(Edit Saved Search)，可以修改保存的搜索。

![修改已儲存的搜尋](/help/sites-cloud/authoring/assets/saved-searches-modify.png)

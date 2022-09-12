---
title: 搜尋
description: 通過全面的搜索更快地查找內容
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 9%

---

# 搜尋 {#search-feature}

AEM的製作環境提供多種搜尋內容的機制，視資源類型而定。

## 搜尋基本知識 {#search-basics}

您可以從頂端工具列使用搜尋功能：

![搜尋圖示](/help/sites-cloud/authoring/assets/search-icon.png)

透過搜尋邊欄，您可以：

* 搜尋特定關鍵字、路徑或標籤
* 根據資源特定條件進行篩選，例如修改的日期、頁面狀態、檔案大小等。
* 定義和使用 [儲存的搜尋](#saved-searches)  — 根據上述准則

>[!NOTE]
>
>也可使用快捷鍵叫用搜尋 `/` （正斜線）。

## 搜尋與篩選 {#search-and-filter}

若要搜尋及篩選資源：

1. 開啟 **搜尋** （在工具列中放大鏡）並輸入您的搜尋詞。 將會提供建議，並可以選取：

   ![搜尋期限](/help/sites-cloud/authoring/assets/search-term.png)

   依預設，搜尋結果將限制在您目前的位置（即主控台和相關資源類型）:

   ![搜尋位置](/help/sites-cloud/authoring/assets/search-term-location.png)

1. 如有需要，您可以移除位置篩選器(選取 **X** 在您要移除的篩選器上)，以搜尋所有主控台/資源類型。
1. 將顯示結果，並根據控制台和相關資源類型分組。

   您可以選擇特定資源（以便執行進一步的操作），或通過選擇所需的資源類型進行細化；例如 **查看所有站點**:

   ![搜尋結果](/help/sites-cloud/authoring/assets/search-results.png)

1. 如果要進一步深入，請選擇「邊欄」符號（左上）以開啟側面板 **篩選器和選項**.

   ![邊欄按鈕](/help/sites-cloud/authoring/assets/rail-button.png)

   根據資源類型，「搜尋」將顯示預先定義的搜尋/篩選條件選項。

   側面板允許您選擇：

   * 已儲存的搜尋
   * 搜索目錄
   * 標記
   * 搜尋條件，例如修改日期、發佈狀態、LiveCopy狀態

   >[!NOTE]
   >
   >搜尋條件可能有所不同：
   >
   >* 視您選取的資源類型而定；例如，資產和社群條件是可理解的專門性。
   >* 您可以自訂搜尋Forms的例項(適合AEM內的位置)。


<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![搜尋端面板](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 您也可以新增其他搜尋詞。

1. 使用 **X** (右上方 **** )關閉搜尋。

>[!NOTE]
>
>在搜尋結果中選取項目時，搜尋條件持續存在。
>
>在搜尋結果頁面上選取項目時，使用瀏覽器返回按鈕後返回搜尋頁面時，搜尋條件仍會保留。

## 已儲存的搜尋 {#saved-searches}

除了按範圍廣泛的Facet進行搜索外，您還可以保存特定搜索配置以便檢索，並在以後階段使用：

1. 定義您的搜尋條件並選取 **儲存**.

   ![儲存搜尋](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 指派名稱，然後使用 **儲存** 若要確認：

   ![以名稱保存搜索](/help/sites-cloud/authoring/assets/search-save-name.png)

1. 下次存取搜尋面板時，您儲存的搜尋將可從選取器使用：

   ![已儲存搜尋](/help/sites-cloud/authoring/assets/saved-searches.png)

1. 儲存後，您可以：

   * 使用 **x** （根據已保存的搜索的名稱）以啟動新查詢（不會刪除已保存的搜索本身）。
   * **編輯保存的搜索**，變更搜尋條件，然後 **儲存** 。

通過選擇保存的搜索並按一下搜索面板底部的「編 **輯保存的搜索** 」(Edit Saved Search)，可以修改保存的搜索。

![修改保存的搜索](/help/sites-cloud/authoring/assets/saved-searches-modify.png)

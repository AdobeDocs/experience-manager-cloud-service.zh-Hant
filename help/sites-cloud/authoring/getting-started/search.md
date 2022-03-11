---
title: 搜尋
description: 通過全面的搜索更快地查找內容
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 8%

---

# 搜尋 {#search-feature}

作者環境提AEM供了各種機制來搜索內容，這取決於資源類型。

## 搜索基礎 {#search-basics}

可從頂部工具欄進行搜索：

![「搜索」表徵圖](/help/sites-cloud/authoring/assets/search-icon.png)

使用搜索欄，您可以：

* 搜索特定關鍵字、路徑或標籤
* 根據資源特定的條件進行篩選，如修改日期、頁面狀態、檔案大小等。
* 定義和使用 [保存的搜索](#saved-searches)  — 根據上述標準

>[!NOTE]
>
>也可以使用熱鍵調用搜索 `/` （正斜線）。

## 搜尋與篩選 {#search-and-filter}

要搜索和篩選資源：

1. 開啟 **搜索** （工具欄中帶有放大鏡）並輸入搜索詞。 將提出建議，並可以選擇：

   ![搜尋期限](/help/sites-cloud/authoring/assets/search-term.png)

   預設情況下，搜索結果將限於當前位置（即控制台和相關資源類型）:

   ![搜索位置](/help/sites-cloud/authoring/assets/search-term-location.png)

1. 如果需要，可以刪除位置篩選器(選擇 **X** 在要刪除的篩選器上)搜索所有控制台/資源類型。
1. 將顯示結果，並根據控制台和相關資源類型進行分組。

   您可以選擇特定資源（用於進一步操作），或通過選擇所需的資源類型進行細化；例如 **查看所有站點**:

   ![搜尋結果](/help/sites-cloud/authoring/assets/search-results.png)

1. 如果要進一步深入，請選擇「軌」符號（左上）以開啟側面板 **篩選器和選項**。

   ![軌道按鈕](/help/sites-cloud/authoring/assets/rail-button.png)

   根據資源類型，「搜索」將顯示預定義的搜索/篩選條件選擇。

   側面板允許您選擇：

   * 已儲存的搜尋
   * 搜索目錄
   * 標記
   * 搜索條件，例如修改日期、發佈狀態、LiveCopy狀態

   >[!NOTE]
   >
   >搜索標準可能會有所不同：
   >
   >* 根據您選擇的資源類型；例如，資產和社區標準是可以理解的專門性。
   >* 您的實例作為「搜索Forms」可以自定義(適合於中的位AEM置)。


<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![搜索側面板](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 您還可以添加其他搜索詞。

1. 使用 **X** (右上方 **** )關閉搜尋。

>[!NOTE]
>
>在搜索結果中選擇項時，將保留搜索條件。
>
>在搜索結果頁面上選擇項目時，當使用「後退瀏覽器」按鈕返回到搜索頁面時，搜索標準將保留。

## 已儲存的搜尋 {#saved-searches}

除了通過各種方面進行搜索外，還可以保存特定搜索配置以在稍後階段進行檢索和使用：

1. 定義搜索條件並選擇 **保存**。

   ![保存搜索](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 指定名稱，然後使用 **保存** 確認：

   ![使用名稱保存搜索](/help/sites-cloud/authoring/assets/search-save-name.png)

1. 下次訪問搜索面板時，您保存的搜索將可從選擇器獲得：

   ![已保存的搜索](/help/sites-cloud/authoring/assets/saved-searches.png)

1. 保存後，您可以：

   * 使用 **x** （根據已保存的搜索的名稱）啟動新查詢（不會刪除已保存的搜索本身）。
   * **編輯保存的搜索**，然後 **保存** 的雙曲餘切值。

通過選擇保存的搜索並按一下搜索面板底部的「編 **輯保存的搜索** 」(Edit Saved Search)，可以修改保存的搜索。

![修改保存的搜索](/help/sites-cloud/authoring/assets/saved-searches-modify.png)

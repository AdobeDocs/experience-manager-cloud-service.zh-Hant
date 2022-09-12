---
title: 如何配置收件箱的搜索篩選器？
description: 了解如何為收件匣項目設定搜尋篩選器。
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# 配置收件箱的搜索篩選器 {#configure-search-filters-inbox}

您可以配置收件箱項的搜索篩選器。 將搜索條件建立在特定收件箱列上，以篩選結果。

例如，要根據「出生收件匣日期」欄範圍來篩選「收件匣」項目，您可以使用「日期範圍」述詞來定義日期範圍。

以下是「收件箱」的可用謂詞類型：

* 範圍述詞

* 文字述詞

* 日期範圍述詞

* 選項屬性述詞

>[!NOTE]
>
>確認您是 `workflow-administrators` 組，以配置收件箱的搜索篩選器。

## 建立或開啟自訂的設定 {#creating-opening-customized-configuration}

1. 導覽至 **[!UICONTROL 工具]**, **[!UICONTROL 一般]**, **[!UICONTROL 搜尋Forms]**.

1. 選取 **[!UICONTROL 收件匣搜尋邊欄]** 設定與點選 **[!UICONTROL 編輯]**.
1. 納入述片語態變更，使用 **[!UICONTROL 編輯搜尋Forms]**.
1. 選擇 **[!UICONTROL 完成]** 以儲存設定。

## 刪除自訂的設定 {#delete-customized-configuration}

要刪除自定義配置：

1. 導覽至 **[!UICONTROL 工具]**, **[!UICONTROL 一般]**, **[!UICONTROL 搜尋Forms]**.

1. 選取 **[!UICONTROL 收件匣搜尋邊欄]** 設定與點選 **[!UICONTROL 刪除]**.

## 設定範圍述詞 {#range-predicate}

您可以使用「範圍述詞」篩選「收件匣」項目，以在「收件匣」欄內搜尋數字範圍。 您也可以選擇包含數字的小數值。

要配置範圍謂語：

1. 開啟 [配置表單](#creating-opening-customized-configuration).
1. 點選 **[!UICONTROL 選擇謂詞]** 標籤和拖曳 **[!UICONTROL 範圍述詞]** 到表單中。
1. 在 **[!UICONTROL 設定]** 頁簽，選擇收件箱列名以進行搜索，從 **[!UICONTROL 欄名稱]** 欄位。
1. 在 **[!UICONTROL 篩選標籤]** 欄位。 選取 **[!UICONTROL 啟用小數值]** 核取方塊，在定義範圍時接受數字的小數值。
1. 指定組態的可選說明，然後點選 **[!UICONTROL 完成]** 來保存它。

開啟「篩選器」頁面時，設定變更會反映。 您在步驟4中指定的篩選標籤會顯示為標籤，並提供定義最大值和最小值的選項。 按Enter鍵時， [!DNL Experience Manager] 對步驟3中指定的列名應用搜索標準並返回收件箱項。

>[!NOTE]
>
>文章列出最新的使用者介面選項。 選項名稱將在即將發行的使用者介面上更新。

## 設定文字述詞 {#text-predicate}

篩選收件匣項目，以使用「文字述詞」在收件匣欄內搜尋文字字串。

要配置文本謂語：

1. 開啟 [配置表單](#creating-opening-customized-configuration).
1. 點選 **[!UICONTROL 選擇謂詞]** 標籤和拖曳 **[!UICONTROL 文字述詞]** 到表單中。
1. 在 **[!UICONTROL 設定]** 頁簽，選擇收件箱列名以進行搜索，從 **[!UICONTROL 欄名稱]** 欄位。
1. 指定在「搜尋」文字方塊中顯示的文字，做為 **[!UICONTROL 搜索文本框佔位符]** 欄位。
1. 指定組態的可選說明，然後點選 **[!UICONTROL 完成]** 來保存它。

開啟「篩選器」頁面時，設定變更會反映。 按Enter鍵時， [!DNL Experience Manager] 對步驟3中指定的列名應用步驟4中指定的搜索文本並返回收件箱項。

## 設定日期範圍述詞 {#date-range-predicate}

您可以使用「日期範圍述詞」篩選「收件匣」項目，以在「收件匣」欄內搜尋日期範圍。

若要設定日期範圍述詞：

1. 開啟 [配置表單](#creating-opening-customized-configuration).
1. 點選 **[!UICONTROL 選擇謂詞]** 標籤和拖曳 **[!UICONTROL 日期範圍述詞]** 到表單中。
1. 在 **[!UICONTROL 設定]** 頁簽，選擇收件箱列名以進行搜索，從 **[!UICONTROL 欄名稱]** 欄位。
1. 在 **[!UICONTROL 篩選標籤]** 欄位。
1. 指定篩選器的開始日期和結束日期標籤。
1. 指定組態的可選說明，然後點選 **[!UICONTROL 完成]** 來保存它。

開啟「篩選器」頁面時，設定變更會反映。 您在步驟4中指定的篩選標籤會顯示為日期範圍篩選的標籤，以及步驟5中指定的開始日期和結束日期標籤。 [!DNL Experience Manager] 對步驟3中指定的列名應用搜索標準並返回收件箱項。

## 配置自定義列選項謂詞 {#custom-column-options-predicate}

您可以使用「自訂欄選項述詞」篩選「收件匣」項目，以在「收件匣」欄內搜尋自訂選項。

要配置自定義列選項謂語：

1. 開啟 [配置表單](#creating-opening-customized-configuration).
1. 點選 **[!UICONTROL 選擇謂詞]** 標籤和拖曳 **[!UICONTROL 自定義列選項謂詞]** 到表單中。
1. 在 **[!UICONTROL 設定]** 頁簽，選擇收件箱列名以進行搜索，從 **[!UICONTROL 欄名稱]** 欄位。
1. 指定自訂欄選項篩選器的標籤，位於 **[!UICONTROL 篩選標籤]** 欄位。
1. 選取 **[!UICONTROL 單選]** 核取方塊，在「收件匣」欄套用篩選時僅啟用選取一個選項。
1. 在 **[!UICONTROL 新增選項]** 小節：
   1. 選擇 **[!UICONTROL 手動]** 來手動定義篩選器搜尋選項。 點選 **[!UICONTROL 新增篩選選項]** 來定義第一個選項。 為要搜索的列選項和選項值文本指定標籤。 例如，如果您要搜尋 **女性** 作為「收件匣」欄中的值，您可以指定 **F** 作為欄選項的標籤，然後新增 **女性** 作為選項值文本。 同樣地，您也可以新增更多篩選選項。
   1. 選擇 **[!UICONTROL JSON路徑]** 使用JSON檔案路徑定義選項。 以下是定義篩選選項的範例JSON檔案：

      ```JSON
          {
         "options":[
            {
            "text":"Female",
            "value":"F"
            },
            {
            "text":"Male",
            "value":"M"
            }
          ]
        }
      ```

   1. 選擇 **[!UICONTROL CRX選項路徑]** 使用CRX儲存庫路徑定義選項。 點選 **[!UICONTROL 新增選項路徑]** 來新增多個路徑。 以下是要定義的範例 `Male` 和 `Female` 篩選選項：

      ```JSON
         <gender jcr:primaryType="sling:OrderedFolder">
                        <male
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Male"
                            value="M"/>
                        <female
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Female"
                            value="F"/>
                    </gender>
      ```

1. 指定組態的可選說明，然後點選 **[!UICONTROL 完成]** 來保存它。

開啟「篩選器」頁面時，設定變更會反映。 您在步驟4中指定的篩選標籤會顯示為「自訂欄選項述詞」的標籤。 [!DNL Experience Manager] 對步驟3中指定的列名應用步驟6中定義的搜索標準並返回收件箱項。

下列影片說明根據 `true` 和 `false` 選項的值。

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## 根據謂語查看搜索篩選器 {#view-search-filters-for-predicates}

您可以根據謂語檢視搜尋篩選器。 選擇 **[!UICONTROL 篩選]** 在「收件箱」頁面上。 篩選器會顯示在左窗格中。 然後，您可以指定搜索條件以篩選收件箱項。

![篩選器頁面](assets/apply-filters.png)

如需管理述詞設定的詳細資訊，請參閱 [設定搜尋Forms](search-forms.md).

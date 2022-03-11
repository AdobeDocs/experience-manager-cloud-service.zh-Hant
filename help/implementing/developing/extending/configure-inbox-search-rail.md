---
title: 如何配置收件箱的搜索篩選器？
description: 瞭解如何為收件箱項配置搜索篩選器。
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# 配置收件箱的搜索篩選器 {#configure-search-filters-inbox}

可以為收件箱項配置搜索篩選器。 將搜索條件基於特定的收件箱列以篩選結果。

例如，要根據「出生日期收件箱」列範圍篩選「收件箱」項，可以使用「日期範圍」謂詞定義日期範圍。

以下是收件箱的可用謂詞類型：

* 範圍述詞

* 文字述詞

* 日期範圍述詞

* 選項屬性述詞

>[!NOTE]
>
>確保您是 `workflow-administrators` 組以配置收件箱的搜索篩選器。

## 建立或開啟自定義配置 {#creating-opening-customized-configuration}

1. 導航到 **[!UICONTROL 工具]**。 **[!UICONTROL 常規]**。 **[!UICONTROL 搜索Forms]**。

1. 選擇 **[!UICONTROL 收件箱搜索欄]** 配置和分路 **[!UICONTROL 編輯]**。
1. 合併謂詞配置更改，使用 **[!UICONTROL 編輯搜索Forms]**。
1. 選擇 **[!UICONTROL 完成]** 的子菜單。

## 刪除自定義配置 {#delete-customized-configuration}

要刪除自定義配置：

1. 導航到 **[!UICONTROL 工具]**。 **[!UICONTROL 常規]**。 **[!UICONTROL 搜索Forms]**。

1. 選擇 **[!UICONTROL 收件箱搜索欄]** 配置和分路 **[!UICONTROL 刪除]**。

## 配置範圍謂詞 {#range-predicate}

您可以使用範圍謂詞篩選收件箱項目，以在收件箱列中搜索數字範圍。 您還可以選擇包括數字的小數值。

要配置範圍謂語，請執行以下操作：

1. 開啟 [配置窗體](#creating-opening-customized-configuration)。
1. 點擊 **[!UICONTROL 選擇謂詞]** 頁籤和拖動 **[!UICONTROL 範圍謂詞]** 的下界。
1. 在 **[!UICONTROL 設定]** 頁籤，選擇「收件箱」列名稱以進行搜索，從 **[!UICONTROL 列名]** 的子菜單。
1. 在中為篩選器指定標籤 **[!UICONTROL 篩選器標籤]** 的子菜單。 選擇 **[!UICONTROL 啟用小數值]** 複選框以在定義範圍時接受數字的小數值。
1. 指定配置和點擊的可選說明 **[!UICONTROL 完成]** 來拯救它。

開啟「篩選器」頁時，配置更改會反映。 在步驟4中指定的篩選器標籤顯示為帶有選項的標籤，以定義最大值和最小值。 按Enter鍵時， [!DNL Experience Manager] 對步驟3中指定的列名應用搜索條件並返回收件箱項。

>[!NOTE]
>
>文章列出了最新的用戶介面選項。 在即將發佈的版本中，將在用戶介面上更新選項名稱。

## 配置文本謂詞 {#text-predicate}

篩選收件箱項，以使用文本謂詞在收件箱列中搜索文本字串。

要配置文本謂詞，請執行以下操作：

1. 開啟 [配置窗體](#creating-opening-customized-configuration)。
1. 點擊 **[!UICONTROL 選擇謂詞]** 頁籤和拖動 **[!UICONTROL 文本謂詞]** 的下界。
1. 在 **[!UICONTROL 設定]** 頁籤，選擇「收件箱」列名稱以進行搜索，從 **[!UICONTROL 列名]** 的子菜單。
1. 指定在「搜索」文本框中顯示的文本作為佔位符文本 **[!UICONTROL 搜索文本框佔位符]** 的子菜單。
1. 指定配置和點擊的可選說明 **[!UICONTROL 完成]** 來拯救它。

開啟「篩選器」頁時，配置更改會反映。 按Enter鍵時， [!DNL Experience Manager] 將步驟4中指定的搜索文本應用於步驟3中指定的列名並返回收件箱項。

## 配置日期範圍謂詞 {#date-range-predicate}

您可以使用「日期範圍謂詞」篩選「收件箱」項目，以在「收件箱」列中搜索日期範圍。

要配置日期範圍謂詞，請執行以下操作：

1. 開啟 [配置窗體](#creating-opening-customized-configuration)。
1. 點擊 **[!UICONTROL 選擇謂詞]** 頁籤和拖動 **[!UICONTROL 日期範圍謂詞]** 的下界。
1. 在 **[!UICONTROL 設定]** 頁籤，選擇「收件箱」列名稱以進行搜索，從 **[!UICONTROL 列名]** 的子菜單。
1. 指定日期範圍篩選器的標籤 **[!UICONTROL 篩選器標籤]** 的子菜單。
1. 指定篩選器的開始日期和結束日期標籤。
1. 指定配置和點擊的可選說明 **[!UICONTROL 完成]** 來拯救它。

開啟「篩選器」頁時，配置更改會反映。 在步驟4中指定的篩選器標籤將作為日期範圍篩選器的標籤以及在步驟5中指定的開始日期和結束日期標籤一起顯示。 [!DNL Experience Manager] 對步驟3中指定的列名應用搜索條件並返回收件箱項。

## 配置自定義列選項謂詞 {#custom-column-options-predicate}

您可以使用「自定義列選項謂詞」篩選收件箱項目，以在「收件箱」列中搜索自定義選項。

要配置自定義列選項謂詞，請執行以下操作：

1. 開啟 [配置窗體](#creating-opening-customized-configuration)。
1. 點擊 **[!UICONTROL 選擇謂詞]** 頁籤和拖動 **[!UICONTROL 自定義列選項謂詞]** 的下界。
1. 在 **[!UICONTROL 設定]** 頁籤，選擇「收件箱」列名稱以進行搜索，從 **[!UICONTROL 列名]** 的子菜單。
1. 在中為自定義列選項篩選器指定標籤 **[!UICONTROL 篩選器標籤]** 的子菜單。
1. 選擇 **[!UICONTROL 單選]** 複選框，以在「收件箱」列上應用篩選器時僅啟用一個選項的選擇。
1. 在 **[!UICONTROL 添加選項]** 部分：
   1. 選擇 **[!UICONTROL 手動]** 來修改選定線條的屬性。 點擊 **[!UICONTROL 添加篩選器選項]** 的子菜單。 指定列選項的標籤和要搜索的選項值文本。 例如，如果要搜索 **女** 作為收件箱列中的值，可以指定 **F** 作為列選項的標籤，然後添加 **女** 選項值文本。 同樣，您可以添加更多篩選器選項。
   1. 選擇 **[!UICONTROL JSON路徑]** 使用JSON檔案路徑定義選項。 以下是定義篩選器選項的示例JSON檔案：

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

   1. 選擇 **[!UICONTROL CRX選項路徑]** 定義選項。 點擊 **[!UICONTROL 添加選項路徑]** 添加多個路徑。 以下是要定義的示例 `Male` 和 `Female` 篩選器選項：

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

1. 指定配置和點擊的可選說明 **[!UICONTROL 完成]** 來拯救它。

開啟「篩選器」頁時，配置更改會反映。 在步驟4中指定的篩選器標籤顯示為自定義列選項謂詞的標籤。 [!DNL Experience Manager] 將步驟6中定義的搜索標準應用於步驟3中指定的列名，並返回收件箱項。

以下視頻說明了根據 `true` 和 `false` 頁籤

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## 基於謂詞查看搜索篩選器 {#view-search-filters-for-predicates}

您可以基於謂詞查看搜索篩選器。 選擇 **[!UICONTROL 篩選]** 的子菜單。 濾鏡顯示在左窗格中。 然後，可以指定搜索條件以篩選收件箱項。

![「篩選器」頁](assets/apply-filters.png)

有關管理謂詞配置的詳細資訊，請參見 [配置搜索Forms](search-forms.md)。

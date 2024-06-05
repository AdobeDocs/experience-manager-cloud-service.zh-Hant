---
title: 如何設定收件匣的搜尋篩選器？
description: 瞭解如何設定收件匣專案的搜尋篩選器。
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 1%

---

# 設定收件匣搜尋篩選器 {#configure-search-filters-inbox}

您可以設定收件匣專案的搜尋篩選器。 依據特定收件匣欄的搜尋條件來篩選結果。

例如，若要根據出生日期收件匣欄範圍來篩選「收件匣」專案，您可以使用日期範圍述詞來定義日期範圍。

以下是收件匣的可用述詞型別：

* 範圍述詞

* 文字述詞

* 日期範圍述詞

* 選項屬性述詞

>[!NOTE]
>
>確定您是 `workflow-administrators` 群組以設定收件匣的搜尋篩選器。

## 建立或開啟自訂設定 {#creating-opening-customized-configuration}

1. 瀏覽至 **[!UICONTROL 工具]**， **[!UICONTROL 一般]**， **[!UICONTROL 搜尋Forms]**.

1. 選取 **[!UICONTROL 收件匣搜尋邊欄]** 設定並選取 **[!UICONTROL 編輯]**.
1. 合併述詞設定變更，使用 **[!UICONTROL 編輯搜尋Forms]**.
1. 選取 **[!UICONTROL 完成]** 以儲存組態。

## 刪除自訂設定 {#delete-customized-configuration}

若要刪除自訂組態：

1. 瀏覽至 **[!UICONTROL 工具]**， **[!UICONTROL 一般]**， **[!UICONTROL 搜尋Forms]**.

1. 選取 **[!UICONTROL 收件匣搜尋邊欄]** 設定並選取 **[!UICONTROL 刪除]**.

## 設定範圍述詞 {#range-predicate}

您可以使用「範圍述詞」來篩選「收件匣」專案，以在「收件匣」欄中搜尋數字範圍。 您也可以選擇包含數字的小數值。

設定範圍述詞：

1. 開啟 [設定表單](#creating-opening-customized-configuration).
1. 選取 **[!UICONTROL 選取述詞]** 定位並拖曳 **[!UICONTROL 範圍述詞]** 至表單。
1. 在 **[!UICONTROL 設定]** 索引標籤中，選取作為搜尋基礎的收件匣欄名稱 **[!UICONTROL 欄名稱]** 欄位。
1. 在中指定篩選的標籤 **[!UICONTROL 篩選標籤]** 欄位。 選取 **[!UICONTROL 啟用十進位值]** 核取方塊，以在定義範圍時接受數字的小數值。
1. 指定組態的選擇性說明，然後選取 **[!UICONTROL 完成]** 以儲存。

當您開啟「篩選器」頁面時，會反映組態變更。 您在步驟4中指定的篩選標籤會顯示為標籤，並附上定義最大值和最小值的選項。 當您按下Enter鍵時， [!DNL Experience Manager] 將搜尋條件套用至步驟3中指定的欄名稱，並傳回「收件匣」專案。

>[!NOTE]
>
>本文列出最新的使用者介面選項。 選項名稱會在即將發行的版本的使用者介面上更新。

## 設定文字述詞 {#text-predicate}

篩選收件匣專案，以使用文字述詞在收件匣欄中搜尋文字字串。

設定文字述詞：

1. 開啟 [設定表單](#creating-opening-customized-configuration).
1. 選取 **[!UICONTROL 選取述詞]** 定位並拖曳 **[!UICONTROL 文字述詞]** 至表單。
1. 在 **[!UICONTROL 設定]** 索引標籤中，選取作為搜尋基礎的收件匣欄名稱 **[!UICONTROL 欄名稱]** 欄位。
1. 指定在「搜尋」文字方塊中顯示的文字，作為 **[!UICONTROL 搜尋文字方塊預留位置]** 欄位。
1. 指定組態的選擇性說明，然後選取 **[!UICONTROL 完成]** 以儲存。

當您開啟「篩選器」頁面時，會反映組態變更。 當您按下Enter鍵時， [!DNL Experience Manager] 將步驟4中指定的搜尋文字套用至步驟3中指定的欄名稱，並傳回收件匣專案。

## 設定日期範圍述詞 {#date-range-predicate}

您可以篩選收件匣專案，以使用日期範圍述詞在收件匣欄中搜尋日期範圍。

設定日期範圍述詞：

1. 開啟 [設定表單](#creating-opening-customized-configuration).
1. 選取 **[!UICONTROL 選取述詞]** 定位並拖曳 **[!UICONTROL 日期範圍述詞]** 至表單。
1. 在 **[!UICONTROL 設定]** 索引標籤中，選取作為搜尋基礎的收件匣欄名稱 **[!UICONTROL 欄名稱]** 欄位。
1. 在「 」中指定日期範圍篩選的標籤 **[!UICONTROL 篩選標籤]** 欄位。
1. 指定篩選的開始日期和結束日期標籤。
1. 指定組態的選擇性說明，然後選取 **[!UICONTROL 完成]** 以儲存。

當您開啟「篩選器」頁面時，會反映組態變更。 您在步驟4中指定的篩選標籤，連同步驟5中指定的開始日期和結束日期標籤，顯示為日期範圍篩選的標籤。 [!DNL Experience Manager] 將搜尋條件套用至步驟3中指定的欄名稱，並傳回「收件匣」專案。

## 設定自訂欄選項述詞 {#custom-column-options-predicate}

您可以使用自訂欄選項述詞來篩選收件匣專案，以搜尋收件匣欄中的自訂選項。

設定自訂欄選項述詞：

1. 開啟 [設定表單](#creating-opening-customized-configuration).
1. 選取 **[!UICONTROL 選取述詞]** 定位並拖曳 **[!UICONTROL 自訂欄選項述詞]** 至表單。
1. 在 **[!UICONTROL 設定]** 索引標籤中，選取作為搜尋基礎的收件匣欄名稱 **[!UICONTROL 欄名稱]** 欄位。
1. 在中指定自訂欄選項篩選器的標籤 **[!UICONTROL 篩選標籤]** 欄位。
1. 選取 **[!UICONTROL 單選]** 核取方塊，啟用在收件匣欄套用篩選器時只選取一個選項。
1. 在 **[!UICONTROL 新增選項]** 區段：
   1. 選取 **[!UICONTROL 手動]** 以手動定義篩選器搜尋選項。 選取 **[!UICONTROL 新增篩選器選項]** 以定義第一個選項。 指定欄選項的標籤和要搜尋的選項值文字。 例如，如果要搜尋 **女性** 作為「收件匣」欄中的值，您可以指定 **F** 作為欄選項的標籤並新增 **女性** 作為選項值文字。 同樣地，您可以新增更多篩選器選項。
   1. 選取 **[!UICONTROL JSON路徑]** 以使用JSON檔案路徑來定義選項。 以下是可定義篩選選項的JSON檔案範例：

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

   1. 選取 **[!UICONTROL CRX選項路徑]** 以使用CRX存放庫路徑來定義選項。 選取 **[!UICONTROL 新增選項路徑]** 以新增多個路徑。 以下為要定義的範例 `Male` 和 `Female` 篩選器選項：

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

1. 指定組態的選擇性說明，然後選取 **[!UICONTROL 完成]** 以儲存。

當您開啟「篩選器」頁面時，會反映組態變更。 您在步驟4中指定的篩選器標籤會顯示為「自訂欄選項」述詞的標籤。 [!DNL Experience Manager] 將步驟6中定義的搜尋條件套用至步驟3中指定的欄名稱，並傳回收件匣專案。

以下影片說明根據頁面篩選欄的步驟。 `true` 和 `false` 選項值。

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## 根據述詞檢視搜尋篩選器 {#view-search-filters-for-predicates}

您可以檢視根據述詞的搜尋篩選器。 選取 **[!UICONTROL 篩選]** 在「收件匣」頁面上。 這些篩選器會顯示在左窗格中。 然後，您可以指定搜尋條件以篩選收件匣專案。

![篩選器頁面](assets/apply-filters.png)

如需有關管理述詞設定的詳細資訊，請參閱 [設定搜尋Forms](search-forms.md).

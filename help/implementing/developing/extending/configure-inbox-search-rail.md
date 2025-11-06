---
title: 如何設定收件匣的搜尋篩選器？
description: 瞭解如何設定收件匣專案的搜尋篩選器。
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
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
>確定您是`workflow-administrators`群組的成員，以便設定收件匣的搜尋篩選器。

## 建立或開啟自訂設定 {#creating-opening-customized-configuration}

1. 導覽至&#x200B;**[!UICONTROL 工具]**、**[!UICONTROL 一般]**、**[!UICONTROL 搜尋Forms]**。

1. 選取&#x200B;**[!UICONTROL 收件匣搜尋邊欄]**&#x200B;設定，然後選取&#x200B;**[!UICONTROL 編輯]**。
1. 使用&#x200B;**[!UICONTROL 編輯搜尋Forms]**&#x200B;合併述片語態變更。
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存組態。

## 刪除自訂設定 {#delete-customized-configuration}

若要刪除自訂組態：

1. 導覽至&#x200B;**[!UICONTROL 工具]**、**[!UICONTROL 一般]**、**[!UICONTROL 搜尋Forms]**。

1. 選取&#x200B;**[!UICONTROL 收件匣搜尋邊欄]**&#x200B;設定，然後選取&#x200B;**[!UICONTROL 刪除]**。

## 設定範圍述詞 {#range-predicate}

您可以使用「範圍述詞」來篩選「收件匣」專案，以在「收件匣」欄中搜尋數字範圍。 您也可以選擇包含數字的小數值。

設定範圍述詞：

1. 開啟組態[的](#creating-opening-customized-configuration)表單。
1. 選取&#x200B;**[!UICONTROL 選取述詞]**&#x200B;索引標籤，並將&#x200B;**[!UICONTROL 範圍述詞]**&#x200B;拖曳至表單。
1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中，從&#x200B;**[!UICONTROL 欄名稱]**&#x200B;欄位選取搜尋所依據的收件匣欄名稱。
1. 在&#x200B;**[!UICONTROL 篩選器標籤]**&#x200B;欄位中指定篩選的標籤。 選取&#x200B;**[!UICONTROL 啟用小數值]**&#x200B;核取方塊，以在定義範圍時接受數字的小數值。
1. 指定組態的選擇性描述，並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存。

當您開啟「篩選器」頁面時，會反映組態變更。 您在步驟4中指定的篩選標籤會顯示為標籤，並附上定義最大值和最小值的選項。 當您按下Enter鍵時，[!DNL Experience Manager]會在步驟3中指定的欄名稱上套用搜尋准則，並傳回收件匣專案。

>[!NOTE]
>
>本文列出最新的使用者介面選項。 選項名稱會在即將發行的版本的使用者介面上更新。

## 設定文字述詞 {#text-predicate}

篩選收件匣專案，以使用文字述詞在收件匣欄中搜尋文字字串。

設定文字述詞：

1. 開啟組態[的](#creating-opening-customized-configuration)表單。
1. 選取&#x200B;**[!UICONTROL 選取述詞]**&#x200B;索引標籤，並將&#x200B;**[!UICONTROL 文字述詞]**&#x200B;拖曳至表單。
1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中，從&#x200B;**[!UICONTROL 欄名稱]**&#x200B;欄位選取搜尋所依據的收件匣欄名稱。
1. 指定在「搜尋」文字方塊中顯示的文字，作為&#x200B;**[!UICONTROL 搜尋文字方塊預留位置]**&#x200B;欄位中的預留位置文字。
1. 指定組態的選擇性描述，並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存。

當您開啟「篩選器」頁面時，會反映組態變更。 當您按下Enter鍵時，[!DNL Experience Manager]會將步驟4中指定的搜尋文字套用至步驟3中指定的欄名稱，並傳回「收件匣」專案。

## 設定日期範圍述詞 {#date-range-predicate}

您可以篩選收件匣專案，以使用日期範圍述詞在收件匣欄中搜尋日期範圍。

設定日期範圍述詞：

1. 開啟組態[的](#creating-opening-customized-configuration)表單。
1. 選取&#x200B;**[!UICONTROL 選取述詞]**&#x200B;索引標籤，並將&#x200B;**[!UICONTROL 日期範圍述詞]**&#x200B;拖曳至表單。
1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中，從&#x200B;**[!UICONTROL 欄名稱]**&#x200B;欄位選取搜尋所依據的收件匣欄名稱。
1. 在&#x200B;**[!UICONTROL 篩選標籤]**&#x200B;欄位中指定日期範圍篩選的標籤。
1. 指定篩選的開始日期和結束日期標籤。
1. 指定組態的選擇性描述，並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存。

當您開啟「篩選器」頁面時，會反映組態變更。 您在步驟4中指定的篩選標籤，連同步驟5中指定的開始日期和結束日期標籤，顯示為日期範圍篩選的標籤。 [!DNL Experience Manager]將搜尋條件套用到步驟3中指定的欄名稱，並傳回收件匣專案。

## 設定自訂欄選項述詞 {#custom-column-options-predicate}

您可以使用自訂欄選項述詞來篩選收件匣專案，以搜尋收件匣欄中的自訂選項。

設定自訂欄選項述詞：

1. 開啟組態[的](#creating-opening-customized-configuration)表單。
1. 選取&#x200B;**[!UICONTROL 選取述詞]**&#x200B;索引標籤，並將&#x200B;**[!UICONTROL 自訂資料行選項述詞]**&#x200B;拖曳至表單。
1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;索引標籤中，從&#x200B;**[!UICONTROL 欄名稱]**&#x200B;欄位選取搜尋所依據的收件匣欄名稱。
1. 在&#x200B;**[!UICONTROL 篩選標籤]**&#x200B;欄位中指定自訂資料行選項篩選的標籤。
1. 選取&#x200B;**[!UICONTROL 單選]**&#x200B;核取方塊，以啟用在收件匣欄套用篩選器時只選取一個選項。
1. 在&#x200B;**[!UICONTROL 新增選項]**&#x200B;區段中：
   1. 選取&#x200B;**[!UICONTROL 手動]**&#x200B;以手動定義篩選器搜尋選項。 選取&#x200B;**[!UICONTROL 新增篩選器選項]**&#x200B;以定義第一個選項。 指定欄選項的標籤和要搜尋的選項值文字。 例如，如果您要在[收件匣]欄中搜尋&#x200B;**Female**&#x200B;作為值，您可以指定&#x200B;**F**&#x200B;作為欄選項的標籤，並新增&#x200B;**Female**&#x200B;作為選項值文字。 同樣地，您可以新增更多篩選器選項。
   1. 選取&#x200B;**[!UICONTROL JSON路徑]**&#x200B;以使用JSON檔案路徑定義選項。 以下是可定義篩選選項的JSON檔案範例：

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

   1. 選取&#x200B;**[!UICONTROL CRX選項路徑]**&#x200B;以使用CRX存放庫路徑定義選項。 選取&#x200B;**[!UICONTROL 新增選項路徑]**&#x200B;以新增多個路徑。 以下是定義`Male`和`Female`篩選選項的範例：

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

1. 指定組態的選擇性描述，並選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存。

當您開啟「篩選器」頁面時，會反映組態變更。 您在步驟4中指定的篩選器標籤會顯示為「自訂欄選項」述詞的標籤。 [!DNL Experience Manager]將步驟6中定義的搜尋條件套用至步驟3中指定的欄名稱，並傳回收件匣專案。

下列影片說明根據`true`和`false`選項值篩選欄的步驟。

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## 根據述詞檢視搜尋篩選器 {#view-search-filters-for-predicates}

您可以檢視根據述詞的搜尋篩選器。 在收件匣頁面上選取&#x200B;**[!UICONTROL 篩選器]**。 這些篩選器會顯示在左窗格中。 然後，您可以指定搜尋條件以篩選收件匣專案。

![篩選器頁面](assets/apply-filters.png)

如需有關管理述詞設定的詳細資訊，請參閱[設定搜尋Forms](search-forms.md)。

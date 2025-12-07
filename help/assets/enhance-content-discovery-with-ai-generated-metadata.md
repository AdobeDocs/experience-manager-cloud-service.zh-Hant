---
title: 在管理員檢視中使用AI產生的中繼資料增強內容探索
description: 瞭解如何在「管理檢視」中使用AI產生的中繼資料來增強內容探索
feature: Smart Tags,Tagging
role: Admin,User
source-git-commit: f83324be68bdab65e5c76ef336eb7e4a2e318dd1
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 9%

---


# 使用AI產生的中繼資料加強內容探索 {#ai-smart-tags}

| UI | 文章連結 |
| -------- | ---------------------------- |
| 資產檢視 | [按一下這裡](/help/assets/ai-generated-metadata-assets-view.md) |
| 管理員檢視 | 本文章 |

AI不會依賴手動輸入，而是自動將描述性標籤指派給數位資產。 這些 AI 產生的標記可提升中繼資料的品質，讓資產搜尋、分類和推薦變得更簡單。此方法不僅可避免手動標籤，進而提升效率，還可確保大量數位內容的一致性和擴充性。 例如，如果資產是影像，AI可以識別其中的物件、場景、情感，或甚至品牌標誌，並產生相關標籤，例如「日落」、「海灘」、「假期」或「微笑」。 AI產生的內容可運用語意和辭彙搜尋技術來增強資產搜尋。 檢視更多[搜尋Assets](search-assets.md)。<!--If the asset is a document, AI reads and interprets the text to assign meaningful keywords that summarize its content—such as "climate change," "policy," or "renewable energy.-->

![增強型智慧標籤](assets/enhanced-smart-tags1.png)

## 如何啟用AI產生的中繼資料？ {#enable-ai-generated-metadata}

若要啟用AI產生的中繼資料：

* 最低必要的AEM發行版本為`20626`。

## 設定AI產生的標題 {#configure-ai-generated-titles}

AEM可讓您在「資產瀏覽」頁面上的「卡片」檢視或「清單」檢視中，設定資產標題的顯示方式。 您可以選擇顯示您定義的資產標題、使用 AI 產生的標題，或僅於資產沒有現有標題時使用 AI 產生的標題。

若要設定AI產生的標題：

1. 導覽至&#x200B;**[!UICONTROL 工具> Assets > Assets設定>智慧標籤增強設定]**。

1. 選取下列其中一個選項：

   * **顯示DC標題（預設）**：在資產屬性中可用的&#x200B;**[!UICONTROL 標題]**&#x200B;欄位中指定標題，以在卡片檢視或清單檢視中顯示。 如果未定義資產標題，AEM Assets會顯示檔案名稱。

   * **顯示AI產生的標題**：顯示AI產生的標題，並忽略資產屬性中指定的標題。 如果AI產生的標題不適用於資產，AEM Assets會顯示其屬性中可用的預設資產標題。

   * **只有在DC標題不存在時才顯示AI產生的標題**：只有在沒有為資產定義資產標題時，AEM Assets才會顯示AI產生的標題。

     ![設定 AI 產生的標題](assets/configure-title-ai-generated.png)

## 使用AI產生的中繼資料 {#using-ai-generated-smart-tags}

<!--[!NOTE]
>
>The enhanced smart tags capability is available only for the newly uploaded assets.
-->

若要使用增強智慧標籤功能，請執行下列步驟：

1. 在[!DNL Experience Manager]介面中，前往所需的資料夾，然後按一下&#x200B;**[!UICONTROL 新增Assets]**。 <!--Alternatively, to update enhanced smart tags in an existing content, click **[!UICONTROL reprocess]**.-->相容的影像檔案格式為`png`、`jpg`、`jpeg`、`psd`、`tiff`、`gif`、`webp`、`crw`、`cr2`、`3fr`、`nef`、`arw`和`bmp`。

1. 等候新上傳的資產處理完畢。 完成後，前往資產屬性。

1. 移至&#x200B;**[!UICONTROL AI產生的]**&#x200B;標籤。 如果[!DNL Experience Manager]版本不相容或未更新，則不會顯示此索引標籤。 有以下欄位：

   * **[!UICONTROL 產生的標題]：**&#x200B;標題提供簡潔的標題，擷取上傳資產的核心概念，讓您一眼就能輕鬆理解。 新增資產時，如果您提供標題（在`dc:title`中），資產瀏覽檢視中會顯示該標題。 如果保留為空白，則會自動指派AI產生的標題。
   * **[!UICONTROL 已產生描述]：**&#x200B;描述提供資產相關資訊的簡短摘要，協助使用者和搜尋模組快速掌握其關聯性。
   * **[!UICONTROL 產生的關鍵字]：**&#x200B;關鍵字是代表資產主要主題的目標辭彙，有助於標籤和內容篩選。

1. [選擇性]如果您覺得遺漏任何相關標籤，可以新增其他標籤或建立自己的標籤。 若要這麼做，請在&#x200B;**[!UICONTROL 產生的關鍵字]**&#x200B;欄位中寫入您的標籤，然後按一下&#x200B;**[!UICONTROL 儲存]**。

## 停用AI產生的中繼資料 {#disable-ai-generated-metadata}

若要停用AI產生的中繼資料：

1. 導覽至&#x200B;**[!UICONTROL 工具> Assets > Assets設定>智慧標籤增強設定]**。

1. 選取&#x200B;**[!UICONTROL 停用智慧標籤增強功能]**。

1. 按一下「**[!UICONTROL 儲存]**」。

上傳至AEM Assets的新資產或資料夾將停用AI產生的中繼資料。 已產生AI產生中繼資料欄位的現有資產或資料夾仍會繼續顯示這些欄位。
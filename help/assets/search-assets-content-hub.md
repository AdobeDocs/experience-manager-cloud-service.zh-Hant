---
title: 在 Content Hub 中搜尋資產
description: 瞭解如何搜尋 [!DNL Content Hub]中的資產
role: User
exl-id: 8578d7d0-32b9-4e5c-80ef-3827e358ac6c
source-git-commit: a0ca51bdf2cd4ece11e05243713a616e9fcb5850
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---

# 在[!DNL Content Hub]中搜尋Assets {#search-assets}

當存放庫中有大量資產時，搜尋合適的資產相當耗時。 [!DNL The Content Hub]搜尋可讓您尋找已核准的資產，這樣您就可以對資產執行其他動作，例如下載、共用或建立集合。 您可以利用各種功能來縮小搜尋結果的範圍，例如，執行文字式搜尋、使用篩選條件、執行標籤或智慧標籤特定搜尋、搜尋特定檔案格式等。

## 先決條件 {#prerequisites}

[Content Hub使用者](deploy-content-hub.md#onboard-content-hub-users)可以執行本文中提到的動作。

## 您可以搜尋的內容  {#what-you-can-search}

[!DNL Content Hub]搜尋提供的結果依據：

* **比對文字：** [!DNL Content Hub]搜尋可讓您使用資產名稱或描述來搜尋資產。 您可以執行關鍵字式搜尋，將關鍵字與資產屬性中可用的文字做比較。

* **相符的內容：** [!DNL Content Hub]搜尋結果清單包含您根據相符的內容所取得之資產的近似結果。 例如，如果您在搜尋列中輸入`cool`，則與`winter`、`snow`、`cold surroundings`相關的資產會顯示在搜尋清單中。

* **資產資訊（標題、標籤或智慧標籤）：** [!DNL Content Hub]會使用智慧搜尋演演算法，儘可能將搜尋結果排入正確的等級。 [中繼資料](#asset-properties.md)是資產所有可用資料的集合，但不一定包含在該資產中。 [它有助於您進一步將資產分類，而且隨著數位資訊量成長，會很有幫助](/help/assets/configure-content-hub-ui-options.md##configure-metadata-search-content-hub)。

* **上次修改日期：**&#x200B;最近修改的資產會出現在搜尋結果清單的最前面。 您也可以視需求篩選日期範圍。

* **使用狀況：**&#x200B;常用的資產會出現在搜尋清單的頂端。

* **搜尋歷程記錄：**&#x200B;在搜尋方塊內按一下，而不輸入字元以取得您的搜尋歷程記錄。 您也可以從歷史記錄中移除任何特定關鍵字。 搜尋記錄儲存在網頁瀏覽器的快取記憶體中，這表示如果您在不同瀏覽器中存取[!DNL Content Hub]搜尋，或清除瀏覽器的快取記憶體，您將無法再檢視搜尋記錄。

* **當您輸入時進行搜尋：** [!DNL Content Hub]搜尋會在您開始輸入時提供自動完成的建議，藉以強化您的搜尋體驗。

## 基本搜尋 {#basic-search}

若要在[!DNL the Content Hub]上執行基本搜尋，請瀏覽至搜尋列，並指定您需要搜尋的關鍵字。 導覽至左側窗格中可用的篩選器，並套用這些篩選器以縮小搜尋結果的範圍。

例如，搜尋關鍵字為&#x200B;**[!UICONTROL 且去年修改過的所有]** JPEG`architect`影像。 若要執行此案例，請執行下列步驟：

1. 指定`architect`作為搜尋關鍵字。

1. 導覽至篩選器面板> **[!UICONTROL 格式]** >選取&#x200B;**[!UICONTROL JPEG]**。

1. 瀏覽至&#x200B;**[!UICONTROL 已修改]** >指定日期範圍。

   ![基本搜尋](assets/basic-search.png)

## 使用篩選器縮小搜尋結果 {#narrow-down-search-results}

使用「篩選器」面板，根據中繼資料搜尋資產。 您可以根據各種搜尋述詞來篩選搜尋結果。 您可以選取所有適當的述詞，以最小化或縮小搜尋結果。 篩選搜尋結果時，您可以選擇10個以上的述詞。 當您在篩選器中選取多個選項時，Content Hub會顯示符合在篩選器中選取之任何選項的資產。 不過，當您跨篩選器選取多個選項時，Content Hub只會顯示符合跨篩選器選取之所有選項的資產，以縮小搜尋結果的範圍。

預設篩選條件包括檔案格式、核准者、核准日期、過期和未過期的資產，以及過期日期。 管理員也可以設定篩選器清單中顯示的篩選器。 如需詳細資訊，請參閱[設定Content Hub使用者介面](configure-content-hub-ui-options.md#configure-filters-content-hub)。

<!--

<table>
    <tbody>
     <tr>
      <th><strong>Search Predicate</strong></th>
      <th><strong>Description</strong></th>
      <th><strong>Properties</strong></th>
     </tr>
     <tr>
      <td> Campaigns </td>
      <td> Allows you to search using planned activity performed to take any particular action. For example, advertisement campaign run on Ferrari to know the understand the interests of people using number of clicks people perform.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Channels </td>
      <td> Helps you to understand the path from where the asset is coming from. For example, web, social media, books, catalog, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Region </td>
      <td> Helps you to understand the location where the asset is created. For example, Japan, EMEA, Worldwide, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Keywords </td>
      <td> Keyword helps you search using terms or the words that you enter based on the topic. For example, images, low-resolution, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Timeframe </td>
      <td> Helps you search assets using timeline. For example, search by year 2024, Q3 2023, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td>File format</td>
      <td>Composition of an asset. The supported assets include image, document, video, printable media, and so on.</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL Quicktime]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL WebP]</li> 
            <li>[!UICONTROL MP4]</li> 
            <li>[!UICONTROL Plain]</li> 
            <li>[!UICONTROL PDF]</li>
            <li>[!UICONTROL SVG + XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Tags</td>
      <td>Tags help you categorize assets that can be browsed and searched more efficiently based on hierarchical taxonomies.</td>
      <td>
        <ul>
            <li>Field label</li>
            <li>Property name</li>
            <li>Path</li>
            <li>Description</li>
        </ul>
      </td>
     </tr>
     <!--<tr>
      <td>Subject</td>
      <td>Classification of assets based on their theme. For example, colorful, hiking, outdoors.</td>
      <td>NA</td>
     </tr>
          <tr>
      <td>Last modified</td>
      <td>Search assets based on their last modification. Specify the date range using the Start date and End date fields.</td>
      <td>
        <ul>
            <li>Range text (From)</li> 
            <li>Range text (To) </li>
        </ul>
      </td>
     </tr>    
     <!--<tr>
      <td>Asset ID</td>
      <td>Unique number that identifies the asset.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Colors </td>
      <td> Helps you search assets using colors that are automatically identified in an asset using Adobe's Sensei AI capabilities.</td>
      <td>NA</td>
     </tr>  
    </tbody>
   </table>

-->

## 透過搜尋完成更多工作 {#do-more-with-search}

[!DNL The Content Hub]不限於搜尋，而是可讓您直接從搜尋或預覽介面執行其他動作，例如[下載](download-assets-content-hub.md)、[共用](share-assets-content-hub.md)以及[新增資產至集合](collections-content-hub.md)。 在搜尋結果頁面上選取資產以檢視這些選項。

---
title: 智慧標籤您的視訊資產
description: Experience Manager會使用 [!DNL Adobe Sensei]自動將內容與描述性智慧標籤新增至影片。
feature: 智慧標籤，標籤
role: Admin,User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 0%

---

# 智慧標籤您的視訊資產 {#video-smart-tags}

對新內容的需求不斷增加，需要減少手動操作，以便不時提供引人入勝的數位體驗。 [!DNL Adobe Experience Manager] as a支援 [!DNL Cloud Service] 使用人工智慧自動標籤視訊資產。手動標籤視訊可能很耗時。 不過，[!DNL Adobe Sensei]支援的視訊智慧標籤功能會使用人工智慧模型來分析視訊內容，並將標籤新增至視訊資產。 因此，DAM使用者可縮短向客戶提供豐富體驗的時間。 Adobe的機器學習服務會為視訊產生兩組標籤。 而一組則對應於該影片中的物件、場景和屬性；另一組與飲用、跑步和慢跑等動作有關。

在[!DNL Adobe Experience Manager]中，預設會將視訊標籤啟用為[!DNL Cloud Service]。 不過，您可以在資料夾上[選擇退出視訊智慧標籤](#opt-out-video-smart-tagging)。 上傳新視訊或重新處理現有視訊時，會自動標籤視訊。 [!DNL Experience Manager] 也會建立縮圖並擷取視訊檔案的中繼資料。在資產[!UICONTROL 屬性]中，智慧標籤會以其[信賴分數](#confidence-score-video-tag)的遞減順序顯示。

## 上傳時的智慧標籤影片 {#smart-tag-assets-on-ingestion}

當您[上傳視訊資產](add-assets.md#upload-assets)以[!DNL Cloud Service]的形式上傳至[!DNL Adobe Experience Manager]時，會處理視訊。 處理完成後，請參閱資產[!UICONTROL 屬性]頁面的[!UICONTROL 基本]標籤。 智慧標籤會自動新增至[!UICONTROL 智慧標籤]下的視訊。 資產微服務會運用[!DNL Adobe Sensei]來建立這些智慧標籤。

![智慧標籤會新增至影片，並在資產屬性的「基本」標籤中顯示](assets/smart-tags-added-to-videos.png)

套用的智慧標籤會以[信賴分數](#confidence-score-video-tag)的降序排序，並結合物件和動作標籤，在[!UICONTROL 智慧標籤]內。

>[!IMPORTANT]
>
>建議您檢閱這些自動產生的標籤，以確保這些標籤符合您的品牌及其值。

## 在DAM中智慧標籤現有視訊 {#smart-tag-existing-videos}

DAM中現有的視訊資產不會自動加上智慧標籤。 您需要手動[!UICONTROL 重新處理資產]，為資產產生智慧標籤。

若要智慧標籤資產或資產存放庫中已存在之資產的資料夾（包括子資料夾），請遵循下列步驟：

1. 選取[!DNL Adobe Experience Manager]標誌，然後從[!UICONTROL Navigation]頁面中選取資產。

1. 選取[!UICONTROL 檔案]以顯示資產介面。

1. 導覽至您要套用智慧標籤的資料夾。

1. 選取整個資料夾或特定視訊資產。

1. 選擇「![重新處理資產」表徵圖](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL 「重新處理資產」表徵圖並選擇「[!UICONTROL 完全處理」]選項。]

<!-- TBD: Limit size -->

![重新處理資產，將標籤新增至現有DAM存放庫的影片](assets/reprocess.gif)

程式完成後，導覽至資料夾內任何視訊資產的[!UICONTROL 屬性]頁面。 自動新增的標籤會顯示在[!UICONTROL Basic]標籤的[!UICONTROL 智慧標籤]區段中。 這些套用的智慧標籤會以[信賴分數](#confidence-score-video-tag)的遞減順序排序。

## 搜索標籤的視頻 {#search-smart-tagged-videos}

若要根據自動產生的智慧標籤來搜尋視訊資產，請使用[Omnisearch](search-assets.md#search-assets-in-aem):

1. 選擇搜索表徵圖![搜索表徵圖](assets/do-not-localize/search_icon.png)以顯示Omnisearch欄位。

1. 在Omnisearch欄位中指定您尚未明確新增至視訊的標籤。

1. 根據標籤進行搜尋。

搜尋結果會根據您指定的標籤顯示視訊資產。

您的搜尋結果是視訊資產與中繼資料中搜尋關鍵字的組合，以及智慧標籤搜尋關鍵字的視訊資產。 不過，會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 如需詳細資訊，請參閱[了解包含智慧標籤的搜尋結果](smart-tags.md#understand-search)。 [!DNL Experience Manager] 

## 協調視訊智慧標籤 {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] 可讓您將智慧標籤組織為：

* 移除指派給您品牌影片的不正確標籤。

* 確保視訊顯示在最相關標籤的搜尋結果中，以縮小視訊的標籤搜尋範圍。 因此，搜尋結果不會顯示不相關視訊。

* 指派較高的排名給標籤，以提高與視訊的相關性。 促銷視訊的標籤，會增加根據該標籤執行搜尋時，視訊出現在搜尋結果中的機率。

若要進一步了解如何協調資產的智慧標籤，請參閱[管理智慧標籤](smart-tags.md#manage-smart-tags-and-searches)。

![協調視訊智慧標籤](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>重新處理資產時，不會記住使用[管理智慧標籤](smart-tags.md#manage-smart-tags-and-searches)中的步驟協調的任何標籤。 原始標籤集會再次顯示。

## 選擇退出視訊智慧標籤 {#opt-out-video-smart-tagging}

由於視訊的自動標籤會與其他資產處理工作（例如建立縮圖和擷取中繼資料）同時執行，因此可能會很耗時。 若要加快資產處理速度，您可以在資料夾層級上傳時選擇退出視訊智慧標籤。

若要針對上傳至特定資料夾的資產選擇退出自動產生智慧型視訊標籤：

1. 開啟資料夾[!UICONTROL 屬性]中的[!UICONTROL 資產處理]標籤。

1. 在「[!UICONTROL 影片智慧標籤]」功能表中，預設會選取「繼承]」選項，並啟用影片智慧標籤。[!UICONTROL 

   選擇[!UICONTROL Inherited]選項時，還將顯示繼承的資料夾路徑，以及該路徑是否設定為[!UICONTROL Enable]或[!UICONTROL Disable]的資訊。

   ![停用視訊智慧標籤](assets/disable-video-tagging.png)

1. 選取[!UICONTROL 停用]以退出已上傳至資料夾之視訊的智慧標籤。

>[!IMPORTANT]
>
>如果您在上傳時選擇退出在資料夾上標籤視訊，且想在上傳後以智慧標籤視訊，則請從資料夾[!UICONTROL 屬性]的[!UICONTROL 資產處理]標籤中&#x200B;**[!UICONTROL 啟用視訊的智慧標籤，並使用[[!UICONTROL 重新處理資產]選項](#smart-tag-existing-videos)將智慧標籤新增至視訊。]**

## 信賴分數 {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] 對對象和動作智慧標籤套用最小信賴度臨界值，以避免每個視訊資產的標籤過多，進而減緩索引速度。您的資產搜尋結果會根據可信度分數進行排名，這通常會改善搜尋結果，超出任何視訊資產所指派標籤的檢查所建議的程度。 不準確的標籤常會有較低的信賴分數，因此很少出現在資產的「智慧標籤」清單頂端。

[!DNL Adobe Experience Manager]中動作和物件標籤的預設臨界值為0.7（值應介於0和1之間）。 如果某些視訊資產未被特定標籤加上標籤，表示演算法對預測標籤的信賴度低於70%。 對於所有使用者，預設臨界值不一定都是最佳的。 因此，您可以變更OSGI設定中的信賴分數值。

若要將信賴分數OSGI設定新增至部署至[!DNL Adobe Experience Manager]作為[!DNL Cloud Service]至[!DNL Cloud Manager]的專案，請執行下列動作：

* 在[!DNL Adobe Experience Manager]專案（自Archetype 24起，或先前的`ui.apps`）中，`config.author` OSGi設定包含名為`com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json`的設定檔案，其內容如下：`ui.config`

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>手動標籤的可信度為100%（最大可信度）。 因此，如果有具有手動標籤的視訊資產符合搜尋查詢，則會在符合搜尋查詢的智慧標籤之前顯示。

## 限制 {#video-smart-tagging-limitations}

* 您無法使用任何特定影片訓練將智慧標籤套用至影片的服務。 它適用於預設的[!DNL Adobe Sensei]設定。

* 未顯示標籤進度。

* 只有小於300 MB的影片會自動加上標籤。 [!DNL Adobe Sensei]服務會略過大小較大的視訊檔案。

* 只有[智慧標籤](/help/assets/smart-tags.md#smart-tags-supported-file-formats)中提及的檔案格式和支援的轉碼器的視訊會受到標籤。

>[!MORELIKETHIS]
>
>* [管理智慧標籤和資產搜尋](smart-tags.md#manage-smart-tags-and-searches)
* [訓練智慧標籤服務並標籤影像](smart-tags.md)


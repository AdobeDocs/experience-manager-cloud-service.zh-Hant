---
title: 智慧標籤您的視訊資產
description: Experience Manager會使用 [!DNL Adobe Sensei]自動將內容相關和描述性的智慧型標籤加入影片。
feature: Smart Tags,Tagging
role: Administrator,Business Practitioner
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---


# 智慧標籤您的視訊資產{#video-smart-tags}

對新內容的需求日益增長，需要減少人工操作，以便迅速提供吸引人的數位體驗。 [!DNL Adobe Experience Manager] 支援 [!DNL Cloud Service] 使用人工智慧自動標籤視訊資產。手動標籤視訊會很耗時。 不過，[!DNL Adobe Sensei]支援的視訊智慧標籤功能使用人工智慧模型來分析視訊內容，並新增標籤至視訊資產。 如此可縮短DAM使用者為其客戶提供多樣化體驗的時間。 Adobe的機器學習服務為一個視頻生成兩組標籤。 而其中一組則對應該視訊中的物件、場景和屬性；另一組則涉及飲酒、跑步和慢跑等動作。

在[!DNL Adobe Experience Manager]中，視訊標籤預設為[!DNL Cloud Service]。 不過，您可以在資料夾上[選擇退出視訊智慧標籤](#opt-out-video-smart-tagging)。 當您上傳新視訊或重新處理現有視訊時，視訊會自動加上標籤。 [!DNL Experience Manager] 此外，還會建立視訊檔案的縮圖並擷取中繼資料。智慧型標籤在資產[!UICONTROL 屬性]中以其[信賴分數](#confidence-score-video-tag)的遞減順序顯示。

## 上傳{#smart-tag-assets-on-ingestion}時智慧標籤影片

當您[將視訊資產](add-assets.md#upload-assets)上傳至[!DNL Adobe Experience Manager]為[!DNL Cloud Service]時，會處理視訊。 處理完成後，請參閱資產[!UICONTROL 屬性]頁面的[!UICONTROL 基本]標籤。 智慧型標籤會自動新增至[!UICONTROL 智慧型標籤]下方的視訊。 資產微服務利用[!DNL Adobe Sensei]來建立這些智慧標籤。

![智慧型標籤會新增至影片，並在資產屬性的「基本」索引標籤中顯示](assets/smart-tags-added-to-videos.png)

在[!UICONTROL 智慧型標籤]中，以[信賴分數](#confidence-score-video-tag)的遞減順序對所套用的智慧型標籤進行排序，並結合物件和動作標籤。

>[!IMPORTANT]
>
>建議您檢閱這些自動產生的標籤，以確保它們符合您的品牌及其價值。

## 在DAM {#smart-tag-existing-videos}中智慧標籤現有視訊

DAM中現有的視訊資產不會自動加上智慧標籤。 您需要手動[!UICONTROL 重新處理資產]，以便為資產產生智慧標籤。

若要智慧標籤資產儲存庫中已存在的資產的視訊資產或資料夾（包括子檔案夾），請遵循下列步驟：

1. 選擇[!DNL Adobe Experience Manager]標誌，然後從[!UICONTROL Navigation]頁面選擇資產。

1. 選擇[!UICONTROL 檔案]以顯示資產介面。

1. 導覽至您要套用智慧標籤的資料夾。

1. 選取整個資料夾或特定視訊資產。

1. 選擇「![重新處理資產」表徵圖](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL 「重新處理資產」表徵圖，然後選擇「完全處理」選項。]

<!-- TBD: Limit size -->

![重新處理資產，以新增標籤至現有DAM儲存庫的視訊](assets/reprocess.gif)

完成此程式後，導航至資料夾內任何視頻資產的[!UICONTROL Properties]頁。 自動添加的標籤顯示在[!UICONTROL Basic]頁籤的[!UICONTROL Smart Tags]部分中。 這些套用的智慧型標籤會依[信賴分數](#confidence-score-video-tag)的遞減順序排序。

## 搜尋標籤的影片{#search-smart-tagged-videos}

若要根據自動產生的智慧標籤來搜尋視訊資產，請使用[Omnisearch](search-assets.md#search-assets-in-aem):

1. 選擇搜索表徵圖![搜索表徵圖](assets/do-not-localize/search_icon.png)以顯示Omnisearch欄位。

1. 在「Omnisearch」欄位中指定您尚未明確新增至視訊的標籤。

1. 根據標籤進行搜尋。

搜尋結果會根據您指定的標籤顯示視訊資產。

您的搜尋結果是中繼資料中視訊資產與搜尋關鍵字的組合，以及以搜尋關鍵字智慧標籤的視訊資產。 但是，會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 如需詳細資訊，請參閱[瞭解 [!DNL Experience Manager] 含智慧型標籤的搜尋結果](smart-tags.md#understandsearch)。

## 協調視訊智慧標籤{#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] 可讓您組織智慧型標籤，以：

* 移除指派給您品牌影片的不正確標籤。

* 確保視訊出現在搜尋結果中，以尋找最相關的標籤，以調整以標籤為基礎的視訊搜尋。 因此，它可消除不相關視訊出現在搜尋結果中的可能性。

* 指派較高的排名給標籤，以提高其與視訊的相關性。 促銷視訊的標籤會增加當根據該標籤執行搜尋時，在搜尋結果中顯示視訊的機率。

若要進一步瞭解如何協調資產的智慧標籤，請參閱[管理智慧標籤](smart-tags.md#manage-smart-tags-and-searches)。

![協調視訊智慧型標籤](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>在重新處理資產時，不會記住使用[管理智慧標籤](smart-tags.md#manage-smart-tags-and-searches)中的步驟協調的任何標籤。 原始標籤集會再次顯示。

## 選擇退出視頻智慧標籤{#opt-out-video-smart-tagging}

當自動標籤視訊與建立縮圖和擷取中繼資料等其他資產處理工作同時執行時，可能會很耗時。 若要加速資產處理，您可以在資料夾層級上傳時選擇退出視訊智慧型標籤。

若要針對上傳至特定資料夾的資產，選擇退出自動產生視訊智慧標籤：

1. 在資料夾[!UICONTROL 屬性]中開啟[!UICONTROL 資產處理]頁籤。

1. 在[!UICONTROL 視訊智慧標籤]功能表中，預設會選取[!UICONTROL 繼承]選項，並啟用視訊智慧標籤。

   當選擇[!UICONTROL Inherited]選項時，繼承的資料夾路徑以及將其設定為[!UICONTROL Enable]或[!UICONTROL Disable]的資訊也會一併顯示。

   ![停用視訊智慧標籤](assets/disable-video-tagging.png)

1. 選擇「[!UICONTROL 停用]」以選擇退出智慧標籤上傳至資料夾的視訊。

>[!IMPORTANT]
>
>如果您已選擇在上傳時不在資料夾上標籤視訊，而想在上傳後智慧標籤視訊，則從資料夾[!UICONTROL 「屬性」的「資產處理」標籤[!UICONTROL 「啟用視訊的智慧標籤」]**，然後使用「重新處理資產」[選項](#smart-tag-existing-videos)新增智慧型標籤至視訊。**]

## 信賴分數{#confidence-score-video-tag}

[!DNL Adobe Experience Manager] 套用物件和動作智慧標籤的最小信賴臨界值，以避免每個視訊資產的標籤過多，進而降低索引速度。您的資產搜尋結果會根據信賴分數進行排名，這通常會改善搜尋結果，超出任何視訊資產的指派標籤檢查所暗示的程度。 不正確的標籤通常會有低可信度分數，因此很少出現在資產的「智慧標籤」清單頂端。

[!DNL Adobe Experience Manager]中動作和物件標籤的預設臨界值為0.7（值應介於0和1之間）。 如果某些視訊資產未由特定標籤標籤，則表示演算法對預測標籤的信心低於70%。 預設臨界值不一定對所有使用者都是最佳值。 因此，您可以變更OSGI設定中的信賴分數值。

若要將信賴分數OSGI組態新增至部署至[!DNL Adobe Experience Manager]的專案，以[!DNL Cloud Service]至[!DNL Cloud Manager]為單位：

* 在[!DNL Adobe Experience Manager]專案（`ui.config`自Archetype 24起，或先前的`ui.apps`）中，`config.author` OSGi組態包含名為`com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json`的組態檔，其內容如下：

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>手動標籤的可信度為100%（最大可信度）。 因此，如果有視訊資產具有與搜尋查詢相符的手動標籤，則會在與搜尋查詢相符的智慧標籤之前顯示。

## 限制 {#video-smart-tagging-limitations}

* 您無法訓練使用任何特定視訊套用智慧型標籤至視訊的服務。 它適用於預設的[!DNL Adobe Sensei]設定。

* 不會顯示標籤進度。

* 只有檔案大小小於300 MB的視訊會自動標籤。 [!DNL Adobe Sensei]服務會跳過大小較大的視訊檔案。

* 只有[智慧型標籤](/help/assets/smart-tags.md#smart-tags-supported-file-formats)中提及的檔案格式和支援的轉碼器中的視訊才會標籤。

>[!MORELIKETHIS]
>
>* [管理智慧標籤和資產搜尋](smart-tags.md#manage-smart-tags-and-searches)
>* [訓練智慧型標籤服務並標籤您的影像](smart-tags.md)


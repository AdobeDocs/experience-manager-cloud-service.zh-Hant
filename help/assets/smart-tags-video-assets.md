---
title: 智慧標籤您的視訊資產
description: 智慧型標籤視訊資產會使用Adobe Sensei服務套用情境式和描述性標籤，以自動化資產標籤。
translation-type: tm+mt
source-git-commit: 68fe67617f0d63872f13427b3fbc7b58f2497aca
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---


# 智慧標籤您的視訊資產 {#video-smart-tags}

對新內容的需求日益增長，需要減少人工操作，以便迅速提供吸引人的數位體驗。 [!DNL Adobe Experience Manager] 雲端服務支援人工智慧輔助的視訊資產自動標籤。 手動標籤視訊會很耗時。 不過，Adobe Sensei支援的視訊智慧標籤功能使用人工智慧模型來分析視訊內容，並新增標籤至視訊資產。 如此可縮短DAM使用者為其客戶提供多樣化體驗的時間。 Adobe的機器學習服務會為視訊產生兩組標籤。 而其中一組則對應該視訊中的物件、場景和屬性；另一組則涉及飲酒、跑步和慢跑等動作。

智慧型標籤支援的視訊檔案格式（及其轉碼器）為MP4(H264/AVC)、MKV(H264/AVC)、MOV(H264/AVC、Motion JPEG)、AVI(indeo4)、FLV(H264/AVC、vp6f)和WMV(WMV2)。 此外，此功能還允許將視訊標籤為300 MB。 視訊上傳後或觸發重新處理時，自動標籤視訊資產會做為標準資產處理（以及建立縮圖和擷取中繼資料）。 智慧型標籤會依其在資產屬性中的信賴 [分數](#confidence-score-video-tag) ，以遞減 [!UICONTROL 順序顯示]。 視訊標籤預設會以雲端服 [!DNL Adobe Experience Manager] 務的形式啟用。 不過，您可以 [選擇退出資料夾上的視訊智慧標籤](#opt-out-video-smart-tagging) 。

## 上傳時智慧標籤影片 {#smart-tag-assets-on-ingestion}

當您將視 [訊資產上傳](add-assets.md#upload-assets)[!DNL Adobe Experience Manager] 至雲端服務時，視訊會經過 ![處理](assets/do-not-localize/assetprocessing.png)。 處理完成後，請參閱「資產 [!UICONTROL 屬性] 」頁面的「基 [!UICONTROL 本」標籤] 。 智慧型標籤會自動新增至「智慧型標籤」 [!UICONTROL 下方的視訊]。 資產計算服務運用Adobe Sensei來建立這些智慧標籤。

![智慧型標籤會新增至影片，並在資產屬性的「基本」索引標籤中顯示](assets/smart-tags-added-to-videos.png)

套用的智慧型標籤會在智慧型標籤內，以遞減 [順序排序](#confidence-score-video-tag)，並結合物件和動作 [!UICONTROL 標籤]。

>[!IMPORTANT]
>
>建議您檢閱這些自動產生的標籤，以確保它們符合您的品牌及其價值。

## 在DAM中智慧標籤現有視訊 {#smart-tag-existing-videos}

DAM中現有的視訊資產不會自動加上智慧標籤。 您需要手動 [!UICONTROL 重新處理資產] ，才能為資產產生智慧標籤。

若要智慧標籤資產儲存庫中已存在的資產的視訊資產或資料夾（包括子檔案夾），請遵循下列步驟：

1. 選取標 [!DNL Adobe Experience Manager] 志，然後從「導覽」頁面 [!UICONTROL 選取] 「資產」。

1. 選取「 [!UICONTROL 檔案] 」以顯示「資產」介面。

1. 導覽至您要套用智慧標籤的資料夾。

1. 選取整個資料夾或特定視訊資產。

1. 選取「 ![重新處理資產」圖](assets/do-not-localize/reprocess-assets-icon.png)[!UICONTROL 示「重新處理資產] 」圖示，然後選取「完 [!UICONTROL 整處理] 」選項。

![重新處理資產，以新增標籤至現有DAM儲存庫的視訊](assets/reprocess.gif)

完成程式後，導覽至資料 [!UICONTROL 夾內任何視訊資產的「屬性] 」頁面。 自動新增的標籤會顯示在「基本」 [!UICONTROL 標籤的] 「智慧標籤 [!UICONTROL 」區段中] 。 這些套用的智慧型標籤會依信賴分數的遞減 [順序排序](#confidence-score-video-tag)。

## 搜尋標籤的影片 {#search-smart-tagged-videos}

若要根據自動產生的智慧標籤來搜尋視訊資產，請使用 [Omnisearch](search-assets.md#search-assets-in-aem):

1. 選取搜尋圖示 ![搜尋圖示](assets/do-not-localize/search_icon.png) ，以顯示Omnisearch欄位。

1. 在「Omnisearch」欄位中指定您尚未明確新增至視訊的標籤。

1. 根據標籤進行搜尋。

搜尋結果會根據您指定的標籤顯示視訊資產。

您的搜尋結果是中繼資料中視訊資產與搜尋關鍵字的組合，以及以搜尋關鍵字智慧標籤的視訊資產。 但是，會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 如需詳細資訊，請參 [ [!DNL Experience Manager] 閱「使用智慧標籤瞭解搜尋結果」](smart-tags.md#understandsearch)。

## 協調視訊智慧型標籤 {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] 可讓您組織智慧型標籤，以：

* 移除指派給您品牌影片的不正確標籤。

* 確保視訊出現在搜尋結果中，以尋找最相關的標籤，以調整以標籤為基礎的視訊搜尋。 因此，它可消除不相關視訊出現在搜尋結果中的可能性。

* 指派較高的排名給標籤，以提高其與視訊的相關性。 促銷視訊的標籤會增加當根據該標籤執行搜尋時，在搜尋結果中顯示視訊的機率。

如需如何協調資產智慧標籤的詳細資訊，請參閱「管 [理智慧標籤」](smart-tags.md#manage-smart-tags-and-searches)。

![協調視訊智慧型標籤](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>重新處理資產時，不會記住使用「管 [理智慧標籤](smart-tags.md#manage-smart-tags-and-searches) 」中步驟協調的任何標籤。 原始標籤集會再次顯示。

## 選擇退出視訊智慧標籤 {#opt-out-video-smart-tagging}

當自動標籤視訊與建立縮圖和擷取中繼資料等其他資產處理工作同時執行時，可能會很耗時。 若要加速資產處理，您可以在資料夾層級上傳時選擇退出視訊智慧型標籤。

若要針對上傳至特定資料夾的資產，選擇退出自動產生視訊智慧標籤：

1. 開啟資 [!UICONTROL 料夾「屬性] 」中的「資產處 [!UICONTROL 理」標籤]。

1. 在「 [!UICONTROL 視訊的智慧標籤] 」功能表中，預 [!UICONTROL 設會選取「繼承] 」選項，並啟用視訊智慧標籤。

   選擇「繼 [!UICONTROL 承] 」選項時，繼承的資料夾路徑以及設定為「啟用」或「禁用」的資訊也會 [!UICONTROL 顯示]。

   ![停用視訊智慧標籤](assets/disable-video-tagging.png)

1. 選取「 [!UICONTROL 停用] 」以選擇退出智慧標籤上傳至資料夾的視訊。

>[!IMPORTANT]
>
>如果您在上傳時選擇不在資料夾上標籤視訊，並想在上傳後智慧標籤視訊，則 **[!UICONTROL Enable Smart Tags for Videos]** from [!UICONTROL Asset ProcessingTab of Folder] Properties並使用 [!UICONTROL Reprocess][](#smart-tag-existing-videos) Recoss智慧標籤選擇新增智慧標籤至視訊。

## 信賴分數 {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] 套用物件和動作智慧標籤的最小信賴臨界值，以避免每個視訊資產的標籤過多，進而降低索引速度。 您的資產搜尋結果會根據信賴分數進行排名，這通常會改善搜尋結果，超出任何視訊資產的指派標籤檢查所暗示的程度。 不正確的標籤通常會有低可信度分數，因此很少出現在資產的「智慧標籤」清單頂端。

動作和物件標籤的預設臨界值 [!DNL Adobe Experience Manager] 為0.7（值應介於0和1之間）。 如果某些視訊資產未由特定標籤標籤，則表示演算法對預測標籤的信心低於70%。 預設臨界值不一定對所有使用者都是最佳值。 因此，您可以變更OSGI設定中的信賴分數值。

若要透過Cloud Manager將信賴分數OSGI設定新增至部署 [!DNL Adobe Experience Manager] 為雲端服務的專案：

* 在專案 [!DNL Adobe Experience Manager] 中(自`ui.config` Archetype 24或之前 `ui.apps`), `config.author` OSGi組態包含名為的組態檔， `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` 其內容如下：

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

* 目前尚未支援訓練智慧型標籤服務（或增強型智慧型標籤）來標籤視訊資產。

* 未顯示標籤進度。

* 只有大小不超過300 MB的視訊才適合進行標籤。 Adobe Sensei服務會智慧標籤符合此准則的視訊，並略過標籤資料夾中的其他視訊。

* 只有這些檔案格式（和支援的轉碼器）的視訊— MP4(H264/AVC)、MKV(H264/AVC)、MOV(H264/AVC、Motion JPEG)、AVI(indeo4)、FLV(H264/AVC、vp6f)和WMV(WMV2)-可以標籤。

>[!MORELIKETHIS]
>
>* [管理智慧標籤和資產搜尋](smart-tags.md#manage-smart-tags-and-searches)
>* [訓練智慧型標籤服務並標籤您的影像](smart-tags.md)


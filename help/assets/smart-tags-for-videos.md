---
title: 為您視訊資產加上智慧型標記
description: Experience Manager會使用 [!DNL Adobe AI]自動將內容與描述性智慧標籤新增至影片。
feature: Smart Tags,Tagging
role: Admin,User
exl-id: 87d0eea2-83a1-4cfa-a4a5-425d0e8abba6
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---

# 為您視訊資產加上智慧型標記 {#video-smart-tags}

對新內容的需求日益增長，需要減少手動工作，以迅速提供引人入勝的數位體驗。 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]支援使用人工智慧自動標籤視訊資產。 手動標籤視訊可能很耗時。 不過，[!DNL Adobe AI]支援的視訊智慧標籤功能會使用人工智慧模型來分析視訊內容並將標籤新增至視訊資產。 從而減少DAM使用者為客戶提供豐富體驗的時間。 Adobe的機器學習服務為影片產生兩組標籤。 而其中一組對應於該視訊中的物件、場景和屬性；另一組則與飲酒、跑步和慢跑等動作相關。

在[!DNL Adobe Experience Manager]中預設已啟用視訊標籤作為[!DNL Cloud Service]。 不過，您可以在資料夾上[選擇退出視訊智慧標籤](#opt-out-video-smart-tagging)。 當您上傳新視訊或重新處理現有視訊時，會自動標籤視訊。 [!DNL Experience Manager]也會建立縮圖，並擷取視訊檔案的中繼資料。 智慧標籤在資產[屬性](#confidence-score-video-tag)中以其[!UICONTROL 信賴分數]的遞減順序顯示。

## 上傳時的智慧標籤影片 {#smart-tag-assets-on-ingestion}

當您[以](add-assets.md#upload-assets)形式將視訊資產[!DNL Adobe Experience Manager]上傳至[!DNL Cloud Service]時，系統會處理視訊。 處理完成後，請參閱資產[!UICONTROL 屬性]頁面的[!UICONTROL 基本]標籤。 智慧型標籤會自動新增至[!UICONTROL 智慧型標籤]下的視訊。 資產微服務利用[!DNL Adobe AI]建立這些智慧標籤。

![智慧標籤已新增至視訊，並可在資產屬性的「基本」標籤中看到](assets/smart-tags-added-to-videos.png)

套用的智慧標籤會以[信賴分數](#confidence-score-video-tag)的遞減順序排序，在[!UICONTROL 智慧標籤]中針對物件和動作標籤進行組合。

>[!IMPORTANT]
>
>建議您檢閱這些自動產生的標籤，以確保其符合您的品牌及其值。

## 為DAM中的現有影片加上智慧標籤 {#smart-tag-existing-videos}

DAM中現有的視訊資產不會自動加上智慧標籤。 您必須手動[!UICONTROL 重新處理Assets]，才能為其產生智慧標籤。

若要以智慧標籤視訊資產，或資產存放庫中已存在資產的資料夾（包括子資料夾），請遵循下列步驟：

1. 選取[!DNL Adobe Experience Manager]標誌，然後從[!UICONTROL 導覽]頁面選取資產。

1. 選取[!UICONTROL 檔案]以顯示Assets介面。

1. 導覽至您要套用智慧標籤的資料夾。

1. 選取整個資料夾或特定視訊資產。

1. 選取![重新處理資產圖示](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL 重新處理Assets]圖示，並選取[!UICONTROL 完整處理]選項。

<!-- TBD: Limit size -->

![重新處理資產，以將標籤新增至現有的DAM存放庫](assets/reprocess.gif)

程式完成後，請導覽至資料夾內任何視訊資產的[!UICONTROL 屬性]頁面。 自動新增的標籤會顯示在[!UICONTROL 基本]索引標籤的[!UICONTROL 智慧標籤]區段中。 這些套用的智慧標籤會以[信賴分數](#confidence-score-video-tag)的遞減順序排序。

## 搜尋標籤的影片 {#search-smart-tagged-videos}

若要根據自動產生的智慧標籤搜尋視訊資產，請使用[Omnisearch](search-assets.md#search-assets-in-aem)：

1. 選取搜尋圖示![搜尋圖示](assets/do-not-localize/search_icon.png)以顯示Omnisearch欄位。

1. 在Omnisearch欄位中指定您尚未明確新增至視訊的標籤。

1. 根據標籤進行搜尋。

搜尋結果會根據您指定的標籤顯示視訊資產。

您的搜尋結果為中繼資料中具有已搜尋關鍵字的視訊資產的組合，以及以已搜尋關鍵字作為智慧標籤的視訊資產。 不過，符合中繼資料欄位中所有搜尋字詞的搜尋結果會先顯示，接著顯示符合智慧標籤中任何搜尋字詞的搜尋結果。 如需詳細資訊，請參閱[瞭解具有智慧標籤的 [!DNL Experience Manager] 搜尋結果](smart-tags.md#understand-search)。

## 稽核視訊智慧標籤 {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager]可讓您組織智慧標籤，以：

* 移除指派給品牌影片的不準確標籤。

* 確保您的影片出現在最相關標籤的搜尋結果中，以精簡標籤式視訊搜尋。 因此，它可避免無關的影片出現在搜尋結果中。

* 將較高的排名指派給標籤，以增加其與視訊的相關性。 升級視訊標籤會增加視訊在根據該標籤執行搜尋時，出現在搜尋結果中的機會。

若要進一步瞭解如何稽核資產的智慧標籤，請參閱[管理智慧標籤](smart-tags.md#manage-smart-tags-and-searches)。

![稽核視訊智慧標籤](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>重新處理資產時，不會記住任何使用[管理智慧標籤](smart-tags.md#manage-smart-tags-and-searches)中的步驟仲裁的標籤。 原始標籤集會再次顯示。

## 選擇退出視訊智慧標籤 {#opt-out-video-smart-tagging}

由於視訊的自動標籤與其他資產處理工作（例如建立縮圖及擷取中繼資料）並行執行，因此非常耗時。 若要加快資產處理速度，您可以在資料夾層級上傳時選擇退出視訊智慧標籤。

若要選擇退出針對已上傳至特定資料夾的資產自動產生視訊智慧標籤：

1. 開啟資料夾[!UICONTROL 屬性]中的[!UICONTROL 資產處理]索引標籤。

1. 在[!UICONTROL 視訊智慧標籤]功能表中，[!UICONTROL 已繼承]選項預設為選取，且視訊智慧標籤已啟用。

   選取[!UICONTROL 繼承]選項時，繼承的資料夾路徑也會與資訊一起顯示，無論其設定為[!UICONTROL 啟用]或[!UICONTROL 停用]。

   ![停用視訊智慧標籤](assets/disable-video-tagging.png)

1. 選取[!UICONTROL 停用]以選擇退出上傳至資料夾的視訊的智慧標籤。

>[!IMPORTANT]
>
>如果您在上傳時選擇不標籤資料夾上的影片，並想在上傳後為影片加上智慧標籤，請從資料夾&#x200B;**[!UICONTROL 屬性]**&#x200B;的[!UICONTROL 資產處理]索引標籤中[!UICONTROL 啟用影片的智慧標籤]，並使用[[!UICONTROL 重新處理資產]選項](#smart-tag-existing-videos)將智慧標籤新增到影片中。

## 信賴分數 {#confidence-score-video-tag}

[!DNL Adobe Experience Manager]套用物件和動作智慧標籤的最低信賴臨界值，以避免每個視訊資產有太多標籤，這會減慢索引速度。 您的資產搜尋結果會根據可信度分數進行排名，這通常會改善搜尋結果，超越任何視訊資產的指派標籤檢查所建議的範圍。 不準確的標籤通常會有較低的信賴分數，因此很少會出現在資產的智慧標籤清單頂端。

[!DNL Adobe Experience Manager]中動作和物件標籤的預設臨界值為0.7 （值應介於0和1之間）。 如果某些視訊資產未使用特定標籤進行標籤，則表示演演算法對於預測標籤的信賴度低於70%。 預設臨界值並非總是適用於所有使用者。 因此，您可以在OSGI設定中變更信賴分數值。

若要透過[!DNL Adobe Experience Manager]將信賴分數OSGI設定新增至部署至[!DNL Cloud Service]做為[!DNL Cloud Manager]的專案：

* 在[!DNL Adobe Experience Manager]專案（`ui.config`自Archetype 24或先前`ui.apps`）中，`config.author` OSGi設定包含名為`com.adobe.cq.assetcompute.impl.aisdk.AISdkImpl.cfg.json`的設定檔，其內容如下：

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>手動標籤被指派為100%的信賴度（最大信賴度）。 因此，如果影片資產具有符合搜尋查詢的手動標籤，則會先顯示符合搜尋查詢的智慧標籤。

## 限制 {#video-smart-tagging-limitations}

* 您無法訓練使用任何特定視訊將智慧標籤套用至視訊的服務。 它可與預設[!DNL Adobe AI]設定搭配使用。

* 標籤進度不會顯示。

* 系統只會自動標籤檔案大小小於300 MB的視訊。 [!DNL Adobe AI]服務會略過較大大小的視訊檔案。

* 只標籤[智慧標籤](/help/assets/smart-tags.md#smart-tags-supported-file-formats)中提及的檔案格式視訊和支援的轉碼器。

>[!MORELIKETHIS]
>
>* [管理智慧標籤和資產搜尋](smart-tags.md#manage-smart-tags-and-searches)
>* [訓練智慧標籤服務並標籤您的影像](smart-tags.md)

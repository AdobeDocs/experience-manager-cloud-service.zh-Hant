---
title: 智慧標籤視頻資產
description: Experience Manager使用 [!DNL Adobe Sensei]。
feature: Smart Tags,Tagging
role: Admin,User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 0%

---

# 智慧標籤視頻資產 {#video-smart-tags}

對新內容的不斷增長需求要求減少手動工作，以便在短時間內提供引人注目的數字型驗。 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 支援使用人工智慧對視頻資產進行自動標籤。 手動標籤視頻可能非常耗時。 但是， [!DNL Adobe Sensei] 支援視頻智慧標籤功能使用人工智慧模型來分析視頻內容並向視頻資產添加標籤。 從而縮短DAM用戶為其客戶提供豐富體驗的時間。 Adobe的機器學習服務為一個視頻生成兩組標籤。 而一組則與視頻中的對象、場景和屬性相對應；另一組則與飲酒，跑步，慢跑等動作有關。

預設情況下，在 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service]。 但是， [選擇退出視頻智慧標籤](#opt-out-video-smart-tagging) 資料夾。 當您上傳新視頻或重新處理現有視頻時，會自動標籤視頻。 [!DNL Experience Manager] 同時建立縮覽圖並提取視頻檔案的元資料。 智慧標籤按其降序顯示 [置信度](#confidence-score-video-tag) 資產 [!UICONTROL 屬性]。

## 上傳時的智慧標籤視頻 {#smart-tag-assets-on-ingestion}

當你 [上載視頻資產](add-assets.md#upload-assets) 至 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service]，處理視頻。 處理完成後，請參閱 [!UICONTROL 基本] 頁籤 [!UICONTROL 屬性] 的子菜單。 智慧標籤會自動添加到視頻的 [!UICONTROL 智慧標籤]。 資產微服務利用 [!DNL Adobe Sensei] 建立這些智慧標籤。

![智慧標籤會添加到視頻中，並可在資產屬性的「基本」頁籤中查看](assets/smart-tags-added-to-videos.png)

應用的智慧標籤按降序排序， [置信度](#confidence-score-video-tag)，組合用於對象和操作標籤，在 [!UICONTROL 智慧標籤]。

>[!IMPORTANT]
>
>建議您查看這些自動生成的標籤，以確保它們符合您的品牌及其價值。

## 智慧標籤DAM中的現有視頻 {#smart-tag-existing-videos}

DAM中已有的視頻資產不是自動智慧標籤的。 你需要 [!UICONTROL 重新處理資產] 手動為它們生成智慧標籤。

要智慧標籤資源庫中已存在的資源的視頻資產或資料夾（包括子資料夾），請執行以下步驟：

1. 選擇 [!DNL Adobe Experience Manager] 標識，然後從 [!UICONTROL 導航] 的子菜單。

1. 選擇 [!UICONTROL 檔案] 顯示「資產」介面。

1. 導航到要應用智慧標籤的資料夾。

1. 選擇整個資料夾或特定視頻資產。

1. 選擇 ![「重新處理資產」表徵圖](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL 重新處理資產] 表徵圖，然後選擇 [!UICONTROL 完整流程] 的雙曲餘切值。

<!-- TBD: Limit size -->

![重新處理資產以將標籤添加到現有DAM儲存庫的視頻](assets/reprocess.gif)

流程完成後，導航到 [!UICONTROL 屬性] 資料夾中任何視頻資源的頁面。 在中可看到自動添加的標籤 [!UICONTROL 智慧標籤] 部分 [!UICONTROL 基本] 頁籤。 這些應用的智慧標籤按降序排序， [置信度](#confidence-score-video-tag)。

## 搜索標籤的視頻 {#search-smart-tagged-videos}

要根據自動生成的智慧標籤搜索視頻資產，請使用 [奧姆尼瑟克](search-assets.md#search-assets-in-aem):

1. 選擇搜索表徵圖 ![搜索表徵圖](assets/do-not-localize/search_icon.png) 的子菜單。

1. 在Omnisearch欄位中指定尚未顯式添加到視頻的標籤。

1. 根據標籤進行搜索。

搜索結果將根據您指定的標籤顯示視頻資產。

搜索結果是元資料中搜索關鍵字的視頻資產和用搜索關鍵字智慧標籤的視頻資產的組合。 但是，首先顯示與元資料欄位中的所有搜索項相匹配的搜索結果，然後顯示與智慧標籤中的任何搜索項相匹配的搜索結果。 有關詳細資訊，請參見 [瞭解 [!DNL Experience Manager] 使用智慧標籤搜索結果](smart-tags.md#understand-search)。

## 中等視頻智慧標籤 {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] 允許您將智慧標籤設定為：

* 刪除分配給您的品牌視頻的不準確標籤。

* 通過確保您的視頻顯示在搜索結果中以查找最相關的標籤，優化基於標籤的視頻搜索。 因此，它消除了不相關視頻出現在搜索結果中的可能性。

* 為標籤指定更高的等級以增強其與視頻的相關性。 當基於該標籤執行搜索時，升級視頻的標籤增加了在搜索結果中出現該視頻的可能性。

要瞭解有關如何調整資產智慧標籤的詳細資訊，請參閱 [管理智慧標籤](smart-tags.md#manage-smart-tags-and-searches)。

![中等視頻智慧標籤](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>使用中的步驟審核的任何標籤 [管理智慧標籤](smart-tags.md#manage-smart-tags-and-searches) 不會因為資產的重新處理而被記住。 將再次顯示原始標籤集。

## 選擇退出視頻智慧標籤 {#opt-out-video-smart-tagging}

由於自動標籤視頻與建立縮略圖和提取元資料等其他資產處理任務並行運行，因此可能非常耗時。 要加快資產處理，您可以選擇在資料夾級別上載時不使用視頻智慧標籤。

為上載到特定資料夾的資產選擇不生成自動視頻智慧標籤：

1. 開啟 [!UICONTROL 資產處理] 資料夾 [!UICONTROL 屬性]。

1. 在 [!UICONTROL 視頻智慧標籤] 菜單， [!UICONTROL 繼承] 選項，並啟用視頻智慧標籤。

   當 [!UICONTROL 繼承] 選項，繼承的資料夾路徑以及是否設定為的資訊也可見 [!UICONTROL 啟用] 或 [!UICONTROL 禁用]。

   ![禁用視頻智慧標籤](assets/disable-video-tagging.png)

1. 選擇 [!UICONTROL 禁用] 選擇不對上傳到資料夾的視頻進行智慧標籤。

>[!IMPORTANT]
>
>如果您選擇在上載時不在資料夾上標籤視頻，並希望在上載後智慧標籤視頻，則 **[!UICONTROL 為視頻啟用智慧標籤]** 從 [!UICONTROL 資產處理] 頁籤 [!UICONTROL 屬性] 使用 [[!UICONTROL 重新處理資產] 選項](#smart-tag-existing-videos) 添加智慧標籤。

## 信心評分 {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] 對對象和操作智慧標籤應用最小置信度閾值以避免每個視頻資產的標籤過多，這會降低索引速度。 您的資產搜索結果會根據置信度得分進行排序，這通常會改善搜索結果，超出對任何視頻資產的已分配標籤的檢查所建議的範圍。 不準確的標籤通常具有低置信度分數，因此它們很少出現在資產的「智慧標籤」清單的頂部。

中操作和對象標籤的預設閾值 [!DNL Adobe Experience Manager] 為0.7（應為介於0和1之間的值）。 如果某些視頻資源沒有被特定標籤標籤，則表明該算法對預測標籤的信心小於70%。 預設閾值可能並不總是對所有用戶最佳。 因此，您可以更改OSGI配置中的置信度分數值。

將置信度分數OSGI配置添加到部署到的項目 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 通 [!DNL Cloud Manager]:

* 在 [!DNL Adobe Experience Manager] 項目(P)`ui.config` 從原型24開始，或者之前 `ui.apps`) `config.author` OSGi配置，包括名為 `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` 內容如下：

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>手動標籤的置信度為100%（最大置信度）。 因此，如果存在具有與搜索查詢匹配的手動標籤的視頻資產，則在匹配搜索查詢的智慧標籤之前顯示這些視頻資產。

## 限制 {#video-smart-tagging-limitations}

* 您不能使用任何特定視頻培訓將智慧標籤應用於視頻的服務。 它與預設 [!DNL Adobe Sensei] 的子菜單。

* 未顯示標籤進度。

* 只有檔案大小小於300 MB的視頻才會自動標籤。 的 [!DNL Adobe Sensei] 服務跳過大小較大的視頻檔案。

* 只有中提到的檔案格式和支援的編解碼器中的視頻 [智慧標籤](/help/assets/smart-tags.md#smart-tags-supported-file-formats) 標籤。

>[!MORELIKETHIS]
>
>* [管理智慧標籤和資產搜索](smart-tags.md#manage-smart-tags-and-searches)
>* [培訓智慧標籤服務並標籤您的映像](smart-tags.md)


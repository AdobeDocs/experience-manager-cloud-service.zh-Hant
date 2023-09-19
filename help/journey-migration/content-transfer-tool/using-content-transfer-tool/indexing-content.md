---
title: 移轉內容後建立索引
description: 瞭解移轉程式如何在目的地Cloud Service例項上為擷取的內容建立索引。
source-git-commit: 22c5cbf300bb0b3b0db04fcfa669dde44197c326
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 8%

---

# 移轉內容後建立索引 {#Indexing-content}

## 索引 {#aem-indexing-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_indexing"
>title="內容編製索引"
>abstract="AEM 編製索引是指將內容移轉到 Cloud Service 例項後編製該內容索引。 必須編製索引才能支援在該例項上搜尋內容。"

一旦Cloud Acceleration Manager完成將內容擷取至您的Cloud Service例項中，即可使用。 一開始不會將內容編列索引，這可能會導致環境不穩定，發生無法搜尋的內容和效能降低等問題。
為獲得執行個體上的最佳效能，移轉程式將自動開始編制內容索引。 除了監視索引進度外，沒有其他要做的事。

> 如需如何開始內嵌的詳細資訊，請參閱 [將內容擷取至Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

下列步驟顯示編制索引期間可在UI中看到的一般流程。 有些標籤在工具提示中提供有用的內容，因此請務必將滑鼠移至專案上，以進一步瞭解目前的索引狀態。

若要開始，請前往Cloud Acceleration Manager 。 按一下您的專案卡，然後按一下「內容轉移」卡。 瀏覽至 **內嵌工作**
並檢視列出的工作。

>[!NOTE]
>您可以使用內嵌工作的動作，透過……下拉式清單來檢視或下載索引記錄檔。 記錄檔將可在
> 索引工作完成後，「索引記錄」動作區段

### 擱置中

這是內嵌執行時、索引工作開始之前，內嵌工作列的顯示方式。 使用者無需採取任何動作。 如果擷取因任何原因而失敗，則會取消索引工作的佇列，而不會啟動。

![影像](/help/journey-migration/content-transfer-tool/assets-indexing/pending.png)

### 正在執行

擷取成功時，索引工作會自動啟動。 擷取工作列將會顯示AEM索引狀態的進度圖示。 您可以開啟持續時間對話方塊以檢視工作進度。

![影像](/help/journey-migration/content-transfer-tool/assets-indexing/running.png)

### 完成

當索引工作成功時，執行個體已準備好以最佳效能使用。 此時，索引工作記錄檔將可供檢視或下載，以便進行檢查。

![影像](/help/journey-migration/content-transfer-tool/assets-indexing/complete.png)

### 錯誤次數

建立目的地Cloud Service執行個體的索引很可能成功。 某些情況下，作業可能會失敗，而擷取工作列會顯示如下。 在所有情況下，將滑鼠懸停在失敗狀態上，可以找到失敗的一些詳細資訊，它可能會提供詳細資訊，幫助您決定後續步驟。 此時，索引工作記錄檔將可供檢視或下載，以幫助發現失敗的來源。 如果下一個步驟不清楚，請聯絡Adobe支援，提供擷取和索引記錄的詳細資訊。

![影像](/help/journey-migration/content-transfer-tool/assets-indexing/failed.png)

## 下一步 {#whats-next}

一旦目標雲端服務執行個體編列索引後，您就可以檢視編列索引工作的記錄，並尋找詳細資訊和錯誤。

移轉完成。 可以開始測試和驗證目的地雲端服務執行個體。

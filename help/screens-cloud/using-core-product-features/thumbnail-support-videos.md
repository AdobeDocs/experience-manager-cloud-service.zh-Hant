---
title: 螢幕中視訊的縮圖支援作為Cloud Service
description: 本頁面說明如何將螢幕中的視訊縮圖支援新增為Cloud Service。
hide: true
index: false
source-git-commit: ea96e811c0164e3cc7d323e734c1617d3c0e9308
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# 影片的縮圖支援 {#thumbnail-support-videos}

## 簡介 {#introduction}

內容作者可以定義視訊的縮圖，以便影像可作為預留位置，並在適當團隊完成實際視訊時，正確測試內容播放和鎖定目標。 當視訊播放失敗時，也可以使用影像。

新增對視訊元件上縮圖影像的支援，讓客戶能在頻道中正確新增有效的元件（含實際內容），並在實際傳送視訊前執行任何鎖定目標設定。

>[!NOTE]
>如果在視訊元件上設定縮圖影像，則會在播放器上視訊播放失敗時播放。 這可讓您將所需的訊息傳送給對象（透過播放內容），而非完全略過訊息。

縮圖支援可讓您：

* 當影片尚未準備好，或您不一定想要在播放器上測試大型資產下載時，準備管道體驗

* 如果裝置上發生播放問題，請設定後援機制。

## 在影片中使用縮圖 {#using-thumbnails}

請依照下列步驟，在影片中使用縮圖：

1. 導覽至現有的Screens頻道或建立新頻道。

   >[!NOTE]
   >若要了解如何建立管道及將內容新增至管道，請參閱[在Screens中建立和管理管道作為Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en)。

1. 選取通道，然後按一下動作列中的&#x200B;**Edit**&#x200B;以開啟編輯器。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. 添加或編輯現有視頻元件，如下圖所示。

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. 編輯視訊元件屬性。

1. 從資產選擇器拖曳影像至縮圖拖放區域。

1. 預覽通道。

1. 如果元件上設定了視訊，則視訊會播放。 如果沒有，且已設定縮圖，則會播放縮圖。 否則，系統會將元件視為未設定，且會略過

## 在影片中使用縮圖時支援的使用案例 {#understand-use-case}

在影片中使用縮圖時，請參閱下列使用案例。

視訊元件包含：

* *不會* 略過任何設定

* *只有縮圖* 會播放縮圖

* *視訊和縮圖視* 訊都會播放視訊

* *如果* 有播放錯誤，視訊會傳送播放縮圖，或是略過至下一個項目，以備未設定縮圖時使用

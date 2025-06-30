---
title: 在Experience Manager Assets中檢視及管理轉譯
description: 瞭解AEM Assets和Dynamic Media如何使用靜態和動態影像轉譯，簡化有效的影像管理。
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---

# 在Experience Manager Assets中檢視及管理轉譯{#renditions}

Adobe Experience Manager (AEM)中的轉譯是數位資產（例如影像）的自訂版本，專為不同裝置和平台而設計，以確保最佳效能。 AEM可協助您輕鬆建立和管理這些轉譯，進而改善使用者體驗。 您可以建立縮圖、針對網頁或行動裝置最佳化影像、新增浮水印、檢視及下載動態轉譯或智慧型裁切轉譯，以及執行更多工作。

Dynamic Media影像預設集和智慧型裁切轉譯可促進符合品牌標準的系統影像管理，進而實現品牌凝聚力的最大化。 這可簡化快速找到及視需要使用動態影像轉譯的程式，而且不需要任何管理員存取。

轉譯分為靜態與動態兩類，每種型別各有獨特功能，本節將對此進行詳細討論。

## 靜態轉譯 {#static-renditions}

靜態轉譯是數位資產的預先產生版本，通常在資產擷取或修改期間建立。 這些轉譯已針對特定用途和平台進行最佳化，例如網頁縮圖、回應式設計的行動友好格式，或列印的高解析度版本，以確保有效率且一致的體驗。
瞭解如何在Experience Manager Assets中[檢視及下載靜態轉譯](#view-and-download-static-renditions)。

### 檢視和下載靜態轉譯{#view-and-download-static-renditions}

若要檢視並下載資產轉譯，請遵循下列步驟：

1. 在Assets檢視上，按一下&#x200B;**Assets**，瀏覽至資料夾，選取資產，然後按一下&#x200B;**詳細資料**。
1. 按一下右窗格中可用的轉譯圖示。
1. 選取要預覽的轉譯，然後按一下![下載圖示](/help/assets/assets/download-icon.svg)進行下載。

   ![檢視及下載動態轉譯](/help/assets/assets/view-download-static-rendition.png)

## 動態轉譯 {#dynamic-renditions}

動態轉譯是資產的自訂版本，可即時建立以符合特定需求，例如根據裝置解析度調整影像大小或裁切以符合不同的外觀比例。
這些轉譯可讓組織提供個人化和最佳化的體驗，以滿足不同的受眾需求。 您可以在Experience Manager Assets中檢視和下載動態轉譯。

## Dynamic Media轉譯 {#dynamic-media-renditions}

### 開始之前

* 您必須是授權的AEM Dynamic Media使用者。
* 使用[!UICONTROL 管理員檢視]設定：
   * [智慧型裁切影像設定檔](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [影像預設集](/help/assets/dynamic-media/managing-image-presets.md)

  您可以[稍後切換檢視](/help/assets/assets-view-introduction.md#how-to-access-assets-view)以在Assets檢視中預覽動態轉譯。
* 將資產發佈至Dynamic Media，以便在Assets檢視中使用Dynamic Media轉譯。 如需詳細資訊，請參閱[將Assets發佈到AEM和Dynamic Media](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm)。


### 檢視和下載Dynamic Media轉譯 {#view-download-dm-renditions}

若要在Experience Manager Assets中檢視或下載影像的動態轉譯，請遵循下列步驟：

1. 移至&#x200B;**[!UICONTROL Assets管理]** > **[!UICONTROL Assets]**。

1. 導覽至適用的資產資料夾。

1. 按一下您需要檢視的資產，然後按一下&#x200B;**[!UICONTROL 詳細資料]**。

1. 在右方功能表中，按一下&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;圖示。 **[!UICONTROL Dynamic Media]**&#x200B;面板會顯示Dynamic Media和智慧型裁切轉譯。

   ![動態轉譯](/help/assets/assets/dm-scene7-renditions.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. 選取要預覽的轉譯，然後按一下&#x200B;**複製URL**&#x200B;以複製所選轉譯的URL。 按一下「**下載轉譯**」即可下載影像資產的轉譯。
1. 選取要預覽的智慧型裁切轉譯，然後按一下「複製URL」**&#x200B;**&#x200B;以複製所選轉譯的URL。
1. 按一下![下載圖示](assets/do-not-localize/download-icon.png)，將所有可用的智慧型裁切轉譯下載為單一zip檔案。
   ![下載圖示](/help/assets/assets/smartcrop-rendition.png)

   >[!NOTE]
   >
   >這些轉譯專案僅適用於影像資產。

## 具有OpenAPI功能轉譯的Dynamic Media {#dm-with-openapi-renditions}

### 開始之前 {#prereqs-dm-with-openapi-renditions}

* 您必須是授權的AEM Dynamic Media使用者。
* Assets必須獲得核准，才能顯示具有OpenAPI功能轉譯的Dynamic Media。 如需詳細資訊，請參閱[在Experience Manager中核准資產](/help/assets/approve-assets.md#copy-delivery-url-approved-assets)
* 必須在您的AEM as a Cloud Service執行個體上啟用具有OpenAPI功能的Dynamic Media 。

### 使用OpenAPI功能檢視Dynamic Media轉譯 {#view-download-dm-with-openapi-renditions}

1. 選取資產並按一下&#x200B;**詳細資料**。
1. 按一下右窗格中可用的Dynamic Media圖示。 「動態媒體」面板為所有資產型別顯示「具有OpenAPI功能的動態媒體」轉譯。
   ![下載圖示](/help/assets/assets/dm-with-open-api-copy-url.png)
1. 選取&#x200B;**Dynamic Media with OpenAPI**&#x200B;選項，然後按一下&#x200B;**複製URL**&#x200B;以複製資產的傳遞URL。



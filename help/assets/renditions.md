---
title: 在Experience Manager Assets中檢視及管理轉譯
description: 瞭解AEM Assets和Dynamic Media如何運用靜態和動態影像轉譯，簡化有效的影像管理。
exl-id: 006dc493-c400-4d0f-b314-c1978582b7fb
feature: Renditions
role: User
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 在Experience Manager Assets中檢視及管理轉譯{#renditions}

Adobe Experience Manager (AEM)中的轉譯是數位資產（例如影像）的自訂版本，專為不同裝置和平台而設計，以確保最佳效能。 AEM可協助您輕鬆建立和管理這些轉譯，進而提升使用者體驗。 您可以建立縮圖、針對網頁或行動裝置最佳化影像、新增浮水印、檢視及下載動態轉譯或智慧型裁切轉譯，以及執行更多工作。

Dynamic Media影像預設集和智慧型裁切轉譯可根據品牌標準，促進系統化的影像管理，進而實現品牌凝聚力的最大化。 這可簡化快速找到及視需要使用動態影像轉譯的程式，而且不需要任何管理員存取。

轉譯分為靜態與動態兩類，每種型別各有獨特功能，本節將對此進行詳細討論。

## 靜態轉譯 {#static-renditions}

靜態轉譯是數位資產的預先產生版本，通常在資產擷取或修改期間建立。 這些轉譯已針對特定用途和平台進行最佳化，例如網頁縮圖、回應式設計的行動友好格式，或列印的高解析度版本，以確保有效率且一致的體驗。
瞭解 [如何檢視和下載](#view-dynamic-renditions) 中的靜態轉譯 [!DNL Experience Manager Assets].

## 動態轉譯 {#dynamic-renditions}

動態轉譯是資產的自訂版本，可即時建立以符合特定需求，例如根據裝置解析度調整影像大小或裁切以符合不同的外觀比例。
這些轉譯可讓組織提供個人化和最佳化的體驗，以滿足不同的受眾需求。 您可以在中檢視及下載動態轉譯 [!DNL Experience Manager Assets].

### 開始之前

* 您必須是授權的AEM Dynamic Media使用者。

* 使用 [!UICONTROL 管理員檢視] 若要設定：
   * [智慧型裁切影像設定檔](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)
   * [影像預設集](/help/assets/dynamic-media/managing-image-presets.md)

  您可以 [切換檢視](/help/assets/assets-view-introduction.md#how-to-access-assets-view) 以稍後在「資產」檢視中預覽動態轉譯。

### 檢視和下載動態轉譯 {#view-renditions}

若要在中檢視或下載影像的動態轉譯 [!DNL Experience Manager Assets]，請遵循下列步驟：

1. 前往 **[!UICONTROL 資產管理]** > **[!UICONTROL 資產]**.

1. 導覽至適用的資產資料夾。

1. 按一下您需要檢視的影像，然後按一下 **[!UICONTROL 詳細資料]**.

1. 在右側功能表中，按一下 **[!UICONTROL 轉譯]**. <br> 此 **[!UICONTROL 轉譯]** 面板隨即開啟，並提供 **[!UICONTROL 動態]** 和 **[!UICONTROL 智慧型裁切]** 轉譯。

   ![動態轉譯](assets/preset_smart_crop.png)
   <!-- ![dynamic renditions](assets/preset_smart_crop_view.png) -->

1. 按一下您需要檢視或下載的轉譯。

1. 按一下 ![下載圖示](assets/do-not-localize/download-icon.png) 圖示加以存取（位於需要下載的動態轉譯旁）。 <br> 或者，您可以選取影像轉譯，然後按一下 **[!UICONTROL 下載轉譯]** 底部的「 」選項。

   您可以按一下 ![下載圖示](assets/do-not-localize/download-icon.png) 圖示位於頂端 **[!UICONTROL 智慧型裁切]** 轉譯區段，可下載該資產所有可用的智慧型裁切轉譯。

>[!NOTE]
>
>只有當資產是從「管理員」檢視上傳時，動態轉譯才會顯示。

---
title: 預覽 3D 資產
description: 瞭解如何在Experience Manager中預覽3D資產。
contentOwner: Rick Brough
feature: 3D Assets
role: User
exl-id: e873bd25-f841-4063-824f-7e48f40bb678
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 5%

---

# 在Adobe Experience Manager中預覽3D資產{#previewing-3d-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/previewing-3d-assets.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

Experience Manager Assets支援3D資產的擷取、管理、預覽和傳送。

您可以使用自動產生的縮圖轉譯或互動式3D檢視器來預覽3D資產。 您可從Experience Manager的資產詳細資訊頁面取得互動式3D檢視器。 該檢視器包含一系列互動式相機控制項，可供您旋轉、縮放和平移3D場景。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Experience Manager中縮圖預覽的支援格式{#supported-thumbnail-previewing-assets}

Experience Manager預設會產生下列檔案格式的縮圖：

| 3D副檔名 | 檔案格式 | MIME型別 | 備註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary |  |
| FBX | Autodesk FBX | application/octet-stream |  |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif |  |
| 3DS | 3D Studio模型 | application/x-3ds |  |
| 美元z | 通用場景描述 | model/vnd.usdz+zip |  |

## Experience Manager中支援的互動式3D預覽格式{#supported-3d-previewing-assets}

Experience Manager原生支援下列檔案格式的Interactive 3D預覽：

| 3D副檔名 | 檔案格式 | MIME型別 | 備註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary |  |
| GLTF | 總帳傳輸格式 | model/gltf+json | 請參閱下方的&#x200B;**附註**。 |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體成型 | application/vnd.ms-pki.stl |  |


>[!NOTE]
>
>如果材質未在gLTF模型預覽中呈現，請確定它們已正確命名，並位於與模型相同的根資料夾中的`textures`資料夾中，類似於以下內容：

    資產（資料夾）
    model.gltf
    model.bin
    紋理（資料夾）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## 在Experience Manager中預覽3D資產時的效能考量事項{#performance-3d-previewing-assets}

在資產詳細資料檢視頁面中開啟3D資產所需的時間取決於多種因素，例如頻寬、影像複雜性和伺服器延遲等。

此外，使用者端電腦的功能（例如工作站、筆記型電腦或行動觸控裝置）也是您以互動方式操作相機時也必須考量的重要因素。 功能相當強大的系統，搭配良好的繪圖功能，可讓互動式3D觀賞體驗更順暢、更理想。

**若要在Experience Manager中預覽3D資產：**

1. 請確定您已將3D資產上傳至Experience Manager。
檢視[支援的3D預覽格式](#supported-3d-previewing-assets)和[上傳資產](/help/assets/manage-digital-assets.md#uploading-assets)。
1. 從Experience Manager，在&#x200B;**[!UICONTROL 導覽]**&#x200B;頁面上，前往&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。

   ![導覽頁面](/help/assets/dynamic-media/assets/navigation-assets.png)

1. 在頁面的右上角，從「檢視」下拉式清單中選取「**[!UICONTROL 卡片檢視]**」，然後導覽至您要預覽的3D資產。

   ![選取3D卡片](/help/assets/dynamic-media/assets/3d-card-select.png)
   _在「卡片檢視」中，選取您要預覽之3D資產的卡片。_

1. 選取3D資產的卡片。

   ![互動式3D預覽](/help/assets/dynamic-media/assets/3d-preview.png)
   _資產詳細資料檢視頁面中的3D資產互動式預覽。_
1. 在3D資產的資產詳細資料檢視頁面上，執行下列任一項作業：

   | 檢視 | 描述 | 滑鼠動作 | 觸控熒幕動作 |
   | --- | --- | --- | --- |
   | **轉動相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 按一下左鍵+拖曳。 | 單指按下+拖曳。 |
   | **平移相機** | 向左、向右、向上或向下平移檢視。 | 按一下右鍵+拖曳。 | 雙指按下+拖曳。 |
   | **縮放相機** | 移入和移出3D場景區域。 | 滾輪。 | 兩指捏合。 |
   | **重新將相機置中** | 將相機重新置中至3D場景中物件上的某個點。 | 按兩下。 | 連按兩下。 |
   | **重設** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點恢復到3D資產的中心。 重設也會將相機移到更近或更遠的位置，以合理的檢視大小完整顯示資產。 |   |   |
   | **全熒幕模式** | 若要進入全熒幕模式，請在頁面的右下角選取「全熒幕」圖示。 |   |   |

1. 完成後，在頁面的右上角附近，選取&#x200B;**[!UICONTROL 關閉]**。

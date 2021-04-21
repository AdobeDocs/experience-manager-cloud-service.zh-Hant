---
title: 預覽 3D 資產
description: 瞭解如何在Dynamic Media預覽3D資產。
translation-type: tm+mt
source-git-commit: 2fd39221eca36f520d0095339423ac2c6a0c322e
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 11%

---


# 在Adobe Experience Manager預覽3D資產{#previewing-3d-assets}

Experience Manager支援3D資產的上傳、傳送和互動式預覽，做為製作程式的一部分。

您可從Experience Manager中的資產詳細資料頁面取得互動式3D檢視器。 這個檢視器還包含一系列互動式相機控制項，可用來環繞、縮放和平移 3D 資產。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## 支援的Experience Manager3D預覽格式{#supported-3d-previewing-assets}

Experience Manager中的互動式3D預覽支援下列檔案格式：

| 3D副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | 模型/gltf-binary |  |
| GLTF | GL傳輸格式 | model/gltf+json | 請參閱下面的&#x200B;**注意**。 |
| OBJ | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體成形 | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 僅支援擷取；預覽無法使用。 |
| USDZ | 通用場景描述Zip封存 | model/vnd.usdz+zip | 僅支援擷取；預覽無法使用。 |

>[!NOTE]
>
>如果材料未在gLTF模型的預覽中呈現，請確保它們的命名正確，並且位於與模型相同的根資料夾中的`textures`資料夾中，如下所示：

    Asset(folder)
    model.
    gltfmodel.
    bintextures(folder)
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## 在Experience Manager中預覽3D資產時的效能考量{#performance-3d-previewing-assets}

在資產詳細資訊檢視頁面中開啟3D資產所花的時間，視頻寬、影像複雜性和伺服器延遲等因素而定。

此外，在您以互動方式操作相機時，用戶端電腦的功能（例如工作站、筆記型電腦或行動觸控裝置）也很重要。 功能相當強大的系統，具備良好的圖形功能，可讓互動式3D檢視體驗更順暢更有利。

**若要在Experience Manager中預覽3D資產：**

1. 請確定您已將3D資產上傳至Experience Manager。
請參閱[3D預覽支援的格式](#supported-3d-previewing-assets)和[上傳資產](/help/assets/manage-digital-assets.md#uploading-assets)。
1. 從Experience Manager，在&#x200B;**[!UICONTROL Navigation]**&#x200B;頁面上，點選&#x200B;**[!UICONTROL 資產>檔案]**。

   ![導覽頁面](/help/assets/dynamic-media/assets/navigation-assets.png)

1. 在頁面的右上角，從「檢視」下拉式清單中，點選「卡片檢視」 ****，然後導覽至您要預覽的3D資產。

   ![3D卡片選擇](/help/assets/dynamic-media/assets/3d-card-select.png)
   _在「卡片檢視」中，點選您要預覽的3D資產卡片。_

1. 點選3D資產的卡片。

   ![互動式3D預覽](/help/assets/dynamic-media/assets/3d-preview.png)
   _在資產詳細資訊檢視頁面中互動式預覽3D資產。_
1. 在3D資產的資產詳細資料檢視頁面上，執行下列任一項作業：

   | 檢視 | 說明 | 滑鼠動作 | 觸控螢幕動作 |
   | --- | --- | --- | --- |
   | **轉動您的相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 左鍵按一下+拖曳。 | 單指按+拖曳。 |
   | **平移您的相機** | 向左、向右、向上或向下平移您的視圖。 | 按一下滑鼠右鍵並拖曳。 | 雙指按住+拖曳。 |
   | **縮放您的相機** | 移入和移出3D場景的區域。 | 滾輪。 | 雙指夾捏。 |
   | **重新輸入您的相機** | 將相機重新輸入到3D場景中某個物件的點。 | 按兩下。 | 點兩下。 |
   | **重設** | 在頁面的右下角附近，點選「重設」圖示，將檢視目標點還原至3D資產的中央。 Reset也會使攝影機更靠近或更遠，以便以合理的檢視大小顯示整個資產。 |  |  |
   | **全螢幕模式** | 若要進入全螢幕模式，請在頁面的右下角，點選全螢幕圖示。 |  |  |

1. 完成後，在頁面右上角附近點選&#x200B;**[!UICONTROL Close]**。

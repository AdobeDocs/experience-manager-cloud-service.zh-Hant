---
title: 將視訊智慧型裁切套用至核准的視訊
description: Dynamic Media具有OpenAPI功能，可讓您為Adobe Experience Manager (AEM)中的已核准視訊資產自動產生「視訊智慧型裁切」輸出。
role: Admin, User
badgeSaas: label="AEM Assets" type="Positive" tooltip="適用於AEM Assets)。"
exl-id: video-smartcrop-dmwoapi
source-git-commit: c2b849ef25afd0809891a822a99ddd3059bf1919
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---


# 將視訊智慧型裁切套用至核准的視訊 {#apply-video-smart-crops-dmwoapi}

[!DNL Dynamic Media with OpenAPI capabilities]可讓您在[!DNL Adobe Experience Manager (AEM)]中自動產生視訊資產的視訊智慧型裁切輸出。 視訊智慧型裁切可分析視訊內容並動態調整框架，以在不同外觀比例和裝置上保持主要主題焦點。

當啟用功能且核准視訊資產時，會自動產生視訊智慧型裁切

## 開始之前 {#prerequisites-for-video-smart-crops}

確定您擁有：

* 存取[!DNL AEM Assets as a Cloud Service]。
* 編輯中繼資料結構的許可權。
* 為您的環境啟用OpenAPI功能的Dynamic Media 。
* 可標籤為&#x200B;**[!UICONTROL 已核准]**&#x200B;的視訊資產。

## 啟用視訊的視訊智慧型裁切 {#enable-video-smart-crops}

若要啟用視訊智慧型裁切，請設定用於視訊資產的中繼資料結構：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 中繼資料結構描述]**。
2. 開啟適用的中繼資料結構描述（例如，**預設**）。
3. 選取&#x200B;**視訊**&#x200B;表單，然後按一下&#x200B;**[!UICONTROL 編輯]**。
4. 新增新的&#x200B;**[!UICONTROL 下拉式清單欄位]**&#x200B;並設定下列專案：

   * **欄位標籤**：建立視訊智慧裁切
   * **對應到屬性**： `./jcr:content/dam:applyVideoSmartCrop`

5. 手動新增下列值：

   * 是→真
   * 否→假

6. 儲存結構。

視訊資產中繼資料表單現在提供&#x200B;**建立視訊智慧裁切**&#x200B;選項。

<!--
broken link
![Create Video Smartcrops field](/help/assets/assets/video-smartcrop-metadata-field.png)
-->

## 將視訊智慧型裁切套用至核准的視訊 {#apply-video-smart-crops}

您可以透過啟用中繼資料欄位並核准資產，將視訊智慧型裁切套用至視訊資產。

執行以下步驟：

1. 在[!DNL Assets View]中，選取&#x200B;**[!UICONTROL Assets]**&#x200B;並導覽至您的資料夾。
2. 選取視訊資產。
3. 按一下&#x200B;**[!UICONTROL 詳細資料]**。
4. 在中繼資料面板中，找出&#x200B;**[!UICONTROL 建立視訊智慧裁切]**。
5. 將值設定為&#x200B;**是**，然後按一下&#x200B;**[!UICONTROL 儲存]**。
6. 將資產狀態設定為&#x200B;**[!UICONTROL 已核准]**。

資產獲得核准後，系統會自動產生「視訊智慧型裁切」輸出。

## 檢視視訊智慧型裁切輸出 {#view-video-smart-crops}

產生視訊智慧型裁切後：

* 視訊播放期間提供輸出。
* Dynamic Media檢視器會根據裝置和外觀比例，自動選取最適當的裁切。
* 視訊播放會以動態方式調整，讓主要主旨保持焦點。

## 使用視訊智慧型裁切的視訊 {#use-video-smart-crops}

無論在何處傳送視訊資產，您都可以使用「視訊智慧型裁切輸出」，例如：

* 網頁
* 應用
* 內嵌式視訊播放器

檢視器在播放期間自動套用適當的智慧型裁切。

>[!NOTE]
>
>* 僅針對&#x200B;**已核准**&#x200B;視訊資產產生視訊智慧型裁切。
>* 在核准資產之前，請確定&#x200B;**建立視訊智慧裁切**&#x200B;欄位已設為&#x200B;**是**。
>* 「視訊智慧型裁切」不會修改原始資產。 裁切會在播放期間動態套用。
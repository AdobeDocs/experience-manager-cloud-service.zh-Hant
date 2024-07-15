---
title: 在Dynamic Media中使用3D資產
description: 瞭解如何在Dynamic Media中使用3D資產。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D Assets
role: User
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '2252'
ht-degree: 2%

---

# 在Dynamic Media中使用3D資產 {#working-with-three-d-assets-dm}

Dynamic Media可讓您上傳、管理、檢視及傳遞3D資產，盡享沈浸式體驗。

* 一鍵式發佈(使用工具列上的&#x200B;**[!UICONTROL 快速Publish]**)來產生URL。
* 透過由Adobe Dimension提供支援的高品質互動式Dimensional檢視器預設集，針對3D資產提供最佳化支援。
* 3D Media WCM元件可讓您輕鬆將3D資產新增至[!DNL Adobe Experience Manager Sites]頁面。

在Dynamic Media中使用3D資產無需額外安裝。

3d](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)中的![鞋

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media支援的3D格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支援下列3D檔案格式。

另請參閱Experience Manager Assets支援的[3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D副檔名 | 檔案格式 | MIME型別 | 附註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary | 將材質和紋理納入為單一資產。 |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體成型 | application/vnd.ms-pki.stl |  |
| USDZ | Universal Scene說明Zip封存 | model/vnd.usdz+zip | *僅支援擷取；不提供檢視或互動。* USDZ是專有的3D格式，可由Safari或iOS以原生方式檢視。 |

資產「詳細資訊」頁面上的3D Media WCM元件和3D預覽版與最新版Chrome (97.x)不相容。 若要使用3D資產，請改用Firefox或Safari，或使用舊版Chrome (96.x)。

## 快速入門：Dynamic Media中的3D資產 {#quick-start-three-d}

下列逐步工作流程說明可協助您在Dynamic Media中快速上手並執行3D資產。

在Dynamic Media中使用3D資產之前，請確定您的[!DNL Experience Manager]管理員已啟用並設定Dynamic MediaCloud Service。

請參閱[設定Dynamic MediaCloud Service](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)。

1. **上傳3D資產**

   * [上傳您的3D資產以用於Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [Dynamic Media中支援的上傳3D檔案格式](#supported-three-d-file-formats-in-dm)

1. **管理3D資產**

   * 組織和搜尋3D資產

      * [組織數位資產](/help/assets/organize-assets.md)
      * [搜尋三維資產](/help/assets/search-assets.md)

   * 檢視三維資產

      * [檢視3D資產並與其互動](#viewing-three-d-assets)
      * [管理維度檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)

   * 使用3D資產中繼資料

      * [管理數位資產的中繼資料](/help/assets/manage-digital-assets.md#editing-properties)
      * [中繼資料結構描述](/help/assets/metadata-schemas.md)

1. **Publish 3D資產**

   * [Publish靜態Dynamic Media 3D資產](#publishing-three-d-assets)
   * [使用維度檢視器發佈Dynamic Media 3D資產的替代方法](#alternate-publish-methods)

## 關於檢視和與3D資產互動 {#viewing-three-d-assets}

本節說明如何以兩種不同的方式檢視3D資產並與其互動：從資產詳細資訊頁面內以及從Sites的3D Media元件內。

互動式3D檢視器包含一系列互動式相機控制項，可供您環繞、縮放和平移3D資產。

在「資產詳細資訊」頁面檢視中開啟3D資產所需的時間取決於多個因素。 這些因素包括：

* 伺服器的頻寬。
* 伺服器的延遲
* 影像的複雜性。

此外，使用者端電腦的功能（例如工作站、筆記型電腦或行動觸控裝置）也是您以互動方式操作相機時也必須考量的重要因素。 功能相當強大的系統，搭配良好的繪圖功能，可讓互動式3D觀賞體驗更順暢、更理想。

>[!TIP]
>
>您可以在檢視器預設集編輯器中開啟維度檢視器預設集，以練習導覽3D資產，而不需要先上傳任何3D檔案。 維度檢視器預設集內建了3D資產，可供您互動。
>
>請參閱[管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

## 從資產詳細資訊頁面檢視3D資產並與其互動 {#viewing-three-d-assets-from-asset-details-page}

另請參閱[使用軟體介面預覽資產](/help/assets/dynamic-media/previewing-assets.md)。

**若要從資產詳細資訊頁面檢視3D資產並與其互動：**

1. 確定您已將3D資產上傳至[!DNL Experience Manager]。

   檢視[上傳您的3D資產以用於Dynamic Media](/help/assets/add-assets.md#upload-assets)。

1. 從[!DNL Experience Manager]，在&#x200B;**[!UICONTROL 導覽]**&#x200B;頁面上選取&#x200B;**[!UICONTROL Assets >檔案]**。
1. 在頁面的右上角，從&#x200B;**[!UICONTROL 檢視]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 卡片檢視]**。
1. 導覽至您要檢視的3D資產。
1. 若要在詳細資訊頁面中開啟資產，請選取3D資產的卡片。
1. 在3D資產的「詳細資訊」頁面上，執行下列任一項作業：

   | 檢視 | 說明 | 滑鼠動作 | 觸控熒幕動作 |
   | --- | --- | --- | --- |
   | **轉動相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 按一下左鍵+拖曳。 | 單指按下+拖曳。 |
   | **平移相機** | 向左、向右、向上或向下平移檢視。 | 按一下右鍵+拖曳。 | 雙指按下+拖曳。 |
   | **縮放相機** | 在3D場景中移入和移出區域。 | 滾輪。 | 兩指捏合。 |
   | **重新將相機置中** | 將相機重新置中至3D場景中物件上的某個點。 | 按兩下。 | 連按兩下。 |
   | **重設** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點恢復到3D資產的中心。 重設也會將相機移到更近或更遠的位置，以合理的檢視大小完整顯示資產。 |   |   |
   | **全熒幕模式** | 若要進入全熒幕模式，請在頁面的右下角選取「全熒幕」圖示。 |   |   |

1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 關閉]**&#x200B;以返回Assets頁面。

## 在3D媒體元件中檢視3D資產並與其互動 {#interacting-with-asset-inside-three-d-media-component}

當網頁處於&#x200B;**[!UICONTROL 編輯]**&#x200B;模式時，無法與3D資產互動。 若要讓資產互動，您可以使用&#x200B;**[!UICONTROL 預覽]**&#x200B;功能在頁面編輯器中檢視網頁，以完整存取3D媒體元件的功能。

>[!IMPORTANT]
>
>您必須先將3D媒體元件新增至網頁，並指派3D資產給該元件，才能完成此工作。 請參閱[將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)和[將3D資產指派至3D媒體元件](#assigning-a-three-d-asset-to-the-component)。

另請參閱[使用軟體介面預覽資產](/help/assets/dynamic-media/previewing-assets.md)。

**若要檢視3D媒體元件中的3D資產並與其互動：**

1. 當網頁處於&#x200B;**[!UICONTROL 編輯]**&#x200B;模式時，請執行下列任一項動作：

   * 在頁面右上角附近，按一下&#x200B;**[!UICONTROL 預覽]**&#x200B;以進入&#x200B;**[!UICONTROL 預覽]**&#x200B;模式。
   * 從瀏覽器中的頁面URL刪除`/editor.html`。

   顯示3D媒體元件](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)內的![3D資產
以**[!UICONTROL 預覽]**&#x200B;模式顯示的完全互動式3D資產。

1. 在&#x200B;**[!UICONTROL 預覽]**&#x200B;模式中時，請執行下列任一項動作：

   | 檢視 | 說明 | 滑鼠動作 | 觸控熒幕動作 |
   | --- | --- | --- | --- |
   | **轉動相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 按一下左鍵+拖曳。 | 單指按下+拖曳。 |
   | **平移相機** | 向左、向右、向上或向下平移檢視。 | 按一下右鍵+拖曳。 | 雙指按下+拖曳。 |
   | **縮放相機** | 在3D場景中移入和移出區域。 | 滾輪。 | 兩指捏合。 |
   | **重新將相機置中** | 將相機重新置中至3D場景中物件上的某個點。 | 按兩下。 | 連按兩下。 |
   | **重設** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點恢復到3D資產的中心。 重設也會將相機移到更近或更遠的位置，以合理的檢視大小完整顯示資產。 |   |   |
   | **全熒幕模式** | 若要進入全熒幕模式，請在頁面的右下角選取「全熒幕」圖示。 |   |   |

## 關於使用3D媒體元件 {#working-with-three-d-media-component}

Dynamic Media包含一個Dynamic Media 3D Media元件，您可以在[!DNL Experience Manager Sites]中使用，以便在網頁上以互動方式檢視3D模型。

* [將3D媒體元件新增至頁面範本](#adding-three-d-media-component-to-page-template)
* [將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)
   * [可選 — 設定3D媒體元件](#configuring-the-three-d-component)
* [將3D資產指派給3D媒體元件](#assigning-a-three-d-asset-to-the-component)

## 將3D媒體元件新增至頁面範本 {#adding-three-d-media-component-to-page-template}

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]**。
1. 導覽至您要啟用3D元件的頁面範本，然後選取範本。
1. 若要開啟範本，請選取&#x200B;**[!UICONTROL 編輯]**。
1. 在頁面的右上角，在下拉式功能表中選取&#x200B;**[!UICONTROL 結構]**&#x200B;模式（如果尚未啟用）。

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. 若要選取空白區域並開啟其相關工具列，請選取&#x200B;**[!UICONTROL 配置容器]**&#x200B;區域中的空白區域。
1. 在工具列中選取&#x200B;**[!UICONTROL 原則]**&#x200B;圖示以開啟&#x200B;**[!UICONTROL 原則編輯器]**。
1. 在&#x200B;**[!UICONTROL 屬性]**&#x200B;區段的&#x200B;**[!UICONTROL 允許的元件]**&#x200B;標籤下，捲動至&#x200B;**[!UICONTROL Dynamic Media]**，然後展開清單並檢查&#x200B;**[!UICONTROL 3D媒體]**。
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存變更並關閉&#x200B;**[!UICONTROL 原則編輯器]**。

   現在，您可以在使用這個範本的所有頁面上放置Dynamic Media 3D媒體元件。

## 將3D媒體元件新增至網頁 {#adding-the-three-d-media-component-to-a-web-page}

如果您使用[!DNL Experience Manager]作為網頁內容管理系統，您可以透過3D媒體元件將3D資產新增至網頁。

另請參閱[將Dynamic Media資產新增至頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

1. 開啟[!DNL Experience Manager Sites]並選取您要新增Dynamic Media 3D Media元件的網頁。
1. 若要在頁面編輯器中開啟頁面，請選取&#x200B;**[!UICONTROL 編輯]** （鉛筆）圖示。 請確定在頁面右上角附近選取&#x200B;**[!UICONTROL 編輯]**&#x200B;模式。

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. 在工具列上，選取「側面板」圖示以切換或「開啟」面板的顯示。

1. 在側面板中，選取加號圖示以開啟&#x200B;**[!UICONTROL 元件]**&#x200B;清單。

   ![3d-media-component-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. 將&#x200B;**[!UICONTROL 3D Media]**&#x200B;元件從&#x200B;**[!UICONTROL 元件]**&#x200B;清單拖曳到頁面上您要顯示3D檢視器的位置。

您現在已準備好指派3D資產給元件。

請參閱[將3D資產指派給3D媒體元件](#assigning-a-three-d-asset-to-the-component)

### 可選 — 設定3D媒體元件 {#configuring-the-three-d-component}

1. 在[!DNL Experience Manager Sites]頁面編輯器中，選取您先前新增至頁面的&#x200B;**[!UICONTROL 3D媒體檢視器]**&#x200B;元件。
1. 若要開啟元件組態對話方塊，請選取&#x200B;**[!UICONTROL 組態]**&#x200B;圖示（扳手）。

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. 在「3D媒體」對話方塊的「檢視器預設集」下拉式清單中，選取「**[!UICONTROL 維度]**」，將「維度」檢視器預設集指派給元件。

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. 在右上角，選取核取記號以儲存變更。

## 將3D資產指派給3D媒體元件 {#assigning-a-three-d-asset-to-the-component}

將3D媒體元件新增至網頁後，即可為其指派3D資產。

請參閱[將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)。

1. 在[!DNL Experience Manager Sites]頁面編輯器中，按一下&#x200B;**[!UICONTROL Assets]**&#x200B;圖示以開啟側邊面板中的&#x200B;**[!UICONTROL Assets]**。
1. 在下拉式清單中，選取&#x200B;**[!UICONTROL 3D]**&#x200B;以僅顯示3D資產檔案型別。
1. 在側面板中，搜尋或捲動至您要在編輯的頁面上檢視的3D資產。
1. 從Assets側面板拖曳3D資產，並將其拖曳至您先前新增至頁面的&#x200B;**[!UICONTROL 3D Media]**&#x200B;元件。

   ![將3d資產指派給3d媒體元件](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>當網頁處於[!DNL Experience Manager Sites] **[!UICONTROL 編輯]**&#x200B;模式時，3D媒體元件會顯示3D資產，但無法與資產互動。 若要讓資產互動，您可以使用&#x200B;**[!UICONTROL 預覽]**&#x200B;功能在頁面編輯器中檢視網頁，以完整存取3D媒體元件的功能。

## Publish靜態Dynamic Media 3D資產 {#publishing-three-d-assets}

Dynamic Media接受各種在Dynamic Media中支援的3D檔案格式為&#x200B;*靜態內容*。 靜態內容表示您可以上傳和發佈3D資產，但不支援與3D資產相關聯的&#x200B;*動態*&#x200B;影像或重新調整。 這是因為Dynamic Media Imaging Server無法辨識3D格式。 因此，在Dynamic Media中發佈3D資產後，您就可以立即複製URL。 3D資產的URL會遵循一般的Dynamic Media URL結構。 不過，與Dynamic Media中的傳統影像資產不同，您無法編輯資產URL中的任何引數。

另請參閱[取得靜態資產的URL](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)。

在&#x200B;**[!UICONTROL 卡片檢視]**&#x200B;中，資產名稱正下方及其日期和時間左側會顯示一個小型全球圖示，以指出資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

如果您使用[!DNL Experience Manager]做為WCM，請使用此發佈方法直接在網頁上新增Dynamic Media 3D資產。

另請參閱[Publish Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

另請參閱[Publish頁面](/help/sites-cloud/authoring/sites-console/publishing-pages.md)。

**若要發佈靜態Dynamic Media 3D資產：**

1. 開啟3D資產（GLB、OBJ或STL檔案格式）。
1. 在「詳細資訊」頁面的工具列上，選取「**[!UICONTROL 快速Publish]**」。

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. 選取&#x200B;**[!UICONTROL 關閉]**&#x200B;以結束對話方塊並返回資產詳細資訊頁面。
1. 從3D資產檔案名稱左側的下拉式清單中，選取&#x200B;**[!UICONTROL 轉譯]**。

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. 選取&#x200B;**[!UICONTROL 原始]**。 發佈（或「啟動」）3D資產時，如果符合下列所有3D資產條件，**[!UICONTROL URL]**&#x200B;按鈕會出現在頁面左下角附近：
   * 3D資產是支援的格式（GLB、OBJ、STL和USDZ）。
   * 3D資產已擷取至Dynamic Media Image Production System (IPS)。
   * 3D資產隨即發佈。

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. 若要顯示您可以在網頁上複製並使用之3D資產的直接生產URL，請選取&#x200B;**[!UICONTROL URL]**。

### 使用維度檢視器發佈Dynamic Media 3D資產的替代方法 {#alternate-publish-methods}

如果您&#x200B;*不是*，且使用[!DNL Experience Manager]做為WCM，請使用下列兩種方法發佈Dynamic Media 3D資產。

* **[!UICONTROL URL]** — 如果您使用協力廠商網頁內容管理系統，而且想要使用維度檢視器將Dynamic Media 3D資產連結至您的網頁，請使用&#x200B;**[!UICONTROL URL]**。

  檢視[將URL連結至您的網頁應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)。

* **[!UICONTROL 內嵌]** — 當您想要使用維度檢視器檢視內嵌在網頁上的Dynamic Media 3D資產時，請使用&#x200B;**[!UICONTROL 內嵌]**。 您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。**[!UICONTROL 內嵌]**&#x200B;對話方塊中不允許編輯程式碼。

  請參閱[將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)。

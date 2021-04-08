---
title: 在Dynamic Media使用3D資產
description: 瞭解如何在Dynamic Media使用3D資產。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
feature: 3D資產
topic: 業務從業人員
role: Business Practitioner
exl-id: 82084ba7-1302-4cbd-8626-d77b3aaa4ed1
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '2271'
ht-degree: 1%

---

# 在Dynamic Media使用3D資產{#working-with-three-d-assets-dm}

Dynamic Media可讓您上傳、管理、檢視和傳遞3D資產，成為身歷其境的體驗。

* 按一下3D資產的發佈（使用工具列上的&#x200B;**[!UICONTROL Quick Publish]**）以產生URL。
* 使用由Adobe Dimension提供支援的高品質互動式維度檢視器預設集，以最佳化支援檢視3D資產。
* 3D Media WCM元件可讓您輕鬆將3D資產新增至Adobe Experience Manager Sites頁面。

在Dynamic Media使用3D資產不需要額外安裝。

![3D鞋](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media{#supported-three-d-file-formats-in-dm}支援的3D格式

Dynamic Media支援下列3D檔案格式。

另請參閱[支援的3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | 模型/gltf-binary | 將材質和紋理整合為單一資產。 |
| OBJ | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用場景描述Zip封存 | model/vnd.usdz+zip | *僅支援擷取；不提供檢視或互動功能。* USDZ是專屬的3D格式，可由Safari或iOS以原生方式檢視。 |

## 快速入門：Dynamic Media的3D資產{#quick-start-three-d}

下列逐步工作流程說明旨在協助您快速上手並執行Dynamic Media的3D資產。

在您使用Dynamic Media的3D資產之前，請確定您的Experience Manager管理員已啟用並設定了Dynamic MediaCloud Services。

請參閱[配置Dynamic MediaCloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)。

1. **上傳3D資產**

   * [上傳您的3D資產以用於Dynamic Media](/help/assets/add-assets.md#upload-assets)
   * [支援的3D檔案格式，可在Dynamic Media上傳](#supported-three-d-file-formats-in-dm)

1. **管理3D資產**

   * 組織及搜尋3D資產

      * [組織數位資產](/help/assets/organize-assets.md)
      * [搜尋3D資產](/help/assets/search-assets.md)
   * 檢視3D資產

      * [檢視並與3D資產互動](#viewing-three-d-assets)
      * [管理維度檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)
   * 使用3D資產中繼資料

      * [管理數位資產的中繼資料](/help/assets/manage-digital-assets.md#editing-properties)
      * [中繼資料結構](/help/assets/metadata-schemas.md)



1. **發佈3D資產**

   * [發佈靜態Dynamic Media3D資產](#publishing-three-d-assets)
   * [使用Dimensional檢視器發佈Dynamic Media3D資產的替代方法](#alternate-publish-methods)

## 關於檢視和與3D資產{#viewing-three-d-assets}互動

本節說明如何以兩種不同的方式檢視和處理3D資產：從資產詳細資訊頁面和網站的3D媒體元件中。

互動式3D檢視器除其他功能外，還包含一系列互動式相機控制項，讓您環繞、縮放和平移3D資產。

在「資產詳細資料」頁面檢視中開啟3D資產所花的時間，取決於數個因素。 這些因素包括：

* 伺服器的頻寬。
* 伺服器延遲
* 影像的複雜性。

此外，在您以互動方式操作相機時，用戶端電腦（例如工作站、筆記型電腦或行動觸控裝置）的功能也很重要。 功能相當強大的系統，具備良好的圖形功能，可讓互動式3D檢視體驗更順暢更有利。

>[!TIP]
>
>您可以在檢視器預設集編輯器中開啟維度檢視器預設集，以練習導覽3D資產，而不需先上傳任何3D檔案。 維度檢視器預設集內建3D資產供您互動。
>
>請參閱[管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md)。

## 從資產詳細資料頁面{#viewing-three-d-assets-from-asset-details-page}檢視並與3D資產互動

另請參閱[使用軟體介面預覽資產](/help/assets/dynamic-media/previewing-assets.md)。

**若要從資產詳細資訊頁面檢視並與3D資產互動**

1. 請確定您已將3D資產上傳至Experience Manager。

   請參閱[上傳您的3D資產以用於Dynamic Media](/help/assets/add-assets.md#upload-assets)。

1. 從Experience Manager，在&#x200B;**[!UICONTROL Navigation]**&#x200B;頁面上，點選&#x200B;**[!UICONTROL 資產>檔案]**。
1. 在頁面的右上角附近，從&#x200B;**[!UICONTROL View]**&#x200B;下拉式清單中，點選&#x200B;**[!UICONTROL Card View]**。
1. 導覽至您要檢視的3D資產。
1. 若要在「詳細資料」頁面中開啟資產，請點選3D資產的卡片。
1. 在3D資產的「詳細資料」頁面上，執行下列任一項作業：

   * **旋轉相機** -環繞3D場景和物件環繞視圖。
      * _滑鼠_:左鍵按一下+拖曳。
      * _觸控螢幕_:單指按+拖曳。
   * **平移您的相機** -向左、向右、向上或向下平移您的檢視。
      * _滑鼠_:按一下滑鼠右鍵並拖曳。
      * _觸控螢幕_:雙指按住+拖曳。
   * **縮放您的相機** -縮放您的相機以移入和移出3D場景的區域。
      * _滑鼠_:滾輪。
      * _觸控螢幕_:雙指夾捏。
   * **重新輸入相機** -將相機重新輸入到3D場景中某個物件的某個點。
      * _滑鼠_:按兩下。
      * _觸控螢幕_:點兩下。
   * **Reset**  —— 靠近頁面的右下角，點選「Reset」（重設）圖示，將檢視目標點還原至3D資產的中央。Reset也會使攝影機更靠近或更遠，以便以合理的檢視大小顯示整個資產。
   * **全螢幕模式** -若要進入全螢幕模式，請在頁面的右下角點選全螢幕圖示。

1. 在頁面的右上角，點選&#x200B;**[!UICONTROL Close]**&#x200B;以返回「資產」頁面。

## 在3D媒體元件{#interacting-with-asset-inside-three-d-media-component}中檢視並與3D資產互動

當網頁處於&#x200B;**[!UICONTROL 編輯]**&#x200B;模式時，不可能與3D資產互動。 若要讓資產具互動性，您可以使用&#x200B;**[!UICONTROL 預覽]**&#x200B;功能，在頁面編輯器中檢視網頁，並完整存取3D媒體元件的功能。

>[!IMPORTANT]
>
>只有在將3D媒體元件新增至網頁並指派3D資產至元件後，您才能完成此工作。 請參閱[將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)和[將3D資產指派至3D媒體元件](#assigning-a-three-d-asset-to-the-component)。

另請參閱[使用軟體介面預覽資產](/help/assets/dynamic-media/previewing-assets.md)。

**若要在3D媒體元件內檢視3D資產並與之互動**

1. 當網頁處於&#x200B;**[!UICONTROL 編輯]**&#x200B;模式時，請執行下列任一操作：

   * 在頁面右上方附近，按一下「預覽」，進入「預覽」模式。********
   * 從瀏覽器的頁面URL刪除`/editor.html`。

完全互動的3D資產，如    ![3D資產顯示在3D媒體元件內3D](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
資產完全互動的3D資產，如預覽模 **** 式所示。

1. 在&#x200B;**[!UICONTROL 預覽]**&#x200B;模式中，執行下列任一操作：

   * **旋轉相機** -環繞3D場景和物件環繞視圖。
      * _滑鼠_:左鍵按一下+拖曳。
      * _觸控螢幕_:單指按+拖曳。
   * **平移您的相機** -向左、向右、向上或向下平移您的檢視。
      * _滑鼠_:按一下滑鼠右鍵並拖曳。
      * _觸控螢幕_:雙指按住+拖曳。
   * **縮放您的相機** -縮放您的相機以移入和移出3D場景的區域。
      * _滑鼠_:滾輪。
      * _觸控螢幕_:雙指夾捏。
   * **重新輸入相機** -將相機重新輸入到3D場景中某個物件的某個點。
      * _滑鼠_:按兩下。
      * _觸控螢幕_:點兩下。
   * **Reset**  —— 靠近頁面的右下角，點選「Reset」（重設）圖示，將檢視目標點還原至3D資產的中央。Reset也會使攝影機更靠近或更遠，以便以合理的檢視大小顯示整個資產。
   * **全螢幕模式** -若要進入全螢幕模式，請在頁面的右下角點選全螢幕圖示。

## 關於使用3D介質元件{#working-with-three-d-media-component}

Dynamic Media包含Dynamic Media3D媒體元件，您可在Experience Manager網站中使用此元件，以互動方式檢視網頁上的3D模型。

* [將3D媒體元件新增至頁面範本](#adding-three-d-media-component-to-page-template)
* [將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)
   * [可選——配置3D介質元件](#configuring-the-three-d-component)
* [將3D資產指派給3D媒體元件](#assigning-a-three-d-asset-to-the-component)


## 將3D媒體元件新增至頁面範本{#adding-three-d-media-component-to-page-template}

1. 導覽至&#x200B;**[!UICONTROL 工具>一般>範本]**。
1. 導覽至您要在中啟用3D元件的頁面範本，然後選取範本。
1. 若要開啟範本，請點選&#x200B;**[!UICONTROL 編輯]**。
1. 在頁面右上方的下拉式功能表中，選取&#x200B;**[!UICONTROL 結構]**&#x200B;模式（如果尚未啟用）。

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. 若要選取空白區域並開啟其相關的工具列，請點選「版面容器」**[!UICONTROL 區域中的空白區域。]**
1. 在工具欄上，按一下&#x200B;**[!UICONTROL 策略]**&#x200B;表徵圖以開啟&#x200B;**[!UICONTROL 策略編輯器]**。
1. 在&#x200B;**[!UICONTROL 屬性]**&#x200B;區段的&#x200B;**[!UICONTROL 允許的元件]**&#x200B;標籤下，捲動至&#x200B;**[!UICONTROL Dynamic Media]**，然後展開清單並勾選&#x200B;**[!UICONTROL 3D媒體]**。
1. 點選&#x200B;**[!UICONTROL Done]**&#x200B;以儲存變更並關閉&#x200B;**[!UICONTROL 原則編輯器]**。

   您現在可以將Dynamic Media3D媒體元件置於使用此範本的所有頁面上。

## 將3D介質元件添加到網頁{#adding-the-three-d-media-component-to-a-web-page}

如果您使用Experience Manager作為網頁內容管理系統，可以透過3D媒體元件將3D資產新增至網頁。

另請參閱[將Dynamic Media資產新增至頁面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)。

1. 開啟Experience Manager網站，並選取您要新增Dynamic Media3D媒體元件的網頁。
1. 若要在頁面編輯器中開啟頁面，請點選&#x200B;**[!UICONTROL Edit]**（鉛筆）圖示。 請確定在頁面右上角附近選取了&#x200B;**[!UICONTROL 編輯]**&#x200B;模式。

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. 在工具列上，點選「側面板」圖示以切換或「開啟」面板的顯示。

1. 在側面板中，點選加號圖示以開啟&#x200B;**[!UICONTROL 元件]**&#x200B;清單。

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. 將&#x200B;**[!UICONTROL 3D Media]**&#x200B;元件從&#x200B;**[!UICONTROL 元件]**&#x200B;清單拖曳至您希望3D檢視器出現的頁面位置。

您現在可以指派3D資產給元件。

請參閱[將3D資產分配給3D介質元件](#assigning-a-three-d-asset-to-the-component)

### 可選——配置3D介質元件{#configuring-the-three-d-component}

1. 在「Experience Manager站點」頁面編輯器中，選擇先前添加到頁面的&#x200B;**[!UICONTROL 3D Media Viewer]**&#x200B;元件。
1. 若要開啟元件設定對話方塊，請點選&#x200B;**[!UICONTROL Configuration]**&#x200B;圖示（扳手）。

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. 在「3D媒體」對話框中，從「查看器預設」下拉清單中，選擇&#x200B;**[!UICONTROL Dimensional]**&#x200B;將維查看器預設分配給元件。

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. 在右上角點選核取標籤以儲存變更。

## 將3D資產分配給3D介質元件{#assigning-a-three-d-asset-to-the-component}

將3D媒體元件新增至網頁後，您就可以指派3D資產給該網頁。

請參閱[將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)。

1. 在「Experience Manager網站」頁面編輯器中，按一下「資產」圖示以開啟側面板中的「資產」。********
1. 在下拉式清單中，選取&#x200B;**[!UICONTROL 3D]**&#x200B;以僅顯示3D資產檔案類型。
1. 在側面板中，搜尋或捲動至您要在編輯的頁面上檢視的3D資產。
1. 從「資產」側面板拖曳3D資產，並將其拖曳至您先前新增至頁面的&#x200B;**[!UICONTROL 3D Media]**&#x200B;元件。

   ![將3D資產指派給3D媒體元件](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>當網頁處於「Experience Manager網站&#x200B;**[!UICONTROL 編輯]**」模式時，3D媒體元件會顯示3D資產，但無法與資產互動。 若要讓資產具互動性，您可以使用&#x200B;**[!UICONTROL 預覽]**&#x200B;功能，在頁面編輯器中檢視網頁，並完整存取3D媒體元件的功能。

## 發佈靜態Dynamic Media3D資產{#publishing-three-d-assets}

Dynamic Media接受Dynamic Media支援的各種3D檔案格式，作為&#x200B;*static content*。 靜態內容表示您可以上傳和發佈3D資產，但是不支援與3D資產相關的&#x200B;*dynamic*&#x200B;影像或影像重新整理。 原因是Dynamic Media影像伺服器無法辨識3D格式。 因此，在Dynamic Media發佈3D資產後，您就可以複製立即URL。 3D資產的URL會遵循通常的Dynamic MediaURL結構。 不過，您無法編輯資產URL中的任何參數，這與Dynamic Media的傳統影像資產不同。

另請參閱[取得靜態資產的URL](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)。

在&#x200B;**[!UICONTROL 資訊卡檢視]**&#x200B;中，資產名稱正下方及其日期和時間左側會顯示一個小型全球圖示，以指出資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

如果您使用Experience Manager做為WCM，請使用此發佈方法，直接在網頁上新增Dynamic Media3D資產。

另請參閱[發佈Dynamic Media資產](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)。

另請參閱[發佈頁面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)。

**若要發佈靜態Dynamic Media3D資產**

1. 開啟3D資產（GLB、OBJ或STL檔案格式），以在「詳細資料」頁面中檢視它。
1. 在工具列上，點選&#x200B;**[!UICONTROL 快速發佈]**。

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. 點選「**[!UICONTROL 關閉]**」以退出對話方塊並返回資產詳細資料頁面。
1. 從3D資產檔案名稱左側的下拉式清單中，點選「轉譯」**[!UICONTROL 「轉譯」]**。

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. 點選&#x200B;**[!UICONTROL original]**。 當3D資產發佈（或「啟動」）時，如果符合下列所有3D資產條件，**[!UICONTROL URL]**&#x200B;按鈕會出現在頁面的左下角附近：
   * 3D資產是支援的格式（GLB、OBJ、STL和USDZ）。
   * 3D資產已收錄至Dynamic Media影像製作系統(IPS)。
   * 3D資產會發佈。

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. 若要顯示3D資產的直接生產URL，您可以複製並在網頁上使用，請點選&#x200B;**[!UICONTROL URL]**。

### 使用Dimensional檢視器{#alternate-publish-methods}發佈Dynamic Media3D資產的替代方法

如果您&#x200B;*not*&#x200B;使用Experience Manager做為WCM，請使用下列兩種方法發佈Dynamic Media3D資產。

* **[!UICONTROL URL]** -使用 **** URL如果您使用協力廠商的網頁內容管理系統，而且您想要使用維度檢視器將Dynamic Media3D資產連結至您的網頁。

   請參閱[將URL連結至您的Web應用程式](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)。

* **[!UICONTROL 內嵌]** -當您 **** 想要使用維度檢視器檢視內嵌在網頁上的Dynamic Media3D資產時，請使用「內嵌」。您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。不允許在&#x200B;**[!UICONTROL Embed]**&#x200B;對話方塊中編輯程式碼。

   請參閱[將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)。

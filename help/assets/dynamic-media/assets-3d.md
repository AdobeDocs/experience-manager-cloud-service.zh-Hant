---
title: 在動態媒體中使用3D資產
description: 瞭解如何在動態媒體中使用3D資產。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS and Experience Manager as a Cloud Service
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: fd75af0bf0c16e20c3b98703af14f329ea6c6371
workflow-type: tm+mt
source-wordcount: '2270'
ht-degree: 1%

---


# 在動態媒體{#working-with-three-d-assets-dm}中使用3D資產

動態媒體可讓您上傳、管理、檢視和傳遞3D資產，成為身歷其境的體驗。

* 按一下3D資產的發佈（使用工具列上的&#x200B;**[!UICONTROL Quick Publish]**）以產生URL。
* 使用Adobe Dimension提供的高品質互動式Dimensional檢視器預設集，最佳化3D資產檢視支援。
* 3D Media WCM元件可讓您輕鬆將3D資產新增至Experience Manager Sites頁面。

在動態媒體中使用3D資產不需要額外安裝。

![3D鞋](/help/assets/dynamic-media/assets/3d-dimensional-viewer-quickpublish-url-embed2a.png)

<!-- See also [Dynamic Media 3D Release Notes.](/help/release-notes/aem3d-release-notes.md) -->

## 動態媒體{#supported-three-d-file-formats-in-dm}支援的3D格式

Dynamic Media支援下列3D檔案格式。

另請參閱[支援的3D格式](/help/assets/file-format-support.md#support-3d-formats)

| 3D副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | 模型/gltf-binary | 將材質和紋理整合為單一資產。 |
| OBJ | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用場景描述Zip封存 | model/vnd.usdz+zip | *僅支援擷取；不提供檢視或互動功能。* USDZ是專屬的3D格式，可由Safari或iOS以原生方式檢視。 |

## 快速入門：動態媒體中的3D資產{#quick-start-three-d}

下列逐步工作流程說明旨在協助您在動態媒體中快速啟動並執行3D資產。

在Dynamic Media中處理3D資產之前，請確定您的Experience Manager管理員已啟用並設定Dynamic Media Cloud服務。

請參閱[設定動態媒體雲端服務。](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services)

1. **上傳3D資產**

   * [上傳您的3D資產以用於動態媒體](/help/assets/add-assets.md#upload-assets)
   * [支援的3D檔案格式，可在動態媒體中上傳](#supported-three-d-file-formats-in-dm)

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

   * [發佈靜態動態媒體3D資產](#publishing-three-d-assets)
   * [使用Dimensional檢視器發佈動態媒體3D資產的替代方法](#alternate-publish-methods)

## 關於檢視和與3D資產{#viewing-three-d-assets}互動

本節說明如何以兩種不同的方式檢視和處理3D資產：從資產詳細資訊頁面和網站的3D媒體元件中。

互動式3D檢視器除其他功能外，還包含一系列互動式相機控制項，讓您環繞、縮放和平移3D資產。

請注意，在「資產詳細資料」頁面檢視中開啟3D資產所花的時間取決於數個因素。 這些因素包括：

* 伺服器的頻寬。
* 伺服器延遲
* 影像的複雜性。

此外，在您以互動方式操作相機時，用戶端電腦（例如工作站、筆記型電腦或行動觸控裝置）的功能也很重要。 功能相當強大的系統，具備良好的圖形功能，可讓互動式3D檢視體驗更順暢更有利。

>[!TIP]
>
>您可以在檢視器預設集編輯器中開啟維度檢視器預設集，以練習導覽3D資產，而不需先上傳任何3D檔案。 維度檢視器預設集內建3D資產供您互動。
>
>請參閱[管理檢視器預設集。](/help/assets/dynamic-media/managing-viewer-presets.md)

## 從資產詳細資料頁面{#viewing-three-d-assets-from-asset-details-page}檢視並與3D資產互動

另請參閱[使用軟體介面預覽資產。](/help/assets/dynamic-media/previewing-assets.md)

**若要從資產詳細資訊頁面檢視並與3D資產互動**

1. 請確定您已將3D資產上傳至Experience Manager。

   請參閱[上傳您的3D資產以用於動態媒體。](/help/assets/add-assets.md#upload-assets)

1. 在Experience Manager的&#x200B;**[!UICONTROL Navigation]**&#x200B;頁面上，點選「**[!UICONTROL 資產>檔案]**」。
1. 在頁面的右上角附近，從&#x200B;**[!UICONTROL View]**&#x200B;下拉式清單中，點選&#x200B;**[!UICONTROL Card View]**。
1. 導覽至您要檢視的3D資產。
1. 點選3D資產的資訊卡，以在資產詳細資訊頁面中開啟它。
1. 在3D資產的詳細資料檢視頁面上，執行下列任一項作業：

   * **旋轉相機** -環繞3D場景和物件環繞視圖。
      * _滑鼠_:左鍵按一下+拖曳。
      * _觸控螢幕_:單指按+拖曳。
   * **平移您的相機** -向左、向右、向上或向下平移您的檢視。
      * _滑鼠_:按一下滑鼠右鍵並拖曳。
      * _觸控螢幕_:雙指按住+拖曳。
   * **縮放您的相機** -縮放您的相機以移入和移出3D場景的區域。
      * _滑鼠_:滾輪。
      * _觸摸屏_:兩指捏。
   * **重新輸入相機**  — 將相機重新輸入到3D場景中某個對象上的某個點。
      * _滑鼠_:按兩下。
      * _觸摸屏_:按兩下。
   * **重置**  — 在頁面右下角附近，按一下「重置」表徵圖將視圖目標點恢復到3D資產的中心。重置還使相機更近或更遠地移動，以便以合理的觀看大小顯示整個資產。
   * **全屏模式**  — 要進入全屏模式，請在頁面右下角按一下全屏表徵圖。

1. 在頁面的右上角，按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;以返回到「Assets（資產）」頁面。

## 查看3D介質元件{#interacting-with-asset-inside-three-d-media-component}內的3D資產並與其交互

當網頁處於&#x200B;**[!UICONTROL 編輯]**&#x200B;模式時，不能與3D資產進行交互。 要使資產具有交互性，可以使用&#x200B;**[!UICONTROL 預覽]**&#x200B;功能在頁面編輯器中查看對3D媒體元件功能具有完全訪問權限的網頁。

>[!IMPORTANT]
>
>只有在將3D媒體元件添加到網頁並將3D資產分配給該元件後，才能完成此任務。 請參見[將3D媒體元件添加到網頁](#adding-the-three-d-media-component-to-a-web-page)和[將3D資產分配給3D媒體元件。](#assigning-a-three-d-asset-to-the-component)

另請參閱[使用軟體介面預覽資產。](/help/assets/dynamic-media/previewing-assets.md)

**查看3D介質元件內的3D資產並與其交互**

1. 當網頁處於&#x200B;**[!UICONTROL 編輯]**&#x200B;模式時，請執行以下任一操作：

   * 在頁面右上角附近，按一下&#x200B;**[!UICONTROL 預覽]**&#x200B;進入&#x200B;**[!UICONTROL 預覽]**&#x200B;模式。
   * 從瀏覽器的頁面URL中刪除`/editor.html`。

全互動式3D資產，如所示    ![顯示在3D介質元件內部的3D](/help/assets/dynamic-media/assets/3d-asset-in-3d-mediaa.png)
資產在預覽模式中顯示的完全互動式3D **** 資產。

1. 在&#x200B;**[!UICONTROL 預覽]**&#x200B;模式下，執行下列任何操作：

   * **轉動相機**  — 圍繞3D場景和對象環繞視圖。
      * _滑鼠_:左鍵按一下並拖動。
      * _觸摸屏_:單指按+拖動。
   * **平移相機**  — 平移視圖左、右、上或下。
      * _滑鼠_:按一下右鍵並拖動。
      * _觸摸屏_:雙指按+拖動。
   * **縮放您的相機** -縮放您的相機以移入和移出3D場景的區域。
      * _滑鼠_:滾輪。
      * _觸摸屏_:兩指捏。
   * **重新輸入相機**  — 將相機重新輸入到3D場景中某個對象上的某個點。
      * _滑鼠_:按兩下。
      * _觸摸屏_:按兩下。
   * **重置**  — 在頁面右下角附近，按一下「重置」表徵圖將視圖目標點恢復到3D資產的中心。重置還使相機更近或更遠地移動，以便以合理的觀看大小顯示整個資產。
   * **全屏模式**  — 要進入全屏模式，請在頁面右下角按一下全屏表徵圖。

## 關於使用3D介質元件{#working-with-three-d-media-component}

動態媒體包括動態媒體3D媒體元件，您可以在「體驗管理器站點」中使用該元件，以在網頁上互動式查看3D模型。

* [將3D介質元件添加到頁面模板](#adding-three-d-media-component-to-page-template)
* [將3D媒體元件添加到網頁](#adding-the-three-d-media-component-to-a-web-page)
   * [可選 — 配置3D介質元件](#configuring-the-three-d-component)
* [將3D資產分配給3D介質元件](#assigning-a-three-d-asset-to-the-component)


## 將3D介質元件添加到頁面模板{#adding-three-d-media-component-to-page-template}

1. 導航到&#x200B;**[!UICONTROL 工具>常規>模板]**。
1. 導航到要在中啟用3D元件的頁面模板並選擇該模板。
1. 按一下「編輯&#x200B;**[!UICONTROL 」開啟模板。]**
1. 在頁面右上角的下拉菜單中，選擇&#x200B;**[!UICONTROL 結構]**&#x200B;模式（如果它尚未處於活動狀態）。

   ![3d-media-component-structure](/help/assets/dynamic-media/assets/3d-media-component-structurea.png)

1. 按一下「佈局容器」**[!UICONTROL 區域中的空區域以選擇它並開啟其關聯工具欄。]**
1. 在工具欄上，按一下&#x200B;**[!UICONTROL Policy]**&#x200B;表徵圖以開啟&#x200B;**[!UICONTROL Policy Editor]**。
1. 在&#x200B;**[!UICONTROL 屬性]**&#x200B;部分的&#x200B;**[!UICONTROL 允許的元件]**&#x200B;頁籤下，滾動到&#x200B;**[!UICONTROL 動態媒體]**，然後展開清單並檢查&#x200B;**[!UICONTROL 3D媒體]**。
1. 按一下&#x200B;**[!UICONTROL 完成]**&#x200B;以保存更改並關閉&#x200B;**[!UICONTROL 策略編輯器]**。

   現在，您可以將「動態介質3D介質」元件放置在使用此模板的所有頁面上。

## 將3D媒體元件添加到網頁{#adding-the-three-d-media-component-to-a-web-page}

如果使用Adobe Experience Manager作為Web內容管理系統，則可以通過3D媒體元件將3D資產添加到網頁。

另請參閱[新增動態媒體資產至頁面。](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)

1. 開啟「體驗管理器」站點，然後選擇要向其中添加「動態介質3D介質」元件的網頁。
1. 按一下「編輯&#x200B;**[!UICONTROL （鉛筆）」表徵圖，將頁面開啟到頁面編輯器中。]**&#x200B;確保在頁面右上角附近選擇了「編輯&#x200B;**[!UICONTROL 」模式。]**

   ![3d-media-component-add](/help/assets/dynamic-media/assets/3d-media-component-edita.png)

1. 在工具欄上，按一下「側面板」表徵圖可切換或「開啟」面板的顯示。

1. 在側面板中，按一下加號表徵圖以開啟&#x200B;**[!UICONTROL 元件]**&#x200B;清單。

   ![3d-media-component-drag-drop](/help/assets/dynamic-media/assets/3d-assets-filtera.png)

1. 將&#x200B;**[!UICONTROL 3D Media]**&#x200B;元件從&#x200B;**[!UICONTROL 元件]**&#x200B;清單拖到希望3D查看器顯示的頁面上的位置。

現在，您已準備好將3D資產分配給元件。

請參閱[將3D資產分配給3D介質元件。](#assigning-a-three-d-asset-to-the-component)

### 可選 — 配置3D介質元件{#configuring-the-three-d-component}

1. 在「體驗管理器站點」頁面編輯器中，選擇以前添加到頁面的&#x200B;**[!UICONTROL 3D媒體查看器]**&#x200B;元件。
1. 按一下「**[!UICONTROL 配置]**」表徵圖（扳手）以開啟元件配置對話框。

   ![3d-media-component-config](/help/assets/dynamic-media/assets/3d-media-component-configa.png)

1. 在「3D媒體」對話框中，從「查看器預設」下拉清單中，選擇「維」**[!UICONTROL ，將「維」查看器預設分配給元件。]**

   ![3d-media-component-edit-config](/help/assets/dynamic-media/assets/3d-media-component-edit-configa.png)

1. 在右上角，按一下複選標籤以保存更改。

## 將3D資產分配給3D介質元件{#assigning-a-three-d-asset-to-the-component}

在將3D媒體元件添加到網頁後，可以為其分配3D資源。

請參閱[將3D媒體元件添加到網頁。](#adding-the-three-d-media-component-to-a-web-page)

1. 在「體驗管理器站點」頁面編輯器中，按一下「資產&#x200B;**[!UICONTROL 」表徵圖以開啟側面板中的「資產]**」。****
1. 在下拉清單中，選擇&#x200B;**[!UICONTROL 3D]**&#x200B;以僅顯示3D資產檔案類型。
1. 在側面板中，搜索或滾動到要在編輯的頁面上查看的3D資產。
1. 將3D資產從「資產」側面板拖放到先前添加到頁面的&#x200B;**[!UICONTROL 3D Media]**&#x200B;元件上。

   ![將3d資產分配給3d介質元件](/help/assets/dynamic-media/assets/3d-asset-adda.png)

>[!NOTE]
>
>當網頁處於「體驗管理器站點」**[!UICONTROL 「編輯」]**&#x200B;模式時，3D媒體元件將顯示3D資產，但不可能與資產進行交互。 要使資產具有交互性，可以使用&#x200B;**[!UICONTROL 預覽]**&#x200B;功能在頁面編輯器中查看對3D媒體元件功能具有完全訪問權限的網頁。

## 發佈靜態動態媒體3D資產{#publishing-three-d-assets}

動態媒體接受各種3D檔案格式，這些格式在動態媒體中作為&#x200B;*靜態內容*&#x200B;受支援。 靜態內容意味著您可以上載和發佈3D資產，但不支援與3D資產關聯的&#x200B;*dynamic*&#x200B;映像或影像重新編寫。 原因是動態媒體映像伺服器無法識別3D格式。 因此，在動態媒體中發佈3D資產後，您可以複製一個即時URL。 3D資產的URL遵循通常的動態媒體URL結構。 但是，不能編輯資產的URL中的任何參數，這與動態媒體中的傳統影像資產不同。

另請參閱[獲取靜態資產的URL。](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)

在&#x200B;**[!UICONTROL 卡視圖]**&#x200B;中，小型全球表徵圖會顯示在資產名稱正下方，並顯示在其日期和時間左側，以指示資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

如果您使用「體驗管理器」作為WCM，請使用此發佈方法將動態媒體3D資產直接添加到您的網頁上。

另請參閱[發佈動態媒體資產。](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

另請參閱[發佈頁面。](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

**發佈靜態動態媒體3D資產**

1. 開啟3D資產（GLB、OBJ或STL檔案格式）以在資產詳細資訊頁面中查看它。
1. 在工具欄上，按一下「快速發佈」**[!UICONTROL 。]**

   ![3d-asset-quick-publish](/help/assets/dynamic-media/assets/3d-asset-quick-publisha.png)

1. 按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;退出對話框並返回資產詳細資訊頁面。
1. 從3D資產檔案名左側的下拉清單中，按一下&#x200B;**[!UICONTROL 格式副本]**。

   ![3d-asset-renditions](/help/assets/dynamic-media/assets/3d-asset-renditionsa.png)

1. 按一下&#x200B;**[!UICONTROL original]**。 在發佈（或「激活」）3D資產時，如果滿足以下所有3D資產條件，則&#x200B;**[!UICONTROL URL]**&#x200B;按鈕將出現在頁面左下角的附近：
   * 3D資產是支援的格式（GLB、OBJ、STL和USDZ）。
   * 3D資產已被引入動態媒體映像生成系統(IPS)。
   * 3D資產已發佈。

   ![3d-asset-url](/help/assets/dynamic-media/assets/3d-asset-urla.png)

1. 點擊&#x200B;**[!UICONTROL URL]**&#x200B;可顯示3D資產的直接生產URL，您可以在網頁上複製和使用該URL。

### 使用維查看器{#alternate-publish-methods}發佈動態媒體3D資產的替代方法

如果&#x200B;*未*&#x200B;使用「體驗管理器」作為WCM，請使用以下兩種方法發佈動態媒體3D資產。

* **[!UICONTROL URL]**  — 使用 **** URL如果您使用的是第三方Web內容管理系統，並且希望使用維查看器將動態媒體3D資產連結到網頁。

   請參閱[將URL連結至您的Web應用程式。](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)

* **[!UICONTROL 嵌入]**  — 當 **** 要使用維查看器查看嵌入在網頁上的動態媒體3D資產時，請使用嵌入。您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。不允許在&#x200B;**[!UICONTROL Embed]**&#x200B;對話方塊中編輯程式碼。

   請參見[將動態媒體視頻、影像查看器或維查看器嵌入到網頁上。](/help/assets/dynamic-media/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)

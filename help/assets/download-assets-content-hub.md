---
title: 從Content Hub下載資產
description: 瞭解如何從Content Hub入口網站下載資產
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 28424cb184d0378669498c78e571961227f6539a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 從Content Hub下載資產 {#download-assets}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 開發人員文件](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![下載資產](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>Content Hub指南現在提供PDF格式。 下載整份指南，並使用Adobe Acrobat AI Assistant回答您的疑問。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub可讓您下載和共用資產。 Content Hub使用者介面只會顯示已核准的資產。 這些資產可能包括影像、影片或任何其他數位內容。 Content Hub可增強協助工具及適應能力，以進行有效的資產分發。

您可以使用Content Hub下載單一或多個資產及其可用的轉譯。

## 下載資產及其轉譯 {#download-asset-renditions}

若要下載資產及其轉譯，請執行以下步驟：

1. 按一下資產以檢視其屬性。

1. 按一下![下載](/help/assets/assets/download-icon.svg)開始下載程式。 「下載」面板會列出所有可用的資產轉譯（原始+其他轉譯）。

   >[!NOTE]
   >
   只有在使用[組態](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)使用者介面啟用轉譯的可見度時，才會顯示轉譯。

1. 選取轉譯並按一下&#x200B;**[!UICONTROL 下載]**。

   ![下載單一資產轉譯](/help/assets/assets/download-single-asset-renditions.png)


如果您正在下載授權資產，請選取&#x200B;**[!UICONTROL 我已閱讀並接受上述條款與條件]**，然後按一下&#x200B;**[!UICONTROL 下載]**。 您也可以按一下&#x200B;**[!UICONTROL 條款與條件]**&#x200B;以檢視資產授權。 只有在資產已使用Assetsas a Cloud Service製作環境核準時，才會顯示授權預覽。 如需詳細資訊，請參閱[管理 Content Hub 上的授權資產](/help/assets/manage-licensed-assets-on-content-hub.md)。

## 下載多個資產及其轉譯 {#download-multiple-assets-renditions}

若要下載多個資產及其轉譯，請執行以下步驟：

1. 選取資產並按一下![下載](/help/assets/assets/download-icon.svg) **[!UICONTROL 下載]**。 [!UICONTROL 下載資產]畫面會顯示，列出所有選取的資產。
1. 按一下&#x200B;**[!UICONTROL 下載]**，從各種下載選項中選取開始下載：

   * **下載[!UICONTROL 原始資產]**：選取此選項即可以原始格式下載選取的資產。
   * **僅下載[!UICONTROL 轉譯]**：選取此選項可下載原始資產以外所有可用的資產轉譯。
   * **下載[!UICONTROL 原始與所有轉譯]**：選取此選項可下載所選資產的原始與轉譯。

     ![下載多個轉譯](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     只有在使用[組態](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)使用者介面啟用轉譯的可見度時，才會顯示轉譯。

   如果任何選取的資產是授權資產，請按一下左窗格中的資產授權以檢視其預覽，這可讓您選取&#x200B;**[!UICONTROL 我已閱讀並接受上述條款與條件]**，然後按一下&#x200B;**[!UICONTROL 下載]**。 只有在資產已使用Assetsas a Cloud Service製作環境核準時，才會顯示授權預覽。 如需詳細資訊，請參閱[管理 Content Hub 上的授權資產](/help/assets/manage-licensed-assets-on-content-hub.md)。

   ![下載多個授權](/help/assets/assets/download-multiple-license.png)

<!--1. On the Content Hub homepage, select the asset and click **Download**. The **Download assets** dialog box displays a license or list of licenses associated with the selected assets in the left pane. 
1. Click a license in the left pane to see its PDF in the middle pane and the associated assets with it in the right pane. The license PDF preview is displayed only if the license is approved in your Assets as a Cloud Service environment. [Approve the license PDFs](/help/assets/approve-assets-content-hub.md) of the selected assets to see their previews.
1. Optional: Click ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the dialog box.
1. Select **I have read and accept all the terms and conditions mentioned above.** 
1. Click **Download** to download the selected assets.-->

<!---This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the preview of the associated assets to the license in the right. Reviewed licenses are highlighted in light blue.


The dialog box that displays depends on whether the download list includes expired assets or only non-expired assets. <br/>
**Download expired assets dialog box:** This dialog box displays the expired assets' preview along with their expiry date in the left pane. The expired assets' count out of total selected displays in the right pane. Click **Proceed with all assets** to download expired assets with other assets (if present). The Download assets dialog box displays. See the [Download assets dialog box](#Download-asset-dialog-box) to proceed further.
    
    >[!NOTE]
    >
    >[Enable the download option for expired assets](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) to download them. Only expired assets that have enabled downloading are available for download.

   <a id="Download-asset-dialog-box"></a> **Download assets dialog box:** This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the associated assets' preview and their count in the right pane. Reviewed licenses are highlighted in light blue.

    >[!NOTE]
    >
    > The **Download Asset dialog box** previews licensing terms and conditions only for approved licenses. [Approve the assets' licenses](/help/assets/approve-assets-content-hub.md) before downloading them to preview their licensing terms in the **Download Asset dialog box**.

1. Click  ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the download dialog box. 

1. Accept the terms and conditions and then click **Download** to download assets associated with the available licenses in the left pane.-->
<!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

<!---
### Download non-licensed Assets {#download-non-licensed-assets}

 To download non-licensed assets, select the assets and click ![download](/help/assets/assets/download-icon.svg) from the top rail.-->








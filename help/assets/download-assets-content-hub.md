---
title: 從Content Hub下載資產
description: 瞭解如何從Content Hub入口網站下載資產
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: e108d25f3cdc025e0fbe8010854f245f62786baf
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 10%

---

# 從Content Hub下載資產 {#download-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 與 Edge Delivery Services 整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

<!-- ![Download assets](assets/download-asset.jpg) -->
![下載資產](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>現已提供 PDF 格式的 Content Hub 指南。下載完整指南，並使用 Adobe Acrobat AI 助理來回答您的查詢問題。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub可讓您下載和共用資產。 Content Hub使用者介面只會顯示已核准的資產。 這些資產可能包括影像、影片或任何其他數位內容。 Content Hub可增強協助工具及適應能力，以進行有效的資產分發。

您可以使用Content Hub下載單一或多個資產及其可用的轉譯。

檢視Content Hub](#types-of-renditions)中可用的[轉譯型別。

## 下載資產及其轉譯 {#download-asset-renditions}

若要下載資產及其轉譯，請執行以下步驟：

1. 按一下資產以檢視其屬性。

1. 按一下![下載](/help/assets/assets/download-icon.svg)開始下載程式。 「下載」面板會列出所有可用的資產轉譯。

   >[!NOTE]
   >
   >* 只有在使用[組態](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)使用者介面啟用轉譯的可見度時，才會顯示轉譯。
   >* 您可以在下載資產時下載所有[靜態、動態和智慧型裁切轉譯](#types-of-renditions)。

1. 選取一或多個轉譯並按一下&#x200B;**[!UICONTROL 下載]**。

   ![下載單一資產轉譯](/help/assets/assets/download-single-asset-renditions.png)


如果您正在下載授權資產，請選取&#x200B;**[!UICONTROL 我已閱讀並接受上述條款與條件]**，然後按一下&#x200B;**[!UICONTROL 下載]**。 您也可以按一下&#x200B;**[!UICONTROL 條款與條件]**&#x200B;以檢視資產授權。 只有在資產已使用Assets as a Cloud Service製作環境核準時，才會顯示授權預覽。 如需詳細資訊，請參閱[管理 Content Hub 上的授權資產](/help/assets/manage-licensed-assets-on-content-hub.md)。

>[!NOTE]
>
> 有權存取[具有Open API功能的Dynamic Media ](/help/assets/dynamic-media-open-apis-overview.md)的使用者可以檢視及下載動態和智慧型裁切轉譯。

## 下載多個資產及其轉譯 {#download-multiple-assets-renditions}

若要下載多個資產及其轉譯，請執行以下步驟：

1. 選取資產並按一下![下載](/help/assets/assets/download-icon.svg) **[!UICONTROL 下載]**。 [!UICONTROL 下載資產]畫面會顯示，列出所有選取的資產。
1. 按一下&#x200B;**[!UICONTROL 下載]**，從各種下載選項中選取開始下載：

   * **下載[!UICONTROL 原始資產]**：選取此選項即可以原始格式下載選取的資產。
   * **僅下載[!UICONTROL 靜態轉譯]**：選取此選項可下載原始資產以外所有可用的資產靜態轉譯。
   * **下載[!UICONTROL 原始和靜態轉譯]**：選取此選項可下載所選資產的原始和靜態轉譯。

     ![下載多個轉譯](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     >* 只有在使用[組態](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)使用者介面啟用轉譯的可見度時，才會顯示轉譯。
     >* 您只能在下載多個資產時下載[靜態轉譯](#types-of-renditions)。

   如果任何選取的資產是授權資產，請按一下左窗格中的資產授權以檢視其預覽，這可讓您選取&#x200B;**[!UICONTROL 我已閱讀並接受上述條款與條件]**，然後按一下&#x200B;**[!UICONTROL 下載]**。 只有在資產已使用Assets as a Cloud Service製作環境核準時，才會顯示授權預覽。 如需詳細資訊，請參閱[管理 Content Hub 上的授權資產](/help/assets/manage-licensed-assets-on-content-hub.md)。

   <!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

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


## 轉譯型別 {#types-of-renditions}

資產轉譯是資產原始檔案的不同表示方式。 這些可能包括縮圖、網頁或行動裝置的最佳化版本、加注水標或受DRM保護的檔案，甚至包括動態元素，例如智慧型裁切。 它們不需要符合原始檔案型別，而是在各種使用案例中用於代表資產。

深入瞭解[在Experience Manager Assets](/help/assets/renditions.md)中檢視及管理轉譯。

[!DNL Experience Manager Assets]支援下列轉譯型別：

* [靜態轉譯](/help/assets/renditions.md#static-renditions)：靜態轉譯是數位資產的預先建立版本，通常在資產擷取或修改期間產生。 它們針對特定用途和平台進行最佳化，例如網頁縮圖、回應式設計的行動裝置友好格式，或列印的高解析度檔案，提供簡化且一致的體驗。

* [動態轉譯](/help/assets/renditions.md#dynamic-renditions)：動態轉譯是資產的即時、自訂版本，可執行各種動作，例如根據不同的裝置解析度調整影像大小或裁切以符合各種外觀比例。 這些轉譯可讓您根據更廣泛的需求，提供個人化和最佳化的體驗。 資產的動態轉譯是在[!DNL Adobe Experience Manager Assets]作者環境中建立。 如需啟用動態轉譯所需步驟的詳細資訊，請參閱[啟用動態轉譯](#enable-dynamic-media-renditions)。

* [智慧型裁切](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)：智慧型裁切在裁切程式進行期間，只著重於資產的重要部分。 適用於的Dynamic Media智慧型裁切運用由Adobe Sensei提供支援的人工智慧來追蹤地標，確保我們的資產在所有熒幕大小上看起來都最理想。 [!DNL Adobe Experience Manager]智慧型裁切會顯示資產轉譯的寬度和高度以及標題。 如需詳細資訊，請參閱[搭配AEM Assets Dynamic Media使用智慧型裁切](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)。

  智慧型裁切轉譯會顯示，而且只有在您能存取具有OpenAPI功能的[Dynamic Media ](/help/assets/dynamic-media-open-apis-overview.md)時，才能下載。 智慧型裁切轉譯僅適用於影像資產。

  ![轉譯型別](/help/assets/assets/renditions-types.png)

### 啟用動態轉譯 {#enable-dynamic-media-renditions}

若要啟用動態轉譯：

1. 確定您具有[Dynamic Media的OpenAPI功能](/help/assets/dynamic-media-open-apis-overview.md)存取權。

   一旦您擁有使用OpenAPI功能的Dynamic Media存取權，所有標籤為`Approved`的資產都可使用Dynamic Media進行公開傳送。

1. 將資產](/help/assets/approve-assets-content-hub.md#set-approval-target)的[核准目標設定為Content Hub，僅核准Content Hub的資產。

1. 啟用[組態](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub)使用者介面之&#x200B;**[!UICONTROL 轉譯]**&#x200B;索引標籤中可用的&#x200B;**[!UICONTROL 啟用轉譯可用性]**&#x200B;切換。

1. 重新儲存現有的影像預設集，以便在Content Hub上使用。 此變數僅適用於您最近使用OpenAPI加入Dynamic Media時。

   若要重新儲存現有的影像預設集，請導覽至[管理]檢視，並選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 影像預設集]**。 選取預設集，按一下&#x200B;**[!UICONTROL 編輯]**，然後按一下&#x200B;**[!UICONTROL 儲存]**。



   >[!NOTE]
   > 
   > 動態轉譯僅適用於影像資產。




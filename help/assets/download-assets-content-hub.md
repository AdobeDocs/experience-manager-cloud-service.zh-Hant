---
title: 從Content Hub下載資產
description: 瞭解如何從Content Hub入口網站下載單一或多個資產及其轉譯。
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 1%

---

# 從Content Hub下載資產 {#download-assets}

[!DNL Content Hub]可讓您下載及共用您的資產。 [!DNL Content Hub]使用者介面只會顯示已核准的資產。 這些資產可能包括影像、影片或任何其他數位內容。 [!DNL Content Hub]增強了有效資產分配的協助工具與適應性。

您可以使用[!DNL Content Hub]下載單一或多個資產及其可用的轉譯。

檢視Content Hub[&#128279;](#types-of-renditions)中可用的轉譯型別。

## 下載一個或多個資產及其轉譯 {#download-asset-renditions}

若要下載一個或多個資產及其轉譯，請執行以下步驟：

1. 若要下載資產，請選取資產卡上可用的![下載](/help/assets/assets/download-icon.svg)以預覽資產，選取可用的轉譯並按一下對話方塊中的&#x200B;**[!UICONTROL 下載]**&#x200B;選項，將選取的轉譯下載為ZIP檔。 如果對話方塊顯示資產授權（針對授權資產），請接受授權條款與條件，然後按一下&#x200B;**[!UICONTROL 下載]**。
   ![](/help/assets/assets/download-an-asset-CH-from-asset-card.png)

   或者，按一下資產縮圖，然後選取![下載](/help/assets/assets/download-icon.svg)，在下載之前，先選取並檢視對話方塊上的可用轉譯。

1. 若要下載多個資產，請選取資產，按一下![下載](/help/assets/assets/download-icon.svg) **[!UICONTROL 下載]**，並檢閱&#x200B;**[!UICONTROL 下載資產]**&#x200B;對話方塊中選取的資產清單。 按一下資產旁的![取消選取](/help/assets/assets/Close.svg)，從清單中取消選取該資產。 選取一或多個轉譯，然後按一下[下載] **&#x200B;**，將轉譯下載為單一ZIP檔。 選取&#x200B;**[!UICONTROL 智慧型裁切]**&#x200B;和&#x200B;**[!UICONTROL 靜態轉譯]**&#x200B;會下載每個選取資產的所有可用靜態和智慧型裁切轉譯。
   ![下載多個資產](/help/assets/assets/download-multiple-assets-CH.png)
下載進行時，您可以繼續使用[!DNL Content Hub]。 Content Hub不會在下載過程中中斷您的工作流程。
   ![下載多個資產](/help/assets/assets/download-assets-notification-ch.png)
如果&#x200B;**[!UICONTROL 下載資產]**&#x200B;對話方塊顯示資產授權，然後從左窗格（[!UICONTROL T&amp;C檔案]區段）選取每個授權，以預覽授權並在對話方塊的中間窗格中顯示與授權關聯的選取資產。 檢閱每個授權後，選取轉譯，按一下&#x200B;**[!UICONTROL 我已閱讀並接受上述條款與條件]**，並選取&#x200B;**[!UICONTROL 下載]**&#x200B;以下載它們。
   ![下載多個資產](/help/assets/assets/download-multiple-licensed-assets-CH.png)

   >[!NOTE]
   >
   >* 只有在使用[[!UICONTROL 組態]](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub)使用者介面啟用轉譯的可見度時，才會顯示轉譯。
   >* 有權存取[[!DNL Dynamic Media with Open API capabilities]](/help/assets/dynamic-media-open-apis-overview.md)的使用者可以檢視及下載動態和智慧型裁切轉譯。
   >* 只有當資產已使用[!DNL Assets as a Cloud Service]編寫環境核準時，才會顯示授權預覽。 如需詳細資訊，請參閱[管理 Content Hub 上的授權資產](/help/assets/manage-licensed-assets-on-content-hub.md)。

<!--

## Download an asset and its renditions {#download-asset-renditions} 

To download an asset and its renditions, execute the following steps: 

1. Click the asset to view its properties.

1. Click ![download](/help/assets/assets/download-icon.svg) to see the list of available asset renditions in the **[!UICONTROL Download]** panel.

   >[!NOTE]
   >
   >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
   >* You can download all [static, dynamic, and smart crop renditions](#types-of-renditions) while downloading an asset.

1. Select one or more renditions and click **[!UICONTROL Download]** to download the selected renditions as a zip file. 
While downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** before clicking **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![Download single asset renditions](/help/assets/assets/download-single-asset-renditions.png)


If you are downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
> The users with access to [Dynamic Media with Open API capabilities](/help/assets/dynamic-media-open-apis-overview.md) can view and download dynamic and smart crop renditions.

## Download multiple assets and their renditions {#download-multiple-assets-renditions} 

To download multiple assets and their renditions, execute the following steps: 

1. Select the assets and click ![download](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]**. The [!UICONTROL Download assets] screen displays listing all the selected assets. 
1. Click **[!UICONTROL Download]** to select from the various download options to begin download:

    * **Download [!UICONTROL Originals]**: Select this option to download the selected assets in the original form.
    * **Download [!UICONTROL Static Renditions only]**: Select this option to download all available static renditions of assets except the original assets.
    * **Download [!UICONTROL Originals & Static Renditions]**: Select this option to download both original and static renditions of the selected assets. 

      ![Download multiple renditions](/help/assets/assets/download-multiple-renditions.png)

      >[!NOTE]
      >
      >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
      >* You can only download [static renditions](#types-of-renditions) while downloading multiple assets.

    If any of the selected asset is a licensed asset, click the license of the asset in left pane to see its preview, which enables you to select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

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

深入瞭解[在 [!DNL Experience Manager Assets]](/help/assets/renditions.md)中檢視及管理轉譯。

[!DNL Experience Manager Assets]支援下列轉譯型別：

* [靜態轉譯](/help/assets/renditions.md#static-renditions)：靜態轉譯是數位資產的預先建立版本，通常在資產擷取或修改期間產生。 它們針對特定用途和平台進行最佳化，例如網頁縮圖、回應式設計的行動裝置友好格式，或列印的高解析度檔案，提供簡化且一致的體驗。

* [動態轉譯](/help/assets/renditions.md#dynamic-renditions)：動態轉譯是資產的即時、自訂版本，可執行各種動作，例如根據不同的裝置解析度調整影像大小或裁切以符合各種外觀比例。 這些轉譯可讓您根據更廣泛的需求，提供個人化和最佳化的體驗。 資產的動態轉譯是在[!DNL Adobe Experience Manager Assets]作者環境中建立。 如需啟用動態轉譯所需步驟的詳細資訊，請參閱[啟用動態轉譯](#enable-dynamic-media-renditions)。

* [智慧型裁切](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles)：智慧型裁切在裁切程式進行期間，只著重於資產的重要部分。 Dynamic Media智慧型裁切運用由Adobe Sensei提供支援的人工智慧來追蹤地標，確保我們的資產在所有熒幕大小上都能呈現最佳效果。 [!DNL Adobe Experience Manager]智慧型裁切會顯示資產轉譯的寬度和高度以及標題。 如需詳細資訊，請參閱[搭配AEM Assets Dynamic Media使用智慧型裁切](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use)。

  智慧型裁切轉譯會顯示，而且只有在您能存取具有OpenAPI功能的[Dynamic Media ](/help/assets/dynamic-media-open-apis-overview.md)時，才能下載。 智慧型裁切轉譯僅適用於影像資產。

  ![轉譯型別](/help/assets/assets/renditions-types.png)

### 啟用動態轉譯 {#enable-dynamic-media-renditions}

若要啟用動態轉譯：

1. 確定您具有[Dynamic Media的OpenAPI功能](/help/assets/dynamic-media-open-apis-overview.md)存取權。

   一旦您擁有使用OpenAPI功能的Dynamic Media存取權，所有標籤為`Approved`的資產都可使用Dynamic Media進行公開傳送。

1. 將資產[&#128279;](/help/assets/approve-assets-content-hub.md#set-approval-target)的核准目標設定為Content Hub，僅核准Content Hub的資產。

1. 啟用[組態](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub)使用者介面之&#x200B;**[!UICONTROL 轉譯]**&#x200B;索引標籤中可用的&#x200B;**[!UICONTROL 啟用轉譯可用性]**&#x200B;切換。

1. 重新儲存現有的影像預設集，以便在Content Hub上使用。 此變數僅適用於您最近使用OpenAPI加入Dynamic Media時。

   若要重新儲存現有的影像預設集，請導覽至[管理]檢視，並選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 影像預設集]**。 選取預設集，按一下&#x200B;**[!UICONTROL 編輯]**，然後按一下&#x200B;**[!UICONTROL 儲存]**。



   >[!NOTE]
   > 
   > 動態轉譯僅適用於影像資產。




---
title: 在 [!DNL the Content Hub]中共用Assets
description: 在 [!DNL the Content Hub]中共用Assets
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 0e66b355d09e2fd2c4c8a5ddacc9b2d033b41bf2
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 17%

---

# 在 Content Hub 中分享資產 {#search-assets-as-a-link}

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

![共用資產橫幅影像](assets/share-assets-banner.png)

>[!AVAILABILITY]
>
>現已提供 PDF 格式的 Content Hub 指南。下載完整指南，並使用 Adobe Acrobat AI 助理來回答您的查詢問題。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

建立所選資產的連結，以便輕鬆與他人共用。 以授權[!DNL Content Hub]使用者的身分，選取您[!DNL Content Hub]環境中可用的一或多個資產、產生連結，然後傳送給其他私人或公開使用者。

## 先決條件 {#prerequisites}

[Content Hub使用者](deploy-content-hub.md#onboard-content-hub-users)可以建立所選資產的連結，並與其他使用者共用。

## 共用資產 {#share-assets}

若要與私人或公開使用者共用一或多個資產，請執行以下步驟：
1. 導覽至您的[!DNL Content Hub]首頁，選取一或多個資產並按一下![共用](/help/assets/assets/share.svg) **[!UICONTROL 共用]**，以在&#x200B;**[!UICONTROL 共用資產]**&#x200B;對話方塊中顯示單一選取的資產或多個選取的資產清單。
您也可以選取並共用![集合](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL 集合]**&#x200B;中可用的資產。
1. 檢視資產或檢閱&#x200B;**[!UICONTROL 共用資產]**&#x200B;對話方塊中可用的資產清單。 按一下資產旁的![取消選取](/help/assets/assets/Close.svg)，從清單中取消選取該資產。
1. 選取&#x200B;**[!UICONTROL 有效期]**&#x200B;並按一下&#x200B;**[!UICONTROL 產生私人連結]**&#x200B;以產生與私人使用者共用的連結。 私人使用者登入其[!DNL Content Hub]環境以存取共用資產頁面。
   ![私人與公開連結](/help/assets/assets/private-and-public-link.png)
啟用&#x200B;**[!UICONTROL 公用連結]**&#x200B;切換，選取&#x200B;**[!UICONTROL 有效期間]**，然後按一下&#x200B;**[!UICONTROL 產生公用連結]**&#x200B;以產生要與公用使用者共用的連結。 公用使用者以來賓身分存取共用資產頁面，無需登入[!DNL Content Hub]。
   ![私人與公開連結](/help/assets/assets/public-and-private-link.png)

   >[!NOTE]
   > 
   > [從設定頁面](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing)啟用公用連結共用，以在&#x200B;**[!UICONTROL 共用資產]**&#x200B;對話方塊上顯示&#x200B;**[!UICONTROL 公用連結]**&#x200B;切換按鈕。

## 從資產的預覽頁面共用資產 {#share-asset-from-preview-page}

執行以下步驟，在預覽資產時共用資產：

1. 導覽至[!DNL Content Hub]首頁，然後按一下資產縮圖以預覽資產，並在對話方塊的右側窗格中顯示功能表選項。
1. 選取![共用](/help/assets/assets/share.svg)以顯示&#x200B;**[!UICONTROL 共用]**&#x200B;面板。
   預覽資產時![共用資產](/help/assets/assets/share-assets-from-share-panel.png)
1. 依照[共用資產](#share-assets)區段中的步驟3，從此&#x200B;**[!UICONTROL 共用]**&#x200B;面板產生並共用資產連結（私人或公開）。

## 存取已共用的資產 {#access-shared-assets}

透過連結存取共用資產頁面，並執行下列動作：

* 選取一或多個資產，然後按一下[下載] ![](/help/assets/assets/download-icon.svg) **[!UICONTROL &lbrace;下載]**，從可用的下載選項中選取[原始] &rbrack;**、[靜態]**&#x200B;**或兩個轉譯。**
  ![](/help/assets/assets/download-shared-assets.png)
* 按一下資產縮圖以檢視資產的中繼資料。
* 在共用資產頁面（[透過私人連結存取](#share-assets)）上，按一下資產縮圖，然後選取![下載](/help/assets/assets/download-icon.svg)，以選取並檢視&#x200B;**[!UICONTROL 下載]**&#x200B;面板上可用的資產動態轉譯，然後再選取並下載。
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)






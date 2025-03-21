---
title: 在 [!DNL the Content Hub]中共用Assets
description: 在 [!DNL the Content Hub]中共用Assets
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 11%

---

# 在 Content Hub 中分享資產 {#search-assets-as-a-link}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
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

透過連結共用資產是讓[!DNL the Content Hub]使用者可以使用資源的便利方式。 功能可讓獲授權的使用者存取及下載與其共用的資產。 從共用連結下載資產時，[!DNL the Content Hub]會使用非同步服務，提供更快速且無中斷的下載。

## 先決條件 {#prerequisites}

[Content Hub使用者](deploy-content-hub.md#onboard-content-hub-users)可以執行本文中提到的動作。

## 共用單一資產 {#share-a-single-asset}

您可以透過執行以下步驟來共用單一資產：

1. 選取資產並按一下![共用圖示](assets/share.svg)圖示以共用資產。

   ![共用單一資產](assets/sharing-single-asset.png)

1. 使用&#x200B;**[!UICONTROL 到期]**&#x200B;欄位來指定連結的到期日。 選取其中一個可用選項，例如24小時、1週、30天、90天、1年或指定自訂日期。

1. 按一下&#x200B;**[!UICONTROL 複製共用連結]**。 接著，您就可以與收件者共用複製的連結。

## 共用多個資產 {#share-multiple-assets}

[!DNL The Content Hub]可讓您透過共用連結共用多個資產。 執行以下步驟：

1. 選取您需要與授權收件者共用的資產。 您可以逐一選取多個資產，或按一下[全選] **[!UICONTROL 一次選取所有可用資產]**。 **[!UICONTROL 全選]**&#x200B;選項只有在您至少選取一個資產時才會顯示。

1. 按一下![共用圖示](assets/share.svg)圖示。

   ![共用多個資產](assets/sharing-multiple-assets.png)

1. 在預覽區段中，您也可以根據需求刪除資產。 使用&#x200B;**[!UICONTROL 到期]**&#x200B;欄位來指定連結的到期日。 選取其中一個可用選項，例如24小時、1週、30天、90天、1年或指定自訂日期。

1. 按一下&#x200B;**[!UICONTROL 複製共用連結]**。 接著，您就可以與收件者共用複製的連結。

## 預覽和共用資產 {#preview-assets}

您可以預覽，在與連結收件者共用前，檢視您要共用的數位資產的外觀。 按一下您需要預覽的資產。 [!DNL Content Hub]會顯示資產](asset-properties-content-hub.md)的[詳細檢視。

按一下![共用圖示](assets/share.svg)圖示以共用資產。 使用&#x200B;**[!UICONTROL 到期]**&#x200B;欄位來指定連結的到期日。 選取其中一個可用選項，例如24小時、1週、30天、90天、1年或指定自訂日期。 按一下&#x200B;**[!UICONTROL 複製共用連結]**。 接著，您就可以與收件者共用複製的連結。

在Content Hub中![預覽資產](assets/preview-assets-content-hub.png)

## 存取已共用的資產 {#access-shared-assets}

共用資產的連結後，獲授權的收件者可按一下該連結，即可在網頁瀏覽器中預覽或下載共用的資產。

按一下共用連結，然後按一下資產卡上可用的下載圖示來下載資產。  您也可以選取多個資產並按一下&#x200B;**[!UICONTROL 下載]**。<!--You can either download original assets or Original+Renditions of an asset.--> [!DNL The Content Hub]會將每個資產逐一下載到本機檔案系統。

![存取共用的連結](assets/content-hub-access-shared-links.png)

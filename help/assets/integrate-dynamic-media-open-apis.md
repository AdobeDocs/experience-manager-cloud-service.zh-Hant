---
title: 將 AEM Assets 與下游應用程式整合
description: 將 AEM Assets 與下游應用程式整合
role: User
exl-id: abd48b5d-2b43-453c-8eb6-31ff509245ca
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 33%

---

# 將 AEM Assets 與下游應用程式整合 {#integrate-dynamic-media-open-apis}

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

>[!AVAILABILITY]
>
>具有 OpenAPI 功能的 Dynamic Media 指南現已提供 PDF 格式。下載完整指南，並使用 Adobe Acrobat AI 助理來回答您的查詢問題。
>
>[!BADGE 具有 OpenAPI 功能的 Dynamic Media 指南 PDF]{type=Informative url="https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

Experience Manager資產存放庫中所有可用的[已核准資產](/help/assets/approve-assets.md)都可傳送給下游應用程式。

您可以使用搜尋和傳送API將您自己的自訂使用者介面與Experience Manager Assets存放庫整合，或使用Adobe的微前端資產選擇器。

![與AEM Assets存放庫整合](assets/asset-selector-integration.png)

這些API可讓您從AEM Assets存放庫搜尋已核准的資產，然後使用傳送URL將資產傳送給下游應用程式。 如需詳細資訊，請參閱[搜尋](/help/assets/search-assets-api.md)和[傳遞](/help/assets/deliver-assets-apis.md) API。

Adobe的Micro-Frontend Asset Selector提供使用者介面，可輕鬆與[!DNL Experience Manager Assets as a Cloud Service]存放庫整合，因此您可以瀏覽或搜尋存放庫中可用的已核准數位資產，並在您的應用程式編寫體驗中使用這些資產。 如需詳細資訊，請參閱[微前端資產選擇器](/help/assets/overview-asset-selector.md)。

>[!MORELIKETHIS]
>
* [整合資產選擇器與各種應用程式](/help/assets/integrate-asset-selector.md)
* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
* [資產選擇器自訂](/help/assets/asset-selector-customization.md)

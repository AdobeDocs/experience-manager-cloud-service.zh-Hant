---
title: 設定資產上傳限制
description: 設定Adobe Experience Manager Assets以根據MIME型別限制使用者可以上傳的資產型別。 它有助於防止意外上傳不需要的格式和惡意檔案。
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
feature: Upload, Asset Ingestion
role: User, Admin, Developer
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 15%

---

# 設定資產上傳限制 {#configure-asset-upload-restrictions}

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

您可以設定Adobe Experience Manager Assets根據MIME型別限制使用者可以上傳的資產型別。

>[!IMPORTANT]
>
>依預設，Experience Manager Assets允許使用者上傳所有MIME型別的資產。 不過，您可以進行設定，限制使用者只能上傳特定MIME型別的檔案。

## 先決條件 {#prerequisites-asset-upload-restrictions}

您必須有管理員許可權才能設定資產上傳限制。

## 套用資產上傳限制 {#apply-restrictions-asset-uploadsssssss}

若要設定[!DNL Experience Manager]以限制使用者上傳特定MIME型別的檔案：

1. 導覽至&#x200B;**[!UICONTROL 工具> Assets > Assets設定]**。

1. 按一下&#x200B;**[!UICONTROL 上傳限制]**。

1. 按一下&#x200B;**[!UICONTROL 新增]**&#x200B;以定義允許的MIME型別。

1. 在文字方塊中指定MIME型別。 您可以再按一下[新增&#x200B;**&#x200B;**]來指定更多允許的MIME型別。 您也可以按一下![刪除圖示](assets/delete-icon.svg)，從清單中刪除任何MIME型別。

1. 按一下「**[!UICONTROL 儲存]**」。

**範例1：允許將所有影像和PDF檔案上傳至Experience Manager Assets**

若要允許將所有格式的影像和PDF檔案上傳到Experience Manager Assets，請執行下列設定：

![資產上傳限制](assets/asset-upload-restrictions.png)

`image/*`作為MIME型別允許上傳所有格式的影像。 `application/pdf`作為MIME型別，允許將PDF檔案上傳至Experience Manager Assets。

如果您嘗試上傳未包含在允許MIME型別清單中的檔案，Experience Manager Assets會顯示下列錯誤訊息：

![限制的檔案](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov`參考的檔案名稱未包含在允許的MIME型別中。

**範例2：允許上傳特定影像格式至Experience Manager Assets**

若要將特定影像格式新增至允許的MIME型別，並限制上傳所有其他資產格式，請執行下列設定：

![資產限制](assets/asset-restrictions.png)

您可以根據影像中描述的設定，將。JPG、.PNG及。GIF格式的影像上傳至Experience Manager Assets。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

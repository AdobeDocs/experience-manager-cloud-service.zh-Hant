---
title: 使用 Vanilla JS 整合資產選擇器
description: 整合資產選擇器與各種Adobe、非Adobe及協力廠商應用程式。
role: Admin, User
exl-id: 1c0051a3-549c-4783-9fc1-594f424a70c3
source-git-commit: 08fc43bc8edeea91bfeb01f053d435e136658e7f
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 67%

---

# 使用 Vanilla JS 整合資產選擇器 {#integration-using-vanilla-js}

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

您可以將任何[!DNL Adobe]或非Adobe應用程式與[!DNL Experience Manager Assets]存放庫整合，並從應用程式中選取資產。 請參閱[資產選擇器與各種應用程式的整合](#asset-selector-integration-with-apps)。

匯入資產選擇器套件，並使用 Vanilla JavaScript 程式庫連接到 Assets as a Cloud Service，便完成了整合作業。編輯`index.html`或您應用程式內的任何適當檔案，以：

* 定義身份驗證詳細資訊
* 存取 Assets as a Cloud Service 存放庫
* 設定資產選擇器顯示屬性

在以下情況下，您可以在不定義某些 IMS 屬性的情況下執行身份驗證：

* 在 [!DNL Adobe] [Unified Shell](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell.html?lang=zh-Hant) 之上整合一個應用程式時。
* 您已經具有針對身份驗證產生的一個 IMS 語彙基元。

## 整合Asset Selector與各種應用程式 {#asset-selector-integration-with-apps}

您可以整合Asset Selector與各種應用程式，例如：

* [將資產選擇器與 [!DNL Adobe] 應用程式整合](/help/assets/integrate-asset-selector-adobe-app.md)
* [整合資產選擇器與非 Adobe 應用程式](/help/assets/integrate-asset-selector-non-adobe-app.md)
* [整合Dynamic Media與OpenAPI功能](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [資產選擇器自訂](/help/assets/asset-selector-customization.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
>* [整合資產選擇器與具備 OpenAPI 功能的 Dynamic Media](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)

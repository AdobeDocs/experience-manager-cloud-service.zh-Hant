---
title: 使用Media Library進行基本的數位資產管理
description: '[!DNL Experience Manager Assets]和媒體庫用於資產管理。'
contentOwner: AG
feature: Asset Management, Publishing
role: User, Architect, Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 9%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# 使用Media Library進行基本資產管理 {#manage-assets-using-media-library}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/medialibrary.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |

[!DNL Adobe Experience Manager]平台提供管理資產的不同功能。 媒體庫可讓使用者將少量資產上傳到存放庫、搜尋並使用網頁中的資產，以及完成資產的簡單資產管理任務。

媒體庫是輕量版數位資產管理(DAM)解決方案，附帶[!DNL Adobe Experience Manager Sites]授權套件。 [!DNL Sites]是Web內容管理(WCM)產品。 媒體庫可與Experience Manager的所有功能搭配使用。

[!DNL Adobe Experience Manager Assets]授權可單獨購買。 [!DNL Experience Manager Assets]可透過企業使用案例、中繼資料、結構描述、搜尋和使用者介面的自訂，以及Media Library提供的許多其他功能，提供強大的資產處理能力。

## 授權需求 {#avail-media-library-license}

擁有[!DNL Sites]授權的客戶有權使用媒體庫。 它適用於[!DNL Experience Manager]的所有元件。

媒體櫃會安裝為Sites的一部分。 除了Sites授權和安裝以外，不需要額外的授權或套件。

## [!DNL Assets]與Media Library {#assets-and-media-library}

Experience Manager Assets提供企業級DAM功能。 Assets功能是在單一套件中與[!DNL Experience Manager]一併提供。 但是，尚未購買Assets授權的使用者無權使用進階DAM功能。 如果沒有Assets授權，則只能使用[媒體庫功能](#use-media-library)。

若要防止您未授權的[!DNL Assets]功能遭到非預期使用，請從[!DNL Experience Manager]移除所有[!DNL Assets]專屬的工作流程、元件、分類、選項及[!DNL Assets]管理員。 這麼做可防止您的使用者意外使用您未授權的[!DNL Assets]功能。

## 使用Media Library {#use-media-library}

Media Library涵蓋下列使用案例：

* 為使用[!DNL Adobe Experience Manager Sites]建立的網頁提供基本DAM功能。
* 使用[!DNL Adobe Experience Manager Forms]建立的最適化表單和通訊。
* 使用[!DNL Adobe Experience Manager Screens]建立的數位熒幕體驗。
* 用於Headless作業的[!DNL Assets] HTTP REST API。

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions

-->

若要使用媒體櫃功能，您可以使用預設的[!DNL Experience Manager]使用者介面。 媒體櫃是[!DNL Experience Manager Sites]安裝的一部分，不需要個別介面或附加元件。 使用現有介面，「媒體庫」使用者有權完成下列工作：

* 建立資料夾以組織資產。
* 上傳資產。
* 發佈資產。
* 編輯、移動和複製資產。
* 瀏覽、篩選和搜尋（包括相似度搜尋）資產。
* 新增值至中繼資料欄位，並編輯其中繼資料欄位中預設可在資產[!UICONTROL 屬性]頁面的[!UICONTROL 基本]索引標籤中取得的值（智慧標籤欄位除外）。
* 新增和刪除靜態轉譯。
* 下載資料夾、資產和資產轉譯。
* 建立資產版本。
* 對資產建立並執行稽核任務。
* 為資產加上註釋。
* 透過「內容尋找器」將資產新增至[!DNL Sites]頁面。
* 使用[!DNL Content Fragments]。
* 在Sites授權底下，針對[!DNL Content Fragments]和參照的媒體資產使用HTTP REST和GraphQL API。
* Marketing Cloud整合。
* 自訂及擴充資產管理使用者介面。
* 存取查詢產生器(API)以擴充搜尋功能。
* 建立靜態標籤。
* 編寫專案和任務。
* 活動資料流（時間軸）。
* 註釋和註解。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>許多進階DAM使用案例已由[!DNL Experience Manager Assets]履行。 媒體庫授權可讓您僅使用媒體庫履行列出的使用案例。 如果未列出使用案例，請勿將其與Media Library授權一起使用。 如有任何疑問，請聯絡客戶支援。

您無法使用智慧標籤、[!DNL Asset]連結、[!DNL Asset]選取器、大量標籤、修改資產工作流程或標準[!DNL Adobe Experience Manager]使用者介面來存取媒體庫，因為沒有[!DNL Assets]授權。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

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

>[!MORELIKETHIS]
>
>* 在 [!DNL Experience Manager Assets][&#128279;](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html?lang=zh-Hant)中的DAM功能
>* [[!DNL Experience Manager] 作為 [!DNL Cloud Service] 產品說明](https://helpx.adobe.com/tw/legal/product-descriptions/adobe-experience-manager-cloud-service.html)

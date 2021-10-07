---
title: 使用Media Library進行基本數位資產管理
description: '[!DNL Experience Manager Assets] 和Media Library進行資產管理。'
contentOwner: AG
feature: Asset Management,Publishing
role: User,Architect,Leader
exl-id: 4737d5ee-9a93-49f3-9f20-d4368e60e9fb
source-git-commit: e294ecdefca89bc3fd16ee2166a1a8418d0237ee
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

<!--

Define Media Lib
Define req for it
Define use cases
Define what is not included

-->

# 使用Media Library進行基本資產管理 {#manage-assets-using-media-library}

[!DNL Adobe Experience Manager] platform提供不同的資產管理功能。Media Library可讓使用者將少量資產上傳至存放庫、搜尋及使用網頁中的資產，並完成資產的簡單資產管理工作。

Media Library是輕量型數位資產管理(DAM)解決方案，隨附[!DNL Adobe Experience Manager Sites]授權。 [!DNL Sites] 是網頁內容管理(WCM)產品。Media Library可搭配所有Experience Manager功能使用。

[!DNL Adobe Experience Manager Assets] 許可證可單獨購買。[!DNL Experience Manager Assets] 可透過企業使用案例、中繼資料的自訂、結構、搜尋和使用者介面，以及Media Library提供的其他功能，來強大處理資產。

## 授權需求 {#avail-media-library-license}

擁有[!DNL Sites]授權的客戶有權使用Media Library。 它適用於[!DNL Experience Manager]的所有元件。

Media Library會隨Sites一併安裝。 除了Sites授權和安裝外，不需要其他授權或套件。

## [!DNL Assets] 與Media Library {#assets-and-media-library}

Experience Manager Assets提供企業級DAM功能。 資產功能透過單一套件[!DNL Experience Manager]提供。 不過，尚未購買Assets授權的使用者無權使用進階DAM功能。 若沒有Assets授權，僅[Media Library功能](#use-media-library)可供使用。

如果要防止意外使用您未獲得許可的[!DNL Assets]功能，請從[!DNL Experience Manager]中刪除所有[!DNL Assets]特定的工作流、元件、分類、選項和[!DNL Assets]管理員。 這麼做可防止使用者意外使用您未授權的[!DNL Assets]功能。

## 使用Media Library {#use-media-library}

Media Library廣泛涵蓋下列使用案例：

* 為使用[!DNL Adobe Experience Manager Sites]建立的網頁提供基本DAM功能。
* 使用[!DNL Adobe Experience Manager Forms]建立的最適化表單和通訊。
* 使用[!DNL Adobe Experience Manager Screens]建立的數位螢幕體驗。
* [!DNL Assets] 無頭操作的HTTP REST API。

<!-- TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.

* Static renditions
* Projects, tasks authoring
* Activity stream (timeline)
* Comments and annotation
-->

若要使用Media Library功能，您可以使用預設的[!DNL Experience Manager]使用者介面。 Media Library是[!DNL Experience Manager Sites]安裝的一部分，不需要單獨的介面或附加元件。 使用現有介面，Media Library使用者有權完成下列工作：

* 建立資料夾以組織資產。
* 上傳資產。
* 發佈資產。
* 編輯、移動和複製資產。
* 瀏覽、篩選和搜尋（包括相似性搜尋）資產。
* 在中繼資料欄位中新增值並編輯值，但「智慧標籤」欄位除外，這些欄位預設可在資產[!UICONTROL 屬性]頁面的[!UICONTROL 基本]標籤中取得。
* 新增和刪除靜態轉譯。
* 下載資料夾、資產和資產轉譯。
* 建立資產版本。
* 建立並執行資產的審核工作。
* 為資產加上注釋。
* 透過「內容尋找器」將資產新增至[!DNL Sites]頁面。
* 使用[!DNL Content Fragments]。
* 在Sites授權下，針對[!DNL Content Fragments]和參考媒體資產使用HTTP REST和GraphQL API。
* Marketing Cloud整合。
* 自訂及擴充資產管理使用者介面。
* 存取查詢產生器(API)以擴充搜尋功能。
* 建立靜態標籤。

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?
As per PM, we must avoid stating such a list, as we don't have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>許多進階DAM使用案例都由[!DNL Experience Manager Assets]履行。 Media Library授權可讓您僅使用Media Library履行列出的使用案例。 如果未列出使用案例，請勿將其用於Media Library授權。 若您有任何疑問，請聯絡客戶支援。

請注意，您無法使用智慧標籤、[!DNL Asset]連結、[!DNL Asset]選擇器、大量標籤、修改資產工作流程，但不具備[!DNL Assets]授權。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [中的DAM功能 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] 產品說明](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-cloud-service.html)


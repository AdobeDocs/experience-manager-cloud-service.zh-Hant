---
title: 適用於  [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service] 的資產選擇器
description: 將資產選擇器與各種Adobe、非Adobe和第三方應用程式整合。
role: Admin, User
exl-id: 1c0051a3-549c-4783-9fc1-594f424a70c3
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 47%

---

# 使用 Vanilla JS 整合資產選擇器 {#integration-using-vanilla-js}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開發人員檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

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
* [Dynamic Media與OpenAPI功能的整合](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)


>[!MORELIKETHIS]
>
>* [資產選擇器自訂](/help/assets/asset-selector-customization.md)
>* [資產選擇器屬性](/help/assets/asset-selector-properties.md)
>* [整合Asset Selector與Dynamic Media以及OpenAPI功能](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)

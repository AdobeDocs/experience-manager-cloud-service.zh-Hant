---
title: '為 [!DNL Edge Delivery Services]編寫內容時整合 [!DNL AEM Assets] '
description: 瞭解如何將 [!DNL AEM Assets] 與 [!DNL Edge Delivery Services]. This integration enables you to integrate [!DNL AEM Assets] 與 [!DNL Microsoft Word] 整合， [!DNL Google Docs], integrate [!DNL AEM Assets] 與 [!DNL Universal Editor], integrate [!DNL Dynamic Media] 與 [!DNL Edge Delivery Services], integrate [!DNL Dynamic Media with OpenAPI capabilities] 與 [!DNL Universal Editor] 整合，以及如何將 [!DNL Dynamic Media with OpenAPI capabilities] 與 [!DNL Microsoft Word] 與 [!DNL Google Docs]整合。
tags: AEM Assets, Edge Delivery Services, Dynamic Media, Dynamic Media with OpenAPI capabilities, Universal Editor, Edge Delivery Services with Universal Editor
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 6%

---


# 為[!DNL Edge Delivery Services]編寫內容時整合[!DNL AEM Assets] {#integrate-aem-assets-with-edge-delivery-services}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
        </td>
         <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
    </tr>
    <tr>
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

![AEM資產與通用編輯器的整合](/help/assets/assets/EDS2.png)

[[!DNL Edge Delivery Services]](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/overview)是一組可撰寫的服務，可讓您在網站上撰寫及傳遞內容的方式上擁有高度彈性。 您可以使用[AEM內容管理](/help/sites-cloud/authoring/author-publish.md)和[使用 [!DNL Universal Editor] 的WYSIWYG製作，以及檔案式製作](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)。

您可以在下列位置編輯內容：

* [[!DNL Microsoft Word]或 [!DNL Google Docs]](#integrate-dynamic-media-with-edge-delivery-services)
* [[!DNL Universal Editor]](#integrate-aem-assets-with-universal-editor-UE)

編輯內容後，您可以將其發佈到Edge Delivery Services。

## 將[!DNL AEM Assets]與[!DNL Edge Delivery Services]的檔案式編寫流程整合 {#integrate-dynamic-media-with-edge-delivery-services}

當[!DNL AEM Assets]與您的檔案式編寫工具（例如[!DNL Microsoft Word]或[!DNL Google Docs]）整合時，它會在您的編寫工具中提供資產選擇器。 使用此資產選擇器來存取[!DNL AEM Assets]，並將核准的資產插入您的內容。
如果您已有[!DNL Edge Delivery Services]網站，請參閱[[!DNL AEM Assets] 外掛程式](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)檔案，以瞭解如何將[!DNL AEM Assets]與您現有的[!DNL AEM]專案整合。
如果您沒有[!DNL Edge Delivery Services]網站，無法發佈使用檔案式編寫工具所編寫的[!DNL AEM Assets]內含式內容，請遵循下列[必要條件](#integrate-aem-assets-with-microsoft-word-and-google-docs)和[整合 [!DNL AEM Assets] 與檔案式編寫環境](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs)區段。

### 先決條件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

在開始之前，請確定您的檔案式製作環境已準備就緒：

* 將[!DNL AEM]與檔案式製作工具整合，以設定製作環境。 請參閱[快速入門 — 開發人員教學課程](https://www.aem.live/developer/tutorial)，瞭解如何設定撰寫環境。

### 將[!DNL AEM Assets]與檔案式製作環境整合{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

設定[!DNL AEM Assets] Sidekick外掛程式以在[!DNL Microsoft Word]或[!DNL Google Docs]中編寫內容時使用資產。

* 請參閱[[!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors)以瞭解如何在Microsoft Word或Google Docs中存取及使用AEM Assets。
* 如需組態詳細資訊，請參閱[設定 [!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin)。
  ![在ms word和google檔案中使用具有openAPI功能的dynamic media](/help/assets/assets/my-assets-sidebar.png)

## 使用[!DNL Dynamic Media with OpenAPI capabilities]傳遞資產 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

您也可以使用使用[!DNL Dynamic Media with OpenAPI capabilities]遞送的資產。 它提供許多優點，例如：

* 僅能從[!DNL AEM Assets Cloud Services]存取品牌核准的資產（影像、影片、PDF和其他資產型別）。
* 治理（參考與資產的副本），有助於自動傳播資產生命週期事件，例如到期、刪除和更新。
* 動態影像轉譯和智慧型裁切。
* 多媒體最佳化和傳送，例如現成可用的最適化視訊串流，以及PDF的原始資產傳送。
* 資產層級曝光報告（[有限可用性](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)）。

如需功能的詳細資訊，請參閱[[!DNL Dynamic Media with OpenAPI capabilities]](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview)檔案。

### 先決條件 {#dynamic-media-with-universal-editor-and-edge-delivery-services}

若要使用資產參考，您必須擁有：

* 已啟用[!DNL Dynamic Media with Open API capabilities]的Assets Cloud Service環境權益。
* [!DNL Dynamic Media]授權。
* [!DNL AEM Assets sidekick plugin]已啟用，並啟用影像資產的複製參考。 如需詳細資訊，請參閱[此檔案以檔案為基礎的編寫](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode)，以及請參閱[此檔案以通用編輯器為基礎的編寫](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)。
* 已核准的Assets。 已核准的資產透過Assets Cloud Services後端或UI動作有`dam:status=Approved`。

### 使用使用[!DNL Dynamic Media with OpenAPI capabilities]傳遞的資產{#Using-Dynamic-Media-with-edge-delivery-services}

選取下列連結，瞭解如何使用[!DNL Dynamic Media with OpenAPI capabilities]傳送您內容中的影像、影片和其他資產型別：

* [新增影像至您的內容](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [新增視訊至您的內容](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [新增非影像和視訊資產，例如PDF、Zip檔案等](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

請觀看此影片，瞭解如何使用具有OpenAPI功能的Dynamic Media在您的內容中傳遞資產。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## 範例[!DNL Edge Delivery Services]網站{#dynamic-media-with-google-docs-and-ms-word}

請參閱[WKND Travel](https://aem-dynamicmedia-demo--dm--hlxsites.aem.live/travel-hospitality/wknd-trvl-home)，這是使用[!DNL Edge Delivery Services]的檔案式撰寫功能建置的網站。 網站內容是在[Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT)中撰寫，而使用[!DNL Dynamic Media with OpenAPI capabilities]傳遞內容中的資產。 完成製作後，內容會直接從檔案發佈。 探索此[Git存放庫](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks)，瞭解用來建立此[!DNL Edge Delivery Services (EDS)]網站檔案式撰寫設定的所有基本檔案、資料夾、設定、網站樣式和功能程式碼。

## 正在整合[!DNL AEM Assets]與[!DNL Edge Delivery Services]的[!DNL Universal Editor]式編寫流程 {#integrate-aem-assets-with-universal-editor-UE}

設定[!DNL Universal Editor]以與[!DNL AEM Assets]整合。 此整合可讓您使用[!DNL Dynamic Media with OpenAPI capabilities]傳遞資產。

* 檢視 [!DNL Edge Delivery] 網站](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)中的[設定，瞭解如何在[!DNL Universal Editor]中新增自訂資產選擇器函式。 自訂資產選擇器可讓您將資產直接插入到[!DNL Universal Editor]內容。
* 請參閱[擴充功能概觀](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)以瞭解如何在[!DNL Universal Editor]中撰寫時存取[!DNL AEM Assets]和插入資產。

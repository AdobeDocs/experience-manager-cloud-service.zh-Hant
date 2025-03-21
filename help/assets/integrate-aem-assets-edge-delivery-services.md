---
title: 為 Edge Delivery Services 製作內容時，將 AEM Assets 進行整合
description: 瞭解如何將AEM Assets與Edge Delivery Services整合。 此整合可讓您將AEM Assets與Microsoft Word和Google Docs整合、將AEM Assets與Universal Editor整合、將Dynamic Media與OpenAPI功能與Universal Editor整合，以及將Dynamic Media與OpenAPI功能與Microsoft Word和Google Docs整合。
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: e4a71d1a513bebed67b9571a483871dc16c36daa
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 3%

---

# 為 Edge Delivery Services 製作內容時，將 AEM Assets 進行整合 {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

使用UE](/help/assets/assets/EDS2.png)的![AEM資產

[Edge Delivery Services](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/overview)是一組可撰寫的服務，可讓您在網站上撰寫及傳遞內容的方式上擁有高度彈性。 您可以使用通用編輯器和檔案式編寫，同時使用[AEM內容管理](/help/sites-cloud/authoring/author-publish.md)和[WYSIWYG編寫](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)。

您可以在下列位置編輯內容：

* [Microsoft Word或Google Docs](#integrate-aem-assets-with-document-based-authoring-tools)
* [通用編輯器](#integrate-aem-assets-with-UE-universal-editor)

編輯內容後，您可以將其發佈到Edge Delivery Services。

## 將AEM Assets與Edge Delivery Services的檔案式製作流程整合 {#integrate-aem-assets-with-document-based-authoring-tools}

當AEM Assets與檔案式製作工具(例如Microsoft Word或Google Docs)整合時，它會在您的編輯器中提供資產選擇器。 使用此資產選擇器來存取AEM Assets，並將核准的資產插入您的檔案。
如果您已有Edge Delivery Services網站，請參閱[AEM Assets外掛程式](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)檔案，瞭解如何將AEM Assets與現有的AEM專案整合。
如果您沒有AEM Assets網站，無法發佈使用檔案式撰寫工具撰寫的AEM Assets內含式內容，請遵循下列[必要條件](#integrate-aem-assets-with-microsoft-word-and-google-docs)和[整合Edge Delivery Services與檔案式撰寫環境](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs)區段。

### 先決條件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

在開始之前，請確定您的檔案式製作環境已準備就緒：

* 將AEM與檔案式製作工具整合，以設定製作環境。 請參閱[快速入門 — 開發人員教學課程](https://www.aem.live/developer/tutorial)，瞭解如何設定撰寫環境。

### 將AEM Assets與檔案式製作環境整合{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

在AEM Assets Word或Google Docs中編寫內容時，請設定Microsoft Sidekick外掛程式以使用資產。

* 請參閱[Adobe Experience Manager Assets Sidekick外掛程式](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors)，瞭解如何在Microsoft Word或Google Docs中存取及使用AEM Assets。
* 如需設定詳細資訊，請參閱[設定Adobe Experience Manager Assets Sidekick外掛程式](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin)。
  ![在ms word和google檔案中使用具有openAPI功能的dynamic media](/help/assets/assets/my-assets-sidebar.png)

## 使用具備OpenAPI功能的Dynamic Media傳遞資產 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

您也可以使用透過DM及OpenAPI功能傳送的資產。 它提供許多優點，例如：

* 從AEM Assets雲端服務僅存取品牌核准的資產（影像、影片、PDF和其他資產型別）。
* 治理（參考與資產的副本），有助於自動傳播資產生命週期事件，例如到期、刪除和更新。
* 動態影像轉譯和智慧型裁切。
* 多媒體最佳化和傳送，例如現成可用的最適化視訊串流，以及PDF的原始資產傳送。
* 資產層級曝光報告（[有限可用性](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)）。

如需功能的詳細資訊，請參閱[具有OpenAPI功能的Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview)檔案。

### 先決條件 {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

若要使用資產參考，您必須擁有：

* 有權使用已啟用開放API功能Dynamic Media的Assets Cloud Service環境。
* Dynamic Media授權。
* 已啟用AEM Assets sidekick外掛程式，並啟用影像資產的複製參考。 如需詳細資訊，請參閱檔案式撰寫的[這個](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode)，以及萬用編輯器式撰寫的[這個](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)。
* 已核准的Assets。 已核准的資產透過Assets Cloud Services後端或UI動作有`dam:status=Approved`。

### 使用具備OpenAPI功能的Dynamic Media所傳送的資產{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

選取下列連結，瞭解如何使用Dynamic Media搭配OpenAPI功能在您的內容中傳遞影像、影片和其他資產型別：

* [新增影像至您的內容](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [新增視訊至您的內容](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [新增非影像和視訊資產，例如PDF、Zip檔案等](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

請觀看此影片，瞭解如何使用具有OpenAPI功能的Dynamic Media在您的內容中傳遞資產。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Edge Delivery Services網站範例{#example-of-an-Edge-Delivery-Services-site}

請參閱[WKND Travel](http://bit.ly/3DExLnf)，此網站是使用Edge Delivery Services的檔案式撰寫功能建置的。 網站內容是在[Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT)中撰寫，而具有OpenAPI功能的Dynamic Media是用來傳遞內容中的資產。 完成製作後，內容會直接從檔案發佈。 探索此[Git存放庫](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks)，瞭解用於建立此Edge Delivery Services (EDS)網站的檔案式撰寫設定的所有基本檔案、資料夾、設定、網站樣式和功能程式碼。

## 將AEM Assets與適用於Edge Delivery Services的Universal Editor式製作流程整合 {#integrate-aem-assets-with-UE-universal-editor}

設定通用編輯器以與AEM Assets整合。 此整合可讓您透過OpenAPI功能使用Dynamic Media來傳送資產。

* 請參閱Edge Delivery網站中的[設定](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)，瞭解如何在Universal Editor中新增自訂資產選擇器功能。 自訂資產選擇器可讓您將資產直接插入至Universal Editor內容。
* 請參閱[擴充功能概觀](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)，瞭解如何在Universal Editor中編寫時存取AEM Assets和插入資產。

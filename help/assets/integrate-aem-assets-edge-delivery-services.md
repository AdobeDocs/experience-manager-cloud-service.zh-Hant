---
title: 為Edge Delivery Services製作內容時整合AEM Assets
description: 瞭解如何將AEM Assets與Edge Delivery Services整合。 此整合可讓您將AEM Assets與Microsoft Word和Google檔案整合、將AEM Assets與Universal Editor整合、將Dynamic Media與OpenAPI功能與Universal Editor整合，以及將Dynamic Media與OpenAPI功能與Microsoft Word和Google檔案整合。 完成這項整合後，您可以在Microsoft Word和Google檔案內使用AEM Assets，在Universal Editor內使用AEM Assets，在Universal Editor內使用Dynamic Media搭配OpenAPI功能來傳送資產，並在Microsoft Word和Google檔案內使用Dynamic Media搭配OpenAPI功能來傳送資產。
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 87acadf3664a180df758ee40e5f5e35c68aef7b8
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# 為Edge Delivery Services製作內容時整合AEM Assets {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![EDS2](/help/assets/assets/EDS2.png)

Edge Delivery Services是一組可撰寫的服務，讓您在網站上製作和傳遞內容的方式上擁有高度彈性。 您可以使用通用編輯器和檔案式編寫，同時使用[AEM內容管理](/help/sites-cloud/authoring/author-publish.md)和[WYSIWYG編寫](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)。

您可以在下列位置編輯內容：

* [Microsoft Word或Google檔案](#integrate-aem-assets-with-document-based-authoring-tools)

* [通用編輯器](#integrate-aem-assets-with-universal-editor)

編輯內容後，您可以將其發佈到Edge Delivery Services。

## 將AEM Assets與Edge Delivery Services的檔案式製作流程整合 {#integrate-aem-assets-with-document-based-authoring-tools}

AEM Assets與檔案型撰寫工具(例如Microsoft Word或Google Docs)的整合功能，可直接在您的編輯器中提供資產選擇器。 使用此資產選擇器來存取AEM Assets，並將核准的資產插入您的檔案。

### 先決條件{#integrate-aem-assets-with-microsoft-word-and-google-docs}

開始之前，請確定您的檔案式製作環境已準備就緒：

* 將AEM與檔案式製作工具整合，以設定製作環境。 請參閱[快速入門 — 開發人員教學課程](https://www.aem.live/developer/tutorial)以設定編寫環境。

### 將AEM Assets與檔案式製作環境整合{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

設定AEM AssetsSidekick外掛程式，以便在Microsoft Word或Google檔案中編寫內容時使用資產。

* 請參閱[Adobe Experience Manager AssetsSidekick外掛程式](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors)，瞭解如何在Microsoft Word或Google檔案中存取及使用AEM Assets。
* 如需設定詳細資訊，請參閱[設定Adobe Experience Manager AssetsSidekick外掛程式](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin)。
  ![my-assets-sidebar](/help/assets/assets/my-assets-sidebar.png)

## 使用具備OpenAPI功能的Dynamic Media交付資產 {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

您也可以使用透過DM及OpenAPI功能傳送的資產。 它提供許多優點，例如：

* 僅從AEM AssetsCloud Service存取品牌核准的資產(影像、影片、PDF和其他資產型別)。
* 治理（參考與資產的副本），有助於自動傳播資產生命週期事件，例如到期、刪除和更新。
* 動態影像轉譯和智慧型裁切。
* 多媒體最佳化和傳送，例如現成可用的最適化視訊串流，以及PDF的原始資產傳送。
* 資產層級曝光報告（[有限可用性](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)）。

如需功能的詳細資訊，請參閱[具有OpenAPI功能的Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview)檔案。

### 先決條件 {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

若要使用資產參考，您必須擁有：

* 有權使用已啟用具開放API功能的Dynamic Media的AssetsCloud Service環境。
* Dynamic Media授權。
* 已啟用AEM Assets sidekick外掛程式，並啟用影像資產的複製參考。 如需詳細資訊，請參閱檔案式撰寫的[這個](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode)，以及萬用編輯器式撰寫的[這個](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)。
* 已核准的Assets。 已核准的Assets透過AssetsCloud Service後端或UI動作具有`dam:status=Approved`。

### 使用具有OpenAPI功能的Dynamic Media所傳送的資產{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

若要在製作內容時使用具有OpenAPI功能的Dynamic Media所傳送的資產，請參閱：

* [使用影像參考](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [使用視訊參考](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [對非影像和視訊資產(例如PDF、Zip檔案等)使用資產參考](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

請觀看此影片，瞭解如何使用Dynamic Media搭配OpenAPI功能傳遞資產。

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## 範例Edge Delivery Services網站{#example-of-an-Edge-Delivery-Services-site}

請參閱[WKND旅遊](https://aem-dynamicmedia-demo--dm--hlxsites.aem.live/travel-hospitality/wknd-trvl-home)。 此網站是使用Edge Delivery Services的檔案型製作功能所建置。 使用Dynamic Media搭配資產傳送的OpenAPI功能，在[Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT)中編寫網站內容。 一旦編寫完成，內容會直接從檔案發佈。 對於此檔案式撰寫設定，所有必要的檔案、資料夾、設定、網站樣式和功能程式碼都儲存在此[Git存放庫](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks)中。

## 將AEM Assets與通用編輯器型Edge Delivery Services製作流程整合 {#integrate-aem-assets-with-universal-editor}

設定通用編輯器以與AEM Assets整合。 此整合可讓您將Dynamic Media與OpenAPI功能搭配使用，以傳送資產。

* 請參閱Edge Delivery網站中的[設定](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)，以在Universal Editor中新增自訂資產選擇器函式。 自訂資產選擇器可讓您將資產直接插入至Universal Editor內容。
* 請參閱[擴充功能概觀](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)，瞭解如何在Universal Editor中編寫時存取AEM Assets和插入資產。

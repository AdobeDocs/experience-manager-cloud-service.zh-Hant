---
title: 在 [!DNL AEM Assets View]中啟用UI擴充性
description: 瞭解 [!DNL AEM Assets View]. [!DNL AEM Assets View] UI的UI擴充功能可讓您新增自訂UI元件，以符合特定的業務需求。
feature: App Builder
role: User, Developer
exl-id: a11f7043-17cf-4331-b76c-d3db099c2411
source-git-commit: a03e6cf842f95f8799f23ed5c7e3b563b092b4e5
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 6%

---

# 在[!DNL AEM Assets View]中啟用UI擴充性 {#AEM-Assets-View-UI-Extensibility}

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

[!DNL AEM Assets View]支援UI擴充功能，可讓您針對[!DNL AEM Assets View]現成功能未滿足的特定工作流程和業務需求，將自訂UI元件新增至[!DNL Assets View] UI。 此[!DNL AEM Assets View]的UI擴充功能可增強其彈性，讓組織能夠針對特定工作流程和需求調整介面。\
您可以將擴充功能新增至&#x200B;**資產**、**資料夾**&#x200B;和&#x200B;**集合**&#x200B;層級。 新增的擴充功能會顯示在&#x200B;**資產**、**集合**&#x200B;或&#x200B;**資料夾** **[!UICONTROL 詳細資料]**&#x200B;頁面的專用面板上。

>[!IMPORTANT]
>
> * [!DNL AEM Assets View] UI擴充性可用於[[!DNL Assets Ultimate]](/help/assets/assets-ultimate-overview.md)。
> * 若要存取[!DNL Assets view] UI擴充功能，[請建立並提交 [!DNL Adobe] 客戶支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
> * 您可以展開&#x200B;**[!UICONTROL 詳細的意見回饋選項]**&#x200B;並按一下&#x200B;**[!UICONTROL 報告問題]**，以提供檔案意見回饋。

## <a id="1"></a>存取Assets檢視{#add-UI-Extensibility-in-AEM-Assets-View}

請依照下圖中所述的步驟來存取[!DNL Assets View]：
![access-assets-view-ui](/help/assets/assets/access-assets-view.jpg)

## 在[!DNL Assets View]中檢視UI延伸模組 {#ui-extensibility-panel-assets-view}

在[!DNL Assets View]內，導覽至資產、資料夾或集合的&#x200B;**[!UICONTROL 詳細資料]**&#x200B;頁面。 **[!UICONTROL 詳細資料]**頁面會在專用面板上顯示新增的UI擴充功能。
![我的工作區](/help/assets/assets/my-workspace-assets-view3.png)

## 新增擴充性元件的先決條件{#assets-view-ui-extensibility}

滿足下列要求，開始在您的[!DNL Assets View UI]上新增擴充性元件：

* [存取 [!DNL Assets View]](#1)。
* 存取[[!DNL Adobe app builder]](https://developer.adobe.com/app-builder/docs/overview/)。
* 組織內系統管理員角色的開發人員權益。 如需詳細資訊，請參閱[此檔案](https://developer.adobe.com/uix/docs/guides/get-access/)。
* [!DNL Adobe IO command line tool (AIO CLI)]已安裝在您的本機電腦上。 此工具對於建立和部署擴充功能專案至關重要。 如需詳細資訊，請參閱[建立您的第一個App Builder應用程式](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app#local-environment-set-up) （存取需要驗證）。
* 充分瞭解[!DNL JavaScript]、[!DNL Node.js]和[!DNL React]技術。

## 將UI擴充性元件新增至[!DNL Assets View] {#ui-extensibility-in-assets-view}

1. 如需UI擴充功能和[!DNL Adobe App Builder]架構的基本資訊，請參閱[快速入門](https://developer.adobe.com/uix/docs/getting-started/)。 瞭解UI擴充功能如何在[!DNL Adobe Experience Cloud services]中整合自訂邏輯和UI，並瞭解實作UI擴充功能的架構和工作流程。
1. 如需UI擴充性的一般資訊，請參閱[指南](https://developer.adobe.com/uix/docs/guides/)，包括本機環境設定、本機預覽、發佈和管理。
1. 請參閱[建立擴充功能的常見概念](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/)，瞭解為[!DNL AEM Assets View]開發UI擴充功能所需的基礎知識。
1. 將自訂側面板新增至[!DNL Assets View]介面。 主機應用程式([!DNL Assets View])管理這些面板，以處理UI互動，例如切換和深層連結。 擴充功能使用`aem/assets/details/1`擴充功能點來整合指定屬性的自訂面板，例如面板ID、標題及內容URL。 開發人員使用`getPanels()`方法註冊自訂面板，並建立顯示自訂內容的路由。 如需詳細實作，包括API參考和程式碼範例，請參閱[詳細資料檢視](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/details-view/)。
1. 設定您的本機環境並建立您的第一個UI擴充功能，以親身體驗在[!DNL Assets View]中開發UI擴充功能的程式。 如需詳細資訊，請參閱[逐步的AEM Assets檢視擴充功能開發](https://developer.adobe.com/uix/docs/services/aem-assets-view/extension-development/)。
1. 使用AIO CLI設定您的應用程式，以產生基本擴充功能結構和必要的程式碼。 如需詳細資訊，請參閱 [!DNL AEM Assets View]](https://developer.adobe.com/uix/docs/services/aem-assets-view/code-generation/)的[程式碼產生。
1. 在本機測試您的擴充功能，確保它們在部署前可如預期般運作。 在完全隔離的環境中執行您的擴充功能或執行部分隔離的擴充功能，並將您的擴充功能連線到生產[!DNL AEM Assets View]以進行測試。 如需詳細資訊，請參閱[疑難排解 —  [!DNL AEM Assets View] 擴充性](https://developer.adobe.com/uix/docs/services/aem-assets-view/debug/)。

## 在Assets檢視中自訂快速動作和動作列 {#customize-quick-actions-and-actions-bar}

您可以在Assets檢視中自訂選取一或多個資產（動作列）時顯示的動作。 Assets檢視也可讓您自訂按一下資產卡片中的更多選項(...)時顯示的動作。 如需詳細資訊，請參閱[瀏覽檢視](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/browse-view/)。

## 在Assets檢視中開啟自訂對話方塊 {#open-custom-dialogs-assets-view}

Assets檢視還能讓您使用選取的文字開啟自訂對話方塊。 您也可以新增連結至文字。 如需詳細資訊，請參閱[模型API](https://developer.adobe.com/uix/docs/services/aem-assets-view/api/commons/#modal-api)。

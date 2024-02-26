---
title: 管理您的示範網站
description: 了解可協助您管理示範網站的工具以及如何移除它們。
exl-id: 988c6e09-c43e-415f-8d61-998c294c5a11
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 100%

---

# 管理您的示範網站 {#manage-demo-sites}

了解可協助您管理示範網站的工具以及如何移除它們。

## 目前進度 {#story-so-far}

在 AEM 參考示範附加元件歷程的上一個文件「[建立網站](create-site.md)」中，您根據參考示範附加元件的範本建立了一個新的示範網站。您現在應該：

* 了解如何存取 AEM 製作環境。
* 了解如何根據範本建立網站。
* 了解導覽網站結構和編輯頁面的基礎知識。

如果您亦[為您的示範網站啟用 AEM Screens](screens.md)，您也應該：

* 了解 AEM Screens 的基礎知識。
* 了解 We.Cafe 示範內容。
* 了解如何針對 We.Cafe 設定 AEM Screens。

現在您已經有自己的示範網站可供探索，本文章說明可幫助您管理示範網站的工具以及如何刪除這些工具。

## 目標 {#objective}

本文件協助您了解如何管理您建立的示範網站。閱讀本文件後，您應該：

* 了解如何存取自助服務示範公用程式。
* 了解您可以使用哪些公用程式。
* 如何刪除現有的示範網站或範本。

## 存取自助服務示範公用程式 {#accessing-utilities}

現在您已經擁有自己的示範網站，您可能想知道如何管理它們。該管道不僅部署網站範本為您的示範網站提供內容，亦部署了一組公用程式來管理這些網站。

1. 從 AEM 全域導覽列中，選取「**工具**」>「**參考示範**」>「**參考示範公用程式**」。

   ![自助服務示範公用程式](assets/demo-utilities.png)

1. 參考示範實用程式是實用功能的集合，可協助設定和監控您的 Adobe Experience Manager 環境。初始視圖是「**儀表板**」，可用來檢查環境及其示範功能的狀態。

   ![儀表板](assets/dashboard.png)

自助服務示範公用程式提供多種工具。

* **刪除網站** - 選擇在此 Adobe Experience Manager 執行個體中您要刪除的網站。請記住，這是一種破壞性動作，一旦啟動就無法復原。
* **刪除網站範本** - 選擇在此 Adobe Experience Manager 執行個體中您要刪除的網站範本。在刪除網站範本之前，請確保同時刪除參考該範本的所有網站。請記住，這是一種破壞性動作，一旦啟動就無法復原。
* **主要作者快取** - 這將取得 Adobe Experience Manager 執行個體中的多個資源，從而加快其取得時間。可能需要幾秒鐘。
* **Android 應用程式** - 用於安裝 Android 應用程式及啟動其示範的工具。根據 **WKND 單頁應用程式**&#x200B;建立一個網站來填入此頁面。從 Android 裝置、模擬器或 Bluestacks 使用。
* **使用者偏好設定** - 關閉教學課程彈快顯對話框。
* **設定 GraphQL** - 快速設定全域 GraphQL 端點。

## 刪除示範網站和範本 {#deleting}

測試一組 AEM 功能後，您可能不再需要示範網站甚至是作為網站基礎的範本。刪除示範網站和示範範本都是簡單的動作。

1. 存取&#x200B;**參考示範公用程式**&#x200B;並選取「**刪除網站**」。

   ![刪除網站](assets/delete-sites.png)

1. 可用的網站以清單形式列出。勾選您要刪除的一個或多個網站，然後選取「**刪除**」。

   >[!CAUTION]
   >
   >刪除網站和範本是一種破壞性動作，一旦啟動就無法復原。

1. 在對話框中確認刪除網站。

   ![確認刪除網站](assets/confirm-site-delete.png)

1. AEM 刪除選定的一個或多個網站並在「**刪除**」按鈕之前的位置顯示進度。

   ![刪除進度](assets/delete-progress.png)

該網站現已刪除。

您可以在「**刪除網站範本**」標題之下用相同的方式刪除範本 (位在&#x200B;**參考示範公用程式**)。

>[!CAUTION]
>
>在刪除網站範本之前，請確保同時刪除參考該範本的所有網站。

## 歷程結尾？ {#end-of-journey}

恭喜！您已完成 AEM 參考示範附加元件的歷程！您現在應該：

* 對 Cloud Manager 有基本了解，並了解管道如何向 AEM 傳遞內容和設定。
* 了解如何使用 Cloud Manager 建立方案。
* 了解如何啟動新方案的參考示範附加元件，並能夠執行管道來部署附加內容。
* 了解如何存取 AEM 製作環境並根據範本來建立網站。
* 了解如何存取自助服務示範公用程式。
* 知道如何刪除現有的示範網站或範本。

現在您已準備好使用自己的示範網站探索 AEM 的功能。但是，AEM 是一個強大的工具，還有許多其他選項可用。查看[其他資源章節](#additional-resources)提供的一些其他資源，以詳細了解您在此歷程中看到的功能。

## 其他資源 {#additional-resources}

* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想直接查閱深入的技術文件。
* [建立網站](/help/sites-cloud/administering/site-creation/create-site.md) - 了解如何在 AEM 中利用網站範本來定義網站的樣式與結構以便建立網站。
* [AEM 的頁面命名慣例](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices)- 請參閱此頁面以了解組織 AEM 頁面的慣例。
* [AEM 基本處理](/help/sites-cloud/authoring/basic-handling.md) - 如果您初次使用 AEM，請探索此文件以了解導覽和主控台組織等基本概念。
* [AEM as a Cloud Service 技術文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - 如果您已經對 AEM 有深入的了解，您可能想直接查閱深入的技術文件。
* [網站範本](/help/sites-cloud/administering/site-creation/site-templates.md) - 如果您想了解有關網站範本的結構以及如何使用它們建立網站的更多資訊，請參閱本文件。

---
title: 管理您的示範網站
description: 了解可協助您管理示範網站的工具以及如何移除它們。
exl-id: 988c6e09-c43e-415f-8d61-998c294c5a11
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 17%

---

# 管理您的示範網站 {#manage-demo-sites}

了解可協助您管理示範網站的工具以及如何移除它們。

## 到目前為止 {#story-so-far}

在AEM參考示範附加元件歷程的上一個檔案中， [建立網站，](create-site.md) 您已根據參考示範附加元件的範本建立新的示範網站。 您現在應該：

* 瞭解如何存取AEM製作環境。
* 瞭解如何根據範本建立網站。
* 瞭解導覽網站結構和編輯頁面的基本概念。

如果您還 [為您的示範網站啟用AEM Screens，](screens.md) 您也應：

* 瞭解AEM Screens的基本概念。
* 瞭解We.Cafe示範內容。
* 瞭解如何為We.Cafe設定AEM Screens。

現在您已擁有自己的示範網站可探索，本文介紹可用來協助您管理示範網站的工具，以及如何移除它們。

## 目標 {#objective}

本檔案可協助您瞭解如何管理您建立的示範網站。 閱讀本文件後，您應該：

* 瞭解如何存取自助示範公用程式。
* 瞭解您可以使用哪些公用程式。
* 如何刪除現有的示範網站或範本。

## 存取自助示範公用程式 {#accessing-utilities}

現在您已擁有自己的示範網站，您可能想知道如何管理這些網站。 此管道不僅部署了網站範本以提供您的示範網站內容，還部署了一組公用程式來管理這些網站。

1. 從AEM全域導覽列中，選取 **工具** > **參考示範** > **參考示範公用程式**.

   ![自助示範公用程式](assets/demo-utilities.png)

1. 參考示範公用程式是實用功能的集合，可協助設定和監控您的Adobe Experience Manager環境。 初始檢視是 **儀表板**，可作為環境及其示範功能的狀態檢查。

   ![控制面板](assets/dashboard.png)

自助示範公用程式提供數種工具。

* **刪除網站**  — 在此Adobe Experience Manager執行個體中選取您要刪除的網站。 請記住，這是破壞性動作，一經啟動便無法復原。
* **刪除網站範本**  — 在此Adobe Experience Manager執行個體中選取您要刪除的網站範本。 在刪除網站範本之前，請確定所有參照該範本的網站也會被刪除。 請記住，這是破壞性動作，一經啟動便無法復原。
* **主要作者快取**  — 這將會在Adobe Experience Manager執行個體中擷取多個資源，從而加快其擷取時間。 這可能需要幾秒鐘的時間。
* **Android應用程式**  — 安裝和啟動示範Android應用程式的工具。 建立網站依據 **WKND單頁應用程式** 以填入此頁面。 從Android裝置、模擬器或Bluestacks使用。
* **使用者偏好設定**  — 關閉教學課程快顯對話方塊。
* **設定GraphQL**  — 快速設定全域GraphQL端點。

## 刪除示範網站和範本 {#deleting}

測試一組AEM功能後，您可能不再需要示範網站，甚至不再需要示範網站所依據的範本。 您可輕鬆刪除示範網站和網站範本。

1. 存取 **參考示範公用程式** 並選取 **刪除網站**.

   ![刪除網站](assets/delete-sites.png)

1. 可用的網站會以清單顯示。 檢查您要刪除的網站，然後選取 **刪除**.

   >[!CAUTION]
   >
   >網站和範本刪除是破壞性動作，一經啟動便無法還原。

1. 在對話方塊中確認網站刪除。

   ![確認網站刪除](assets/confirm-site-delete.png)

1. AEM會刪除所選的一個或多個網站，並在下列位置顯示進度： **刪除** 按鈕之前為。

   ![刪除進度](assets/delete-progress.png)

網站現已刪除。

您可以使用相同方式在標題下方刪除範本 **刪除網站範本** 在 **參考示範公用程式**.

>[!CAUTION]
>
>在刪除網站範本之前，請確定所有參照該範本的網站也會被刪除。

## 歷程結尾？ {#end-of-journey}

恭喜！您已完成AEM參考示範附加元件歷程！ 您現在應該：

* 基本瞭解Cloud Manager，並瞭解管道如何將內容和設定傳送到AEM。
* 瞭解如何使用Cloud Manager建立計畫。
* 瞭解如何為新程式啟動參考示範附加元件，並能夠執行管道以部署附加元件內容。
* 瞭解如何存取AEM製作環境，以根據範本建立網站。
* 瞭解如何存取自助示範公用程式。
* 瞭解如何刪除現有的示範網站或範本。

您現在已準備好使用自己的示範網站來探索AEM的功能。 但是，AEM 是一個強大的工具，還有許多其他選項可用。查看[其他資源章節](#additional-resources)提供的一些其他資源，以詳細了解您在此歷程中看到的功能。

## 其他資源 {#additional-resources}

* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想要直接查閱深入的技術文件。
* [建立網站](/help/sites-cloud/administering/site-creation/create-site.md)  — 瞭解如何使用AEM建立網站，使用網站範本定義網站的樣式和結構。
* [AEM頁面命名慣例](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices).  — 請參閱本頁面以瞭解組織AEM頁面的慣例。
* [AEM基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 如果您不熟悉AEM，請參閱本檔案，瞭解導覽與主控台組織等基本概念。
* [AEM as a Cloud Service 技術文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - 如果您已經對 AEM 有深入的了解，您可能想要直接查閱深入的技術文件。
* [網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)  — 如果您想深入瞭解網站範本的結構，以及如何使用範本建立網站，請參閱本檔案。

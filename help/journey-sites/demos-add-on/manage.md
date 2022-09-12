---
title: 管理您的示範網站
description: 了解可協助您管理示範網站的工具，以及如何移除示範網站。
exl-id: 988c6e09-c43e-415f-8d61-998c294c5a11
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 管理您的示範網站 {#manage-demo-sites}

了解可協助您管理示範網站的工具，以及如何移除示範網站。

## 迄今為止的故事 {#story-so-far}

在AEM參考示範附加元件歷程的上一份檔案中， [建立網站，](create-site.md) 您根據「參考演示附加元件」的模板建立了新的演示站點。 您現在應該：

* 了解如何存取AEM製作環境。
* 了解如何根據範本建立網站。
* 了解導覽網站結構和編輯頁面的基本知識。

如果您也 [啟用AEM Screens,](screens.md) 您也應：

* 了解AEM Screens的基本知識。
* 了解We.Cafe示範內容。
* 了解如何為We.Cafe設定AEM Screens。

現在您有自己的示範網站可供探索，本文說明可協助您管理示範網站的工具，以及如何移除示範網站。

## 目標 {#objective}

本檔案可協助您了解如何管理您建立的示範網站。 閱讀後，您應：

* 了解如何存取自助服務示範公用程式。
* 了解您有哪些實用程式可用。
* 如何刪除現有的示範網站或範本。

## 訪問自助服務演示實用程式 {#accessing-utilities}

現在您擁有自己的示範網站，因此您可能想要了解如何管理示範網站。 管道不僅部署了網站範本以提供示範網站的內容，還部署了一組公用程式來管理這些網站。

1. 在AEM全域導覽列中，選取 **工具** -> **參考示範** -> **參考示範公用程式**.

   ![自助服務演示實用程式](assets/demo-utilities.png)

1. 參考示範公用程式是實用功能的集合，可協助您設定及監控Adobe Experience Manager環境。 初始檢視是 **控制面板**，可作為環境及其示範功能的狀態檢查。

   ![控制面板](assets/dashboard.png)

自助服務演示實用程式提供了多種工具。

* **刪除網站**  — 在此Adobe Experience Manager例項中選取您要刪除的網站。 請記住，這是破壞性動作，一旦啟動即無法復原。
* **刪除網站範本**  — 在此Adobe Experience Manager例項中選取您要刪除的網站範本。 刪除網站範本之前，請確定參照該範本的所有網站也被刪除。 請記住，這是破壞性動作，一旦啟動即無法復原。
* **主要作者快取**  — 這會在Adobe Experience Manager例項內擷取數個資源，加快擷取時間。 可能需要幾秒。
* **Android應用程式**  — 安裝和啟動示範Android應用程式的工具。 根據 **WKND單頁應用程式** 填入此頁面。 從Android裝置、模擬器或藍點使用。
* **使用者偏好設定**  — 關閉教學課程快顯對話方塊。
* **設定GraphQL**  — 快速設定全局GraphQL終結點。

## 刪除示範網站和範本 {#deleting}

在測試了一組AEM功能後，您可能不再需要示範網站，甚至不再需要示範網站所依據的範本。 您可輕鬆刪除示範網站和網站範本。

1. 存取 **參考示範公用程式** 點選或按一下 **刪除網站**.

   ![刪除網站](assets/delete-sites.png)

1. 可用的網站會列在清單中。 檢查您要刪除的網站，然後點選或按一下 **刪除**.

   >[!CAUTION]
   >
   >網站和範本刪除是破壞性動作，一經啟動即無法復原。

1. 在對話方塊中確認網站刪除。

   ![確認網站刪除](assets/confirm-site-delete.png)

1. AEM會刪除選取的網站，並顯示其進度，其中 **刪除** 按鈕。

   ![刪除進度](assets/delete-progress.png)

網站現在已刪除。

您可以以相同方式刪除標題下的範本 **刪除網站範本** 在 **參考示範公用程式**.

>[!CAUTION]
>
>刪除網站範本之前，請確定參照該範本的所有網站也被刪除。

## 旅程的結束？ {#end-of-journey}

恭喜！ 您已完成AEM參考示範附加程式歷程！ 您現在應該：

* 了解Cloud Manager的基本知識，並了解管道如何將內容和設定傳送至AEM。
* 了解如何使用Cloud Manager建立新方案。
* 了解如何為新程式激活參考演示附加元件，並能夠運行管道來部署附加元件內容。
* 了解如何存取AEM製作環境，以根據範本建立網站。
* 了解如何存取自助服務示範公用程式。
* 了解如何刪除現有的示範網站或範本。

您現在可以使用自己的示範網站來探索AEM的功能。 不過，AEM是功能強大的工具，有許多其他選項可供使用。 查看 [「其他資源」部分](#additional-resources) 以進一步了解您在此歷程中看到的功能。

## 其他資源 {#additional-resources}

* [Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您想要取得Cloud Manager功能的詳細資訊，可直接參閱深入的技術檔案。
* [建立網站](/help/sites-cloud/administering/site-creation/create-site.md)  — 了解如何使用AEM使用網站範本來定義網站的樣式和結構來建立網站。
* [AEM頁面命名慣例。](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices)  — 請參閱本頁面，了解組織AEM頁面的慣例。
* [AEM基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 如果您是剛接觸AEM的人，熟悉導覽與主控台組織等基本概念，請探索本檔案。
* [AEMas a Cloud Service技術檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)  — 如果您已對AEM有明確的了解，建議您直接參閱深入的技術檔案。
* [網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)  — 如果您想進一步了解網站範本的結構，以及如何使用範本建立網站，請參閱本檔案。

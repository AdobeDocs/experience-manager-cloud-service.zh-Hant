---
title: 管理分階段產品目錄體驗
description: 了解如何管理分階段產品目錄體驗。
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# 建立分階段產品目錄體驗 {#building-experiences}

了解如何管理分階段產品目錄體驗。

## 迄今為止的故事 {#story-so-far}

在AEM內容與商務歷程的上一份檔案中， [管理產品目錄頁面和範本](catalog-templates.md)，您已學習如何根據範本管理和建立產品目錄體驗。

本文以這些基本知識為基礎。

## 目標 {#objective}

本檔案可協助您了解如何根據分階段產品資料和AEM Launches管理產品目錄體驗。 許多時候，作者必須同時準備即將推出的產品發佈（例如新的服裝系列）。 這需要存取分階段產品資料（尚未上線），以及準備內容的能力。 此新內容將隨產品推出而上線。

    >[!NOTE]
    >
    >此功能僅適用於支援代號式驗證的Adobe Commerce或雲端版及第三方連接器。 如需詳細資訊，請參閱[快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html)。

首先，讓我們了解作者如何透過CIF存取各階段產品資料。

## 使用分階段產品資料 {#staged-product-data}

使用產品座艙是存取分階段產品資料的一種方式。 按一下主AEM功能表中的商務圖示，開啟產品目錄。 這可讓您存取即時產品資料。 開啟左側的篩選標籤，然後展開 **分段目錄**. 使用預覽資料，您現在可以存取任何時間點的分階段產品資料。 分段資料包括新類別、產品或價格等更新欄位。

![舞台座艙](assets/staged-cockpit.png)

使用時間扭曲檢視，可以使用暫時資料預覽店面。 開啟編輯器，並將模式切換為時間扭曲。 選擇任何未來日期。 請注意您在特定日期檢視頁面之編輯器頂端的資訊。

![階段時間扭曲](assets/staged-timewarp.png)

您現在可以使用暫存資料來瀏覽目錄。 如果您開啟階段類別或產品頁面，編輯器會顯示視覺指標。

![階段pl](assets/staged-plp.png)

    >[!NOTE]
    >
    >Omnisearch沒有內容，因此只會傳回即時產品目錄資料

## AEM啟動 {#launches}

AEM Launches可讓您建立分階段產品資料的內容。 如果您不熟悉啟動，請遵循 [「其他資源」部分](#additional-resources). 然後會使用「啟動日期」來存取分階段產品資料。

![階段啟動](assets/staged-launch.png)

請注意，選擇者會遵守啟動日期，並在右側顯示階段指標。

![階段選取器](assets/staged-picker.png)

## 下一步 {#what-is-next}

現在您已完成此部分的歷程，您應：

* 了解Launch提供的分階段產品目錄和內容概念
* 可透過產品座艙和編輯器存取各階段產品目錄資料

您現在已準備好管理 [產品體驗](product-experience-management.md). 不過，AEM內容與商務有許多其他選項可供使用。 查看 [「其他資源」部分](#additional-resources) 以進一步了解您在此歷程中看到的功能。

## 其他資源 {#additional-resources}

* [產品座艙](/help/commerce-cloud/authoring/product-cockpit.md)
* [快速入門](/help/commerce-cloud/getting-started.md)
* [啟動](/help/sites-cloud/authoring/launches/overview.md)

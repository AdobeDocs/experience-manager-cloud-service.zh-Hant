---
title: 管理預備產品目錄體驗
description: 瞭解如何管理分階段的產品目錄體驗。
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 10%

---

# 建立分階段產品目錄體驗 {#building-experiences}

瞭解如何管理分階段的產品目錄體驗。

## 目前進度 {#story-so-far}

在AEM內容和Commerce歷程的上一個檔案[管理產品目錄頁面和範本](catalog-templates.md)中，您已瞭解如何根據範本管理和建置產品目錄體驗。

本文基於這些基礎之上。

## 目標 {#objective}

本檔案可協助您瞭解如何根據分階段產品資料和AEM啟動來管理產品目錄體驗。 許多時候，作者必須同時準備即將推出的產品（例如新的服裝系列）。 需要存取分階段產品資料（尚未上線）和準備內容的能力。 此新內容將在產品上市時上線。

>[!NOTE]
>
>此功能僅適用於Adobe Commerce或Cloud Edition，以及支援權杖式驗證的協力廠商聯結器。 如需詳細資訊，請參閱[快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html)。

首先，讓我們瞭解作者如何使用CIF存取分階段產品資料。

## 使用分階段產品資料 {#staged-product-data}

存取分階段產品資料的一種方式是使用產品駕駛艙。 按一下AEM主功能表中的Commerce圖示，開啟產品目錄。 這可讓您存取即時產品資料。 開啟左側的篩選標籤，並展開&#x200B;**階段目錄**。 您現在可以使用預覽資料存取任何時間點的階段產品資料。 階段資料包含新類別、產品或價格等更新欄位。

![中繼駕駛艙](assets/staged-cockpit.png)

您可以使用時間扭曲檢視，以階段資料預覽店面。 開啟編輯器並將模式切換為timewarp。 選取任何未來的日期。 請注意編輯器上方的資訊，表示您正在檢視特定日期的頁面。

![階段時間扭曲](assets/staged-timewarp.png)

您現在可以瀏覽包含階段資料的目錄。 如果您開啟分階段類別或產品頁面，編輯器將顯示視覺指示器。

![階段plp](assets/staged-plp.png)

>[!NOTE]
>
>Omnisearch沒有內容，因此只會傳回即時產品目錄資料

## AEM 啟動 {#launches}

AEM啟動可讓您建立分階段產品資料的內容。 如果您不熟悉Launches，請依照[其他資源區段](#additional-resources)下的檔案連結操作。 然後會使用「啟動日期」來存取分階段的產品資料。

![階段啟動](assets/staged-launch.png)

請注意，選擇器會在啟動日期右側使用分階段指示器。

![階段選擇器](assets/staged-picker.png)

## 後續步驟 {#what-is-next}

現在您已完成歷程的這一部分，您應該：

* 透過Launch瞭解分階段產品目錄和內容的概念
* 能夠透過產品駕駛艙和編輯器存取分階段產品目錄資料

您現在已準備好管理[產品體驗](product-experience-management.md)。 不過，AEM內容和Commerce有許多其他可用選項。 查看[其他資源區段](#additional-resources)提供的一些其他資源，以詳細了解您在此歷程中看到的功能。

## 其他資源 {#additional-resources}

* [產品駕駛艙](/help/commerce-cloud/authoring/product-cockpit.md)
* [快速入門](/help/commerce-cloud/getting-started.md)
* [啟動](/help/sites-cloud/authoring/launches/overview.md)

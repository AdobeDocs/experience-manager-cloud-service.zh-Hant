---
title: 管理分階段產品目錄體驗
description: 瞭解如何管理分階段的產品目錄體驗。
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# 構建分階段產品目錄體驗 {#building-experiences}

瞭解如何管理分階段的產品目錄體驗。

## 到目前為止的故事 {#story-so-far}

在上一篇內容和AEM商務旅程中， [管理產品目錄頁和模板](catalog-templates.md)，您學習了如何基於模板管理和構建產品目錄體驗。

本文基於這些基本原理。

## 目標 {#objective}

本文檔幫助您瞭解如何根據已轉移的產品資料和啟動管理產品目AEM錄體驗。 很多時候，作者必須同時準備即將推出的產品（例如新服裝系列）。 這需要訪問分階段產品資料（尚未生存）和準備內容的能力。 此新內容將隨產品發佈而直播。

    >[！注釋]
    >
    >此功能僅適用於支援基於令牌的身份驗證的Adobe Commerce或雲版和第三方連接器。 有關其他資訊，請參閱[入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html)。

首先，讓我們看看作者如何使用CIF訪問分階段產品資料。

## 使用分段產品資料 {#staged-product-data}

訪問分階段產品資料的一種方法是使用產品駕駛艙。 按一下主菜單中的「商業」表徵圖開啟產品目AEM錄。 這將允許您訪問即時產品資料。 開啟左側的篩選器頁籤並展開 **暫存目錄**。 使用預覽資料，您現在可以訪問任何時間點的已提貨產品資料。 分段資料包括新類別、產品或更新的欄位（如價格）。

![座艙](assets/staged-cockpit.png)

使用時間曲線視圖可以使用暫存資料預覽儲存庫。 開啟編輯器並將模式切換為時間曲線。 選擇任何將來日期。 請注意編輯器頂部的資訊，您正在查看某一日期的頁面。

![階段時間曲線](assets/staged-timewarp.png)

現在，您可以使用暫存資料瀏覽目錄。 如果開啟已轉移的類別或產品頁面，編輯器將顯示可視指示器。

![階段pl](assets/staged-plp.png)

    >[！注釋]
    >
    >Omnisearch沒有上下文，因此將只返回即時產品目錄資料

## 啟AEM動 {#launches}

啟AEM動使您能夠為已轉移的產品資料建立內容。 如果您不熟悉啟動，請按照 [「其他資源」部分](#additional-resources)。 然後使用「啟動日期」(Launch Date)訪問已提貨的產品資料。

![階段發射](assets/staged-launch.png)

請注意，選擇者在右側使用已提貨指示符來尊重啟動日期。

![舞台選取器](assets/staged-picker.png)

## 下一步是什麼 {#what-is-next}

現在，您已完成了此部分的旅程，您應：

* 瞭解產品發佈時分階段產品目錄和內容的概念
* 能夠通過產品駕駛艙和編輯器訪問分階段的產品目錄資料

您現在已準備好管理 [產品體驗](product-experience-management.md)。 但是，AEM Content and Commerce有許多其他選項。 簽出中的某些可用額外資源 [「其他資源」部分](#additional-resources) 瞭解您在此過程中看到的功能。

## 其他資源 {#additional-resources}

* [產品座艙](/help/commerce-cloud/authoring/product-cockpit.md)
* [快速入門](/help/commerce-cloud/getting-started.md)
* [啟動](/help/sites-cloud/authoring/launches/overview.md)

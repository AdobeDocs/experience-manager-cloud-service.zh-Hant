---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.6.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.6.0 版發行說明。'
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 20%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2022.6.0 版發行說明 {#release-notes}

以下章節概述2022.6.0版的功能發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2022.6.0)為2022年6月30日。

下一個版本(2022.7.0)計畫於2022年8月8日發行。

## 發行影片 {#release-video}

請觀看2022年6月版本概觀影片，瞭解2022.6.0版本新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新功能 {#sites-features}

* 新 [使用者介面](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 內容管理員和內容作者現在可以有效地管理（執行發佈、取消發佈、複製、移動等動作）、搜尋/篩選，以及為Headless使用案例建立內容片段。

  ![內容片段主控台](/help/release-notes/assets/cf-ui.png)

* 新 [目錄元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) 不僅適用於核心元件，也適用於所有元件，可自動在內容頁面上呈現ToC。 而且，由於它是在伺服器端轉譯並由Dispatcher完全快取，因此載入也相當有效率。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

Experience Manager Assets現在使用Adobe Sensei AI功能 [區分影像中的顏色，並在擷取時自動將這些顏色套用為標籤](/help/assets/color-tag-images.md). 這些標籤會根據影像顏色組合來增強搜尋體驗。 您可以設定標籤到影像的顏色數量（範圍在1到40之間），以便日後可以根據這些顏色搜尋影像。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新功能 {#forms-features}

* **[整合Adaptive Forms與Microsoft® Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)**：您現在可以設定最適化表單，在提交時執行Microsoft® Power Automate Cloud Flow。 設定的最適化表單會將擷取的資料、附件和記錄檔案傳送到Power Automate Cloud Flow進行處理。 它可幫助您建立自訂資料擷取體驗，同時利用Microsoft® Power Automate的強大功能，圍繞擷取的資料建立商業邏輯，並自動化客戶工作流程。

* **建立最適化表單的精靈**：您可以使用業務使用者友善的精靈來快速撰寫最適化Forms。 精靈提供快速索引標籤導覽，以輕鬆選取預先設定的範本、樣式、欄位和提交選項來建立調適型表單。

  ![建立最適化表單的精靈](/help/release-notes/assets/wizard.png)

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新產品駕駛艙屬性頁面，提供更好、更簡化的概觀

![產品駕駛艙屬性概觀](/help/assets/CIF/product_cockpit_properties_overview.png)

* 改善協力廠商聯結器在I/O執行階段的相容性和健全性

* 改善對GQL使用者端設定覆寫的支援（例如，設定自訂快取行為）

* 現成支援多個商務端點，並可透過Cloud Manager設定。 詳情請見CIF部落格 [此處](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### 錯誤修正 {#bug-fixes-cif}

* 多值產品選擇器欄位會將第2個和其他產品顯示為無效

* 產品選取器偶爾會隱藏在元件後面

## 參考示範附加元件 {#cloud-services-demos}

### 新增功能 {#what-is-new-demos}

* 全新WKND內容與商務範本，可擴充WKND的E2E購物體驗，包含產品目錄、購物車、結帳和myAccount。 此範本使用CIF及其CIF核心元件，因此您也需要安裝CIF附加元件。 詳情請見CIF部落格 [此處](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![WKND商店](/help/assets/CIF/wknd_shop.png)

![WKND pdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 如5月(2022.5.0)發行說明中所述，復寫代理程式管理畫面下的「新增樹狀結構」選項 **散佈** 索引標籤已移除。 應改用復寫具有樹狀階層內容的套件 [管理發布](/help/operations/replication.md#manage-publication) 或 [發佈內容樹狀結構](/help/operations/replication.md#manage-publication#publish-content-tree-workflow) 工作流程。

## Cloud Manager {#cloud-manager}

您可以在[此處](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

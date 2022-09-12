---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.6.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.6.0 版發行說明。'
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
source-git-commit: 472b670623e77957ff9a366359ebef8c6c0604ae
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 6%

---

# 的最新發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下章節概述目前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>您可從這裡導覽至舊版的發行說明；例如，2020年、2021年等。

>[!NOTE]
>
>請參閱 [近期檔案更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 如需與版本不直接相關的檔案更新詳細資訊。

## 發行日期 {#release-date}

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2022.6.0)為2022年6月30日。

下一版(2022.7.0)預計於2022年8月8日發行。

## 發行影片 {#release-video}

查看2022年6月版本概述影片，以取得2022.6.0版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 新 [使用者介面](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 內容管理員和內容作者現在可以有效管理（執行動作，例如發佈、取消發佈、複製、移動等）、搜尋/篩選，以及建立無頭使用案例的內容片段。

   ![內容片段主控台](/help/release-notes/assets/cf-ui.png)

* 新 [目錄元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) 不僅可搭配核心元件使用，也可搭配所有元件使用，自動在內容頁面上轉譯ToC。 而且，由於Dispatcher會在伺服器端轉譯並完全快取，因此載入的效率也會很高。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

Experience Manager Assets目前使用Adobe Sensei AI功能 [區分影像中的顏色，並在擷取時自動將這些顏色套用為標籤](/help/assets/color-tag-images.md). 這些標籤可根據影像色彩構成啟用增強的搜尋體驗。 您可以配置在1到40之間的範圍內被標籤到影像的顏色數，以便以後可以根據這些顏色搜索影像。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### 中的新功能 [!DNL Forms] {#forms-features}

* **[整合適用性Forms與Microsoft®電源自動化](/help/forms/forms-microsoft-power-automate-integration.md)**:您現在可以設定適用性表單，在提交時執行Microsoft® Power Automate Cloud Flow。 配置的適用性表單會將捕獲的資料、附件和記錄文檔發送到Power Automate Cloud Flow進行處理。 它可協助您建立自訂資料擷取體驗，同時運用Microsoft® Power Automate的強大功能，圍繞擷取的資料建立業務邏輯，並自動化客戶工作流程。

* **建立最適化表單的精靈**:您可以使用商務使用者易記精靈，快速撰寫適用性Forms。 精靈提供快速的索引標籤導覽，讓您輕鬆選取預先設定的範本、樣式、欄位和提交選項，以建立最適化表單。

   ![建立最適化表單的精靈](/help/release-notes/assets/wizard.png)

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新產品座艙屬性頁面，提供更佳和簡化的概觀

![產品座艙屬性概述](/help/assets/CIF/product_cockpit_properties_overview.png)

* 改善I/O Runtime上第三方連接器的相容性和健全性

* 改善對GQL用戶端配置覆寫的支援（例如設定自訂快取行為）

* 現在支援多個商務端點立即可用，並可透過Cloud Manager進行設定。 您可以在CIF部落格中找到詳細資訊 [此處](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554).


### 錯誤修正 {#bug-fixes-cif}

* 多值產品選擇器欄位將第2個和其他產品顯示為無效

* 產品選擇器偶爾會隱藏在元件後面

## 參考示範附加元件 {#cloud-services-demos}

### 新增功能 {#what-is-new-demos}

* 新的WKND內容與商務範本，透過E2E購物體驗來擴充WKND，其中包含產品目錄、購物車、結帳和myAccount。 此範本使用CIF及其CIF核心元件，因此您也需安裝CIF附加元件。 您可以在CIF部落格中找到詳細資訊 [此處](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e).

![WKND商店](/help/assets/CIF/wknd_shop.png)

![WKND PDP](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 如5月(2022.5.0)發行說明所述，復寫代理管理畫面下的「新增樹狀結構」選項位於 **分發** 標籤已移除。 應改為使用複製具有內容樹層次的包 [管理出版物](/help/operations/replication.md#manage-publication) 或 [發佈內容樹](/help/operations/replication.md#manage-publication#publish-content-tree-workflow) 工作流程。

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月發行的完整清單 [此處](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## 移轉工具 {#migration-tools}

您可以找到移轉工具發行的完整清單 [此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

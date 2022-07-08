---
title: 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: d6038920a5866c19a94980cc14fa46dec48daf51
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 3%

---


# 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

以下部分概述了當前（最新）版本的一般發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從此處，您可以導航到以前版本的發行說明；比如2020年，2021年等等。

>[!NOTE]
>
>請參閱 [最近的文檔更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) 有關與版本不直接相關的文檔更新的詳細資訊。

## 發行日期 {#release-date}

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 本版本(2022.6.0)為2022年6月30日。

下一版(2022.7.0)計畫於2022年7月28日發行。

## 發佈視頻 {#release-video}

查看2022年6月版本概述視頻，瞭解2022.6.0版中添加的功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 新 [用戶介面](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 現在，內容管理員和內容作者可以高效地管理（採取諸如發佈、取消發佈、複製、移動等操作）、搜索/篩選，以及為無頭使用案例建立內容片段。

   ![內容片段控制台](/help/release-notes/assets/cf-ui.png)

* 新 [目錄元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html) 不僅適用於核心元件，而且適用於所有元件，可自動在內容頁面上呈現ToC。 而且，由於它由調度程式在伺服器端呈現並完全快取，因此它還可以高效地載入。

## [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

Experience Manager Assets目前使用Adobe SenseiAI功能 [區分影像中的顏色，並在攝取時自動將這些顏色作為標籤應用](../../assets/color-tag-images.md)。 這些標籤基於影像顏色合成，支援增強的搜索體驗。 您可以配置標籤到影像的顏色數量，以便以後可以根據這些顏色搜索影像。

## [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

### 中的新功能 [!DNL Forms] {#forms-features}

* **[將自適應Forms與Microsoft® Power Automate整合](/help/forms/forms-microsoft-power-automate-integration.md)**:您現在可以配置自適應表單，在提交時運行Microsoft® Power自動化雲流。 配置的自適應表單將捕獲的資料、附件和記錄文檔發送到Power Automate Cloud Flow進行處理。 它幫助您構建自定義資料捕獲體驗，同時利用Microsoft® Power Automate的強大功能，圍繞捕獲的資料構建業務邏輯並自動化客戶工作流。

* **用於建立自適應表單的嚮導**:您可以使用業務用戶友好嚮導快速編寫AdaptiveForms。 該嚮導提供快速頁籤導航，以便輕鬆選擇預先配置的模板、樣式、欄位和提交選項以建立自適應表單。

   ![用於建立自適應表單的嚮導](/help/release-notes/assets/wizard.png)

## CIF附加模組 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新產品座艙屬性頁面，以便更好、更簡化的概述

![產品座艙屬性概述](/help/assets/CIF/product_cockpit_properties_overview.png)

* I/O運行時上第三方連接器的相容性和健壯性得到提高

* 改進了對GQL客戶端配置覆蓋的支援（例如設定自定義快取行為）

* 現在支援開箱即用的多個商業端點，並可通過雲管理器進行配置。 您可以在CIF部落格中查找詳細資訊 [這裡](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554)。


### 錯誤修正 {#bug-fixes-cif}

* 多值產品選取器欄位顯示第二個和其他產品無效

* 產品選取器偶爾隱藏在元件後面

## 參考演示附件 {#cloud-services-demos}

### 新增功能 {#what-is-new-demos}

* 新的WKND內容和商業模板，通過E2E購物體驗擴展了WKND，產品目錄、購物車、結帳和myAccount。 此模板使用CIF及其CIF核心元件，因此您還需要安裝CIF附加元件。 您可以在CIF部落格中查找詳細資訊 [這裡](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e)。

![WKND商店](/help/assets/CIF/wknd_shop.png)

![WKND PDP](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] 作為 [!DNL Cloud Service] 基礎 {#foundation}

### 新增功能 {#what-is-new-foundation}

* 如5月(2022.5.0)發行說明中所述，複製代理管理螢幕下的「添加樹」選項 **分發** 頁籤。 應使用樹層次結構複製內容的包 [管理發布](/help/operations/replication.md#manage-publication) 或 [發佈內容樹](/help/operations/replication.md#manage-publication#publish-content-tree-workflow) 工作流。

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月版本的完整清單 [這裡](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)。

## 遷移工具 {#migration-tools}

您可以找到遷移工具版本的完整清單 [這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)。

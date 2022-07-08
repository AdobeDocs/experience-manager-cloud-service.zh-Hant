---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.5.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.5.0 版發行說明。'
source-git-commit: d6038920a5866c19a94980cc14fa46dec48daf51
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 7%

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

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 本版本(2022.5.0)為2022年6月9日。
下一版(2022.6.0)計畫於2022年6月30日發行。

## 發佈視頻 {#release-video}

查看2022年5月版本概述視頻，瞭解2022.5.0版中添加的功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 搶鮮版頻道中可用的新功能 {#prerelease-features-sites}

* 各種GraphQL功能
* A [新控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 為無頭使用內容片段而優化

## [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* [Dynamic Media智慧成像](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) 現在支援AVIF檔案格式 — 進一步改進Google核心網關重要性（最大內容塗料）,AVIF比WebP提供20%的額外尺寸縮減。 總的來說，AVIF比JPEG（在某些影像中甚至高達76%）提供了41%的平均尺寸縮減率。

* [!UICONTROL Experience Manager AssetsBrand Portal] 現在每十二小時執行一次自動作業，以刪除發佈到的所有Brand PortalAEM資產。 因此，您不需要手動刪除「貢獻」資料夾中的資產，以使資料夾大小低於閾值限制。 請參閱 [Experience Manager Assets·Brand Portal有什麼新聞嗎](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html)。

### [!DNL Assets] 搶鮮版頻道中可用的新功能 {#prerelease-features-assets}

Experience Manager Assets目前使用Adobe SenseiAI功能 [區分影像中的顏色，並在攝取時自動將這些顏色作為標籤應用](/help/assets/color-tag-images.md)。 這些標籤基於影像顏色合成，支援增強的搜索體驗。 您可以配置標籤到影像的顏色數量，以便以後可以根據這些顏色搜索影像。


## [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* **將自適應Forms與Microsoft® Power Automate整合**:您現在可以配置自適應表單，在提交時運行Microsoft® Power自動化雲流。 配置的自適應表單將捕獲的資料、附件和記錄文檔發送到Power Automate Cloud Flow進行處理。 它幫助您構建自定義資料捕獲體驗，同時利用Microsoft® Power Automate的強大功能，圍繞捕獲的資料構建業務邏輯並自動化客戶工作流。

* **用於建立自適應表單的嚮導**:您可以使用業務用戶友好嚮導快速編寫AdaptiveForms。 該嚮導提供快速頁籤導航，以便輕鬆選擇預先配置的模板、樣式、欄位和提交選項以建立自適應表單。

   ![用於建立自適應表單的嚮導](/help/release-notes/assets/wizard.png)

## CIF附加模組 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 快速訪問產品駕駛艙：在站點編輯器中按一下一次即可輕鬆訪問完整的詳細產品資訊

   ![啟用願望清單](/help/assets/CIF/enable-wishlist.png)

* 支援其他營銷商務元件：可將元件配置為顯示附加購物車和附加清單的行動要求

   ![產品駕駛艙的站點編輯器快捷方式](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] 作為 [!DNL Cloud Service] 基礎 {#foundation}

### 新增功能 {#what-is-new-foundation}

* 複製代理管理螢幕下的「添加樹」選項 **分發頁籤**&#x200B;此前已宣佈為棄用的，將於2022年6月20日或不久後刪除。 應使用樹層次結構複製內容的包 [管理發布](/help/operations/replication.md#manage-publication) 或 [發佈內容樹工作流](/help/operations/replication.md#publish-content-tree-workflow)。

* 不建議使用複製代理管理螢幕或複製API來分發大於10 MB（具有屬性的節點，不包括二進位檔案）的內容包，並將在2022年9月12日或之後立即實施。 相反， [管理發布](/help/operations/replication.md#manage-publication) 或 [發佈內容樹工作流](/help/operations/replication.md#publish-content-tree-workflow) 必須用於複製這些大型內容包。 在7月，複製代理管理螢幕的 **分發頁籤** 如果嘗試複製這些大型內容包，則無論何時AEM使用複製API複製這些大型內容包，都會在錯誤日誌中進行複製。 9月，警告將替換為錯誤。 請相應地調整您的流程。

### [!DNL Experience Manager] 搶鮮版頻道中可用的新功能 {#prerelease-features-foundation}

* 現AEM在as a Cloud Service與Unified Shell整合，以改進用戶體驗，並將其與所有其它Experience Cloud應用程式統一。 請參閱 [統一AEMShell上的as a Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) 的子菜單。

## [!DNL Experience Manager] 作為 [!DNL Cloud Service] 基礎安全 {#foundation-security}

### TLS 1.0、1.1棄用

從2022年6月30日起，Experience Manageras a Cloud Service將要求與用戶系統進行更加安全的網路通信和資料交換。 將AEM只使用傳輸層安全性(TLS)1.2協定。 舊版TLS 1.0和1.1版將被棄用。

如果繼續將舊版本的TLS用作1.0、1.1，則可能會失去對Experience Manageras a Cloud Service的訪問權限。

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月版本的完整清單 [這裡](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)。

## 遷移工具 {#migration-tools}

您可以找到遷移工具版本的完整清單 [這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)。

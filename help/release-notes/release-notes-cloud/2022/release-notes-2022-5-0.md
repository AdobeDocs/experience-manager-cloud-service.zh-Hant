---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.5.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.5.0 版發行說明。'
exl-id: 1b867582-e34c-435b-b8f8-fc71dddcaccb
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 7%

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

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2022.5.0)為2022年6月9日。
下一版(2022.6.0)預計於2022年6月30日推出。

## 發行影片 {#release-video}

請觀看2022年5月版本概述影片，以取得2022.5.0版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 搶鮮版頻道中可用的新功能 {#prerelease-features-sites}

* 各種GraphQL功能
* A [新主控台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 針對無頭使用內容片段而最佳化

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* [Dynamic Media Smart Imaging](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f) 現在支援AVIF檔案格式 — 進一步改進Google核心網路重要（最大的內容塗料）,AVIF可通過WebP實現20%的額外尺寸縮減。 AVIF總計可比JPEG減少41%的平均大小（在某些影像中甚至高達76%）。

* [!UICONTROL Experience Manager AssetsBrand Portal] 現在會每十二小時執行自動作業，刪除發佈至AEM的所有Brand Portal資產。 因此，您不需要手動刪除「貢獻」資料夾中的資產，即可將資料夾大小維持在臨界值限制以下。 請參閱 [Experience Manager Assets Brand Portal的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

### [!DNL Assets] 搶鮮版頻道中可用的新功能 {#prerelease-features-assets}

Experience Manager Assets目前使用Adobe Sensei AI功能 [區分影像中的顏色，並在擷取時自動將這些顏色套用為標籤](/help/assets/color-tag-images.md). 這些標籤可根據影像色彩構成啟用增強的搜尋體驗。 您可以配置在1到40之間的範圍內被標籤到影像的顏色數，以便以後可以根據這些顏色搜索影像。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 搶鮮版頻道中可用的新功能 {#prerelease-features-forms}

* **整合適用性Forms與Microsoft®電源自動化**:您現在可以設定適用性表單，在提交時執行Microsoft® Power Automate Cloud Flow。 配置的適用性表單會將捕獲的資料、附件和記錄文檔發送到Power Automate Cloud Flow進行處理。 它可協助您建立自訂資料擷取體驗，同時運用Microsoft® Power Automate的強大功能，圍繞擷取的資料建立業務邏輯，並自動化客戶工作流程。

* **建立最適化表單的精靈**:您可以使用商務使用者易記精靈，快速撰寫適用性Forms。 精靈提供快速的索引標籤導覽，讓您輕鬆選取預先設定的範本、樣式、欄位和提交選項，以建立最適化表單。

   ![建立最適化表單的精靈](/help/release-notes/assets/wizard.png)

## CIF附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 快速訪問產品座艙：在Sites Editor中按一下即可輕鬆存取完整的詳細產品資訊

   ![啟用願望清單](/help/assets/CIF/enable-wishlist.png)

* 支援其他行銷商務元件：元件可設定為顯示附加至購物車和附加至願望清單呼叫動作

   ![Sites編輯器快速鍵至產品座艙](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 複製代理管理螢幕下的「添加樹」選項 **「分發」頁簽**，先前宣佈為已過時的，將於2022年6月20日或之後不久移除。 應改為使用複製具有內容樹層次的包 [管理出版物](/help/operations/replication.md#manage-publication) 或 [發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow).

* 不建議使用復寫代理管理螢幕或復寫API來分送大於10 MB的內容套件（具有屬性的節點，不包括二進位檔），且將於2022年9月12日或之後不久強制執行。 相反， [管理出版物](/help/operations/replication.md#manage-publication) 或 [發佈內容樹工作流程](/help/operations/replication.md#publish-content-tree-workflow) 必須用來複製這些大型內容包。 7月時，復寫代理管理畫面的 **「分發」頁簽** 如果每當使用復寫API來復寫這些大型內容包時，都嘗試復寫這些大型內容包，並在AEM錯誤日誌中。 9月時，警告將替換為錯誤。 請據此調整您的流程。

### [!DNL Experience Manager] 搶鮮版頻道中可用的新功能 {#prerelease-features-foundation}

* AEM as a Cloud Service現已與Unified Shell整合，以改善使用者體驗，並與所有其他Experience Cloud應用程式統一。 請參閱 [AEMas a Cloud Service於Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) 以取得更多詳細資訊。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation安全性 {#foundation-security}

### 不再使用TLS 1.0、1.1

自2022年6月30日起，Experience Manageras a Cloud Service將需要與使用者系統進行更安全的網路通訊和資料交換。 AEM將專門使用傳輸層安全性(TLS)、1.2通訊協定。 舊版TLS 1.0和1.1將遭取代。

如果您繼續使用舊版TLS 1.0、1.1，您可能會失去Experience Manageras a Cloud Service的存取權。

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月發行的完整清單 [此處](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## 移轉工具 {#migration-tools}

您可以找到移轉工具發行的完整清單 [此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

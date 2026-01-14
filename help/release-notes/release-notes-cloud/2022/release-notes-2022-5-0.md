---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.5.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.5.0 版發行說明。'
exl-id: 1b867582-e34c-435b-b8f8-fc71dddcaccb
feature: Release Information
role: Admin
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 26%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2022.5.0 版發行說明 {#release-notes}

以下章節概述2022.5.0版[!DNL Experience Manager] as a Cloud Service的功能發行說明。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service]目前版本(2022.5.0)的發行日期為2022年6月9日。
下一個版本(2022.6.0)計畫於2022年6月30日發行。

## 發行影片 {#release-video}

請觀看 2022 年 5 月版本概觀影片，了解 2022.5.0 版本新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 發行前通道中可用的新功能 {#prerelease-features-sites}

* 各種GraphQL功能
* 針對無周邊使用內容片段而最佳化的[新主控台](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* [Dynamic Media智慧型影像](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f)現在支援AVIF檔案格式 — 進一步改善Google Core Web Vital （最大內容繪製）；相較於WebP，AVIF提供20%的額外大小縮減。 相較於JPEG，AVIF總計平均大小縮減率高達41% （在某些影像中甚至高達76%）。

* [!UICONTROL Experience Manager Assets Brand Portal]現在每12小時執行一次自動工作，以刪除發佈至AEM的所有Brand Portal資產。 因此，您不需要手動刪除「貢獻」資料夾中的資產，使資料夾大小不超過臨界值限制。請參閱[Experience Manager Assets Brand Portal的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html)。

### [!DNL Assets] 發行前通道中可用的新功能 {#prerelease-features-assets}

Experience Manager Assets現在使用Adobe AI功能[區分影像中的顏色，並在擷取時自動將這些差異套用為標籤](/help/assets/color-tag-images.md)。 這些標籤會根據影像顏色組合來增強搜尋體驗。 您可以設定標籤到影像的顏色數量（範圍在1到40之間），以便日後可以根據這些顏色搜尋影像。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 發行前通道中可用的新功能 {#prerelease-features-forms}

* **整合最適化Forms與Microsoft® Power Automate**：您現在可以設定最適化表單，在提交時執行Microsoft® Power Automate雲端流程。 設定的最適化表單會將擷取的資料、附件和記錄文件傳送到 Power Automate Cloud Flow 進行處理。它可幫助您建立自訂資料擷取體驗，同時利用Microsoft® Power Automate的強大功能，圍繞擷取的資料建立商業邏輯，並自動化客戶工作流程。

* **用於建立最適化表單的精靈**：您可以使用業務使用者友善的精靈來快速撰寫最適化Forms。 精靈提供快速索引標籤導覽，以便輕鬆選取用於建立最適化表單的預先設定範本、樣式、欄位和提交選項。

  ![建立最適化表單的精靈](/help/release-notes/assets/wizard.png)

## CIF 附加元件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 快速存取產品駕駛艙：在網站編輯器中按一下滑鼠，即可輕鬆存取完整詳細的產品資訊

<!-- Image was not found during PR validation despite correct path   ![Enable wantlist](/help/assets/CIF/enable-wishlist.png) -->

* 支援其他行銷商務元件：元件可設定為顯示加入購物車和加入願望清單call-to-action

  ![網站編輯器到產品駕駛艙的捷徑](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 復寫代理程式管理畫面的&#x200B;**Distribute索引標籤**&#x200B;下的「新增樹狀結構」選項（先前宣佈已棄用），已於2022年6月20日或隨後不久移除。 應改用[管理發布](/help/operations/replication.md#manage-publication)或[發佈內容樹狀工作流程](/help/operations/replication.md#publish-content-tree-workflow)，來復寫具有樹狀階層內容的封裝。

* 使用復寫代理程式管理畫面或復寫API來分發大於10 MB的內容套件（具有屬性的節點，不包括二進位檔案）已過時，並自2022年9月12日或隨後不久強制棄用。 必須改用[管理出版物](/help/operations/replication.md#manage-publication)或[發佈內容樹狀工作流程](/help/operations/replication.md#publish-content-tree-workflow)來復寫這些大型內容封裝。 在7月，如果嘗試復寫這些大型內容套件，復寫代理程式管理畫面的&#x200B;**散發標籤**&#x200B;中會出現警告訊息，而且每當使用復寫API復寫這些大型內容套件時，AEM錯誤記錄中也會出現警告訊息。 在9月，警告取代為錯誤。 相應地調整您的流程。

### [!DNL Experience Manager] 發行前通道中可用的新功能 {#prerelease-features-foundation}

* AEM as a Cloud Service現在與Unified Shell整合，以改進使用者體驗，並將其與所有其他Experience Cloud應用程式統一。 如需詳細資訊，請參閱Unified Shell上的[AEM as a Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md)。

## [!DNL Experience Manager]作為[!DNL Cloud Service] Foundation安全性 {#foundation-security}

### 不再使用TLS 1.0、1.1

自2022年6月30日起，Experience Manager as a Cloud Service將要求與使用者系統進行更安全的網路通訊和資料交換。 AEM將僅使用傳輸層安全性(TLS) 1.2通訊協定。 舊版TLS 1.0和1.1現已棄用。

如果您繼續將舊版TLS用作1.0、1.1，則可能無法存取Experience Manager as a Cloud Service。

## Cloud Manager {#cloud-manager}

您可以在[這裡](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0 版發行說明。'
exl-id: 6c86838a-cabf-4770-b1ae-618af70193a2
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 20%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2022.4.0 版發行說明 {#release-notes}

以下章節概述2022.4.0版的功能發行說明 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>從這裡，您可以瀏覽至舊版的發行說明；例如，2020、2021 等版本。

>[!NOTE]
>
>請參閱[近期文件更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)瞭解與版本不直接相關的文件更新的詳細資料。

## 發行日期 {#release-date}

的發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 目前版本(2022.4.0)為2022年5月5日。
下一個版本(2022.5.0)計畫於2022年6月9日發行。

## 發行影片 {#release-video}

請檢視 [2022年4月版本總覽](https://video.tv.adobe.com/v/342612?quality=12) 2022.4.0版新增功能摘要影片。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新功能 {#sites-features}

* 內容模型資料型別現在可以定義為 [可翻譯](/help/assets/content-fragments/content-fragments-models.md#properties) 使用內容模型編輯器中的簡單核取方塊。 此外，AEM翻譯規則和設定會自動更新。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新功能 {#assets-features}

* 您現在可以 [排序標籤](/help/assets/organize-assets.md#use-tags-to-organize-assets) 標籤選擇器視窗中的標籤名稱、建立日期或修改日期，以遞增或遞減順序顯示。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **通訊 — Forms as a Cloud ServiceSDK中的檔案操作API支援**： [Document Manipulation API](/help/forms/aem-forms-cloud-service-communications.md) 協助組合、重新排列和驗證PDF檔案。 您現在可以透過AEM Formsas a Cloud ServiceSDK在本機開發環境中使用Communications - Document Generation API。

* **使用自訂XCI產生記錄檔案**：您現在可以 [使用自訂XCI檔案來設定記錄檔案的各種屬性](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). 它會以自訂變更覆寫主XCI。 它提供對產生記錄檔案的更多控制權，增加個人化和自訂機會。

* **在最適化表單中使用隱藏的驗證碼**：您可以使用 [隱藏的驗證碼，僅在可疑活動的情況下顯示驗證碼質詢](/help/forms/captcha-adaptive-forms.md). 如果未發現可疑活動，則不會顯示驗證碼質詢。 它有助於評估人工表單完成情況，而無需核取方塊要求，減少自訂工作，並改善終端使用者體驗。

* **表單資料模型設定**：您現在可以 [跨環境重複使用表單資料模型設定](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config)，簡化資料整合併降低IT成本。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### SDK建置分析器 {#sdk-build-analyzers}

AEMas a Cloud ServiceSDK Build Analyzer Maven外掛程式會偵測Maven專案中的問題，包括遺漏的相依性。 它讓開發人員有機會在本機開發期間以及使用Cloud Manager部署到雲端環境之前發現問題。

最近新增了一個新分析器：

* `content-packages-validation`  — 驗證在部署期間安裝的套件的格式正確的內容語法和結構

強烈建議使用最新版本的分析器更新您的Maven專案，或者包含分析器（如果尚未更新）。 如需詳細資訊，請參閱檔案 [此處](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html).

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基礎安全性 {#foundation-security}

### 不再使用TLS 1.0、1.1

自2022年6月30日起，Experience Manageras a Cloud Service將需要與使用者系統進行更安全的網路通訊和資料交換。 AEM打算專門使用傳輸層安全性(TLS) 1.2通訊協定。 舊版TLS 1.0和1.1現已棄用。

如果您繼續將舊版TLS用作1.0、1.1，則可能無法存取Experience Manageras a Cloud Service。

## Cloud Manager {#cloud-manager}

您可以在[此處](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月發行的完整清單。

## 移轉工具 {#migration-tools}

您可以在[此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到移轉工具版本的完整清單。

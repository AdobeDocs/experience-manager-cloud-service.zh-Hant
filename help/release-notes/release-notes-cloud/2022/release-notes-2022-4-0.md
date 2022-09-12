---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0 版發行說明。'
exl-id: 6c86838a-cabf-4770-b1ae-618af70193a2
source-git-commit: f42cf1b82f7cf42be2afd30d69d71354fe0afeb3
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 5%

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

發行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新發行(2022.4.0)為2022年5月5日。
下一版(2022.5.0)預計於2022年6月9日發行。

## 發行影片 {#release-video}

查看 [2022年4月發行概述](https://video.tv.adobe.com/v/342612?quality=12) 影片，以取得2022.4.0版中新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 內容模型資料類型現在可定義為 [可翻譯](/help/assets/content-fragments/content-fragments-models.md#properties) 在內容模型編輯器中使用簡單核取方塊。 此外，也會自動更新AEM翻譯規則和設定。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* 您現在可以 [排序標籤](/help/assets/organize-assets.md#use-tags-to-organize-assets) 依據標籤名稱、建立日期或修改日期，以遞增或遞減順序在標籤選取器視窗中顯示。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **通訊 — Forms as a Cloud ServiceSDK中的檔案操作API支援**: [檔案操作API](/help/forms/aem-forms-cloud-service-communications.md) 幫助組合、重新排列和驗證PDF文檔。 您現在可以透過AEM Forms as a Cloud ServiceSDK，在本機開發環境中使用通訊 — 檔案產生API。

* **使用自訂XCI產生記錄檔案**:您現在可以 [使用自訂XCI檔案來設定記錄檔案的各種屬性](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). 會以自訂變更覆寫主XCI。 它提供了對記錄文檔生成的更多控制，增加了個人化和定制機會。

* **在最適化表單中使用不可見的驗證碼**:您可以使用 [隱形驗證碼，僅在可疑活動時顯示驗證碼挑戰](/help/forms/captcha-adaptive-forms.md). 如果未發現任何可疑活動，則不顯示驗證碼質詢。 它有助於評估人工表單填寫情況，而無需核取方塊要求、減少自訂工作，並改善一般使用者體驗。

* **表單資料模型設定**:您現在可以 [跨環境重複使用表單資料模型配置](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config)，簡化資料整合併降低IT成本。


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### SDK建置分析器 {#sdk-build-analyzers}

AEMas a Cloud ServiceSDK建置Analyzer Maven外掛程式會偵測Maven專案中的問題，包括缺少相依性。 這可讓開發人員在本機開發期間，即可在使用Cloud Manager部署至雲端環境之前，先行探索問題。

最近新增了新的分析器：

* `content-packages-validation`  — 驗證部署過程中將安裝的包的格式正確的內容語法和結構

強烈建議您使用最新版本的分析器更新您的maven專案，或納入分析器（如果尚未這麼做）。 如需詳細資訊，請參閱本檔案 [此處](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html).

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation安全性 {#foundation-security}

### 不再使用TLS 1.0、1.1

自2022年6月30日起，Experience Manageras a Cloud Service將需要與使用者系統進行更安全的網路通訊和資料交換。 AEM將專門使用傳輸層安全性(TLS)、1.2通訊協定。 舊版TLS 1.0和1.1將遭取代。

如果您繼續使用舊版TLS 1.0、1.1，您可能會失去Experience Manageras a Cloud Service的存取權。

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月發行的完整清單 [此處](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## 移轉工具 {#migration-tools}

您可以找到移轉工具發行的完整清單 [此處](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

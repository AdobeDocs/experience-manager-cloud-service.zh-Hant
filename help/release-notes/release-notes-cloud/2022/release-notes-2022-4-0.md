---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0 版發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2022.4.0 版發行說明。'
exl-id: 6c86838a-cabf-4770-b1ae-618af70193a2
source-git-commit: f42cf1b82f7cf42be2afd30d69d71354fe0afeb3
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 5%

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

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 當前版本(2022.4.0)為2022年5月5日。
下一版(2022.5.0)計畫於2022年6月9日發行。

## 發佈視頻 {#release-video}

看看 [2022年4月發佈概述](https://video.tv.adobe.com/v/342612?quality=12) 視頻，瞭解2022.4.0版中添加的功能摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 中的新功能 [!DNL Sites] {#sites-features}

* 內容模型資料類型現在可定義為 [可譯](/help/assets/content-fragments/content-fragments-models.md#properties) 使用內容模型編輯器中的簡單複選框。 此外，還AEM會自動更新翻譯規則和配置。

## [!DNL Experience Manager Assets] 作為 [!DNL Cloud Service] {#assets}

### 中的新功能 [!DNL Assets] {#assets-features}

* 你現在可以 [排序標籤](/help/assets/organize-assets.md#use-tags-to-organize-assets) 按照標籤名稱、建立日期或修改日期的升序或降序排列。


## [!DNL Experience Manager Forms] 作為 [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **通信 — Formsas a Cloud ServiceSDK中的文檔操作API支援**: [文檔處理API](/help/forms/aem-forms-cloud-service-communications.md) 幫助合併、重新排列和驗證PDF文檔。 現在，您可以借助AEM Formsas a Cloud ServiceSDK在本地開發環境中使用Communications - Document Generation API。

* **使用自定義XCI生成記錄文檔**:你現在可以 [使用自定義XCI檔案設定記錄文檔的各種屬性](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file)。 它用自定義更改覆蓋主XCI。 它提供了對記錄文檔生成的更多控制，增加了個性化和定制機會。

* **以自適應形式使用不可見的驗證碼**:您可以使用 [只有在可疑活動時，才能顯示驗證碼挑戰](/help/forms/captcha-adaptive-forms.md)。 如果未發現可疑活動，則不顯示驗證碼質詢。 它有助於評估人形表單的完成情況，而無需複選框要求，減少定制工作，並改善最終用戶體驗。

* **表單資料模型配置**:你現在可以 [跨環境重用表單資料模型配置](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config)、簡化資料整合併降低IT成本。


## [!DNL Experience Manager] 作為 [!DNL Cloud Service] 基礎 {#foundation}

### SDK生成分析器 {#sdk-build-analyzers}

as a Cloud ServiceAEMSDK生成分析器Maven插件可檢測給定項目中的問題，包括缺少依賴項。 它為開發人員提供了在本地開發過程中發現問題的機會，而且遠在使用Cloud Manager部署到雲環境之前。

最近添加了一個新分析器：

* `content-packages-validation`  — 驗證部署過程中將安裝的包的格式正確的內容語法和結構

強烈建議使用分析器的最新版本更新您的主項目，或者如果尚未更新，則包括分析器。 有關詳細資訊，請參閱文檔 [這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)。

## [!DNL Experience Manager] 作為 [!DNL Cloud Service] 基礎安全 {#foundation-security}

### TLS 1.0、1.1棄用

從2022年6月30日起，Experience Manageras a Cloud Service將要求與用戶系統進行更加安全的網路通信和資料交換。 將AEM只使用傳輸層安全性(TLS)1.2協定。 舊版TLS 1.0和1.1版將被棄用。

如果繼續將舊版本的TLS用作1.0、1.1，則可能會失去對Experience Manageras a Cloud Service的訪問權限。

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月版本的完整清單 [這裡](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)。

## 遷移工具 {#migration-tools}

您可以找到遷移工具版本的完整清單 [這裡](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)。

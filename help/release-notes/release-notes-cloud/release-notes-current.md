---
title: 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 當前發行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 7ee2e43ab8a5726b2ecf7f157f67b5f3cc73fcff
workflow-type: tm+mt
source-wordcount: '719'
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

發佈日期 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 當前版本(2022.4.0)為2022年5月5日。
下一版(2022.5.0)計畫於2022年5月26日發行。

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

## CIF附加模組 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 快速訪問產品駕駛艙：在站點編輯器中按一下一次即可輕鬆訪問完整的詳細產品資訊

   ![啟用願望清單](/help/assets/CIF/enable-wishlist.png)

* 支援其他營銷商務元件：可將元件配置為顯示附加購物車和附加清單的行動要求

   ![產品駕駛艙的站點編輯器快捷方式](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## [!DNL Experience Manager] 作為 [!DNL Cloud Service] 基礎 {#foundation}

### SDK生成分析器 {#sdk-build-analyzers}

as a Cloud ServiceAEMSDK生成分析器Maven插件可檢測給定項目中的問題，包括缺少依賴項。 它為開發人員提供了在本地開發過程中發現問題的機會，而且遠在使用Cloud Manager部署到雲環境之前。

最近添加了一個新分析器：

* `content-packages-validation`  — 驗證部署過程中將安裝的包的格式正確的內容語法和結構

強烈建議使用分析器的最新版本更新您的主項目，或者如果尚未更新，則包括分析器。 有關詳細資訊，請參閱文檔 [這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)。

## Cloud Manager {#cloud-manager}

您可以找到Cloud Manager每月版本的完整清單 [這裡](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)。

## 最佳做法分析器 {#bpa-release}

### 發行日期 {#release-date-bpa}

最佳做法分析器2.1.28版的發佈日期為2022年4月22日。

### 新增功能 {#what-is-new-bpa}

* 能夠檢測和報告不支援的Asset Manager API的使用情況。 as a Cloud Service中不再支援四個APIAEM。 客戶應確保不再使用這些API，並應使用新的資產上載方法。

* 能夠檢測內容片段模板的使用情況。 不再支援在as a Cloud Service上建立新內容片段的內容片段模AEM板。 客戶將需要建立內容片段模型以替換內容片段模板。

* 能夠在儲存庫中資產的元節點下檢測具有100個以上子體的資產。 建議在載入包含此類資產的資料夾時刪除不需要的元資料節點來提高效能。

* 能夠檢測和報告所使用的資料儲存類型。

* 已為窗體門戶AEM更新模式。

### 錯誤修正 {#bug-fixes-bpa}

* BPA報告的是核心元件的調查結果，而不是只報告客戶元件。 這個已經修復了。

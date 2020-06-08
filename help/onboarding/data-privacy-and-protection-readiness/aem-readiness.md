---
title: 資料保護與資料隱私權法規- Adobe Experience Manager雲端服務就緒性
description: '瞭解Adobe Experience Manager如何以雲端服務的方式支援各種資料保護與資料隱私權規定； 包括歐盟通用資料保護規則(GDPR)、加州消費者隱私法，以及如何在將新AEM實作為雲端服務專案時符合規定。 '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# Adobe Experience Manager作為雲端服務準備，以符合資料保護與資料隱私權法規 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本檔案內容不構成法律咨詢，不代表法律咨詢。
>
>請洽詢貴公司的法律部門，以取得有關資料保護與資料隱私權法規的建議。

>[!NOTE]
>
>如需Adobe對隱私權問題之回應，以及這對您身為Adobe客戶意味著什麼的詳細資訊，請參 [閱Adobe的隱私權中心](https://www.adobe.com/privacy.html)。

Adobe提供檔案和程式（當有API時），讓客戶隱私權管理員或AEM管理員處理資料保護和資料隱私權要求，並協助客戶遵守這些規定。 說明的程式可讓客戶手動或從外部入口網站或服務呼叫API（若有的話），以執行法規要求。

>[!CAUTION]
>
>此處記載的詳細資訊僅限Adobe Experience Manager做為雲端服務。
>
>來自其他Adobe隨選服務的資料，連同任何相關的隱私權要求，都需要對該服務採取行動。
>
>如需詳細資訊， [請參閱Adobe的隱私權中心](https://www.adobe.com/privacy.html)。

## 簡介 {#introduction}

Adobe Experience Manager的雲端服務執行個體，以及在其上執行的應用程式，都歸客戶所有和營運。

因此， GDPR、CCPA等資料保護法規在很大程度上是客戶的責任。

作為簡短的介紹，資料隱私和保護法規包括了新規則，應遵循新規則，其角色包括：

* 業務實體(CCPA)和／或資料控制器(GDPR)

* 服務提供商(CCPA)和／或資料處理器(GDPR)

這些條例的主要規定是：

1. 將個人資料的定義擴充為包含所有唯一ID; 直接和間接可識別的資料。

2. 已強化同意要求。

3. 增加對刪除權限（資料擦除）的關注。

4. 選擇退出資料銷售。

若是Adobe Experience Manager的雲端服務：

* 客戶擁有並操作執行個體和在其上執行的應用程式。

   * 這有效地意味著客戶管理法規角色，包括業務實體和服務提供商、資料控制器和資料處理器等。

   * Adobe Experience Platform Privacy Service不屬於AEM的工作流程，如下圖所示。

* AEM包含客戶隱私權管理員和／或AEM管理員執行隱私權法規要求的檔案和程式； 手動或透過API（若有）。

* 未新增任何服務或UI。

   * 相反，程式和API會記錄在案，以供處理隱私權法規要求的客戶UI/入口網站使用。

* AEM將不包含任何現成可用的工具，以支援隱私權要求工作流程。

   * Adobe將提供客戶的隱私權管理員和／或AEM管理員的檔案和程式，讓他們可以手動執行與隱私權規定相關的要求。

Adobe提供處理與Adobe Experience Manager雲端服務之存取、刪除及選擇退出相關隱私權要求的程式。 在某些情況下，可從客戶開發的入口網站或指令碼呼叫API，以協助自動化。

下圖說明隱私權要求工作流程的外觀（使用Adobe Experience Manager 6.5說明）:

![資料保護與隱私權](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager雲端服務與法規準備 {#aem-as-a-cloud-service-and-regulatory-readiness}

如需AEM a Cloud Service產品區域的法規檔案，請參閱以下章節。

## Adobe Experience Manager雲端服務基礎 {#aem-foundation}

See [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Adobe Experience Manager 雲端服務 Sites {#aem-sites}

See [AEM Sites Readiness for Data Protection and Data Privacy Regulations.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager與Adobe Target和Adobe Analytics的雲端服務整合 {#aem-integration-with-adobe-target-adobe-analytics}

這些Adobe Experience Manager作為雲端服務的整合，與資料保護和隱私權（例如GDPR）就緒服務整合。 AEM中不會儲存Adobe Target或Adobe Analytics中與整合相關的個人資料。
如需詳細資訊，請參閱：

* [Adobe Target —— 隱私權概觀](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics資料隱私權工作流程](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

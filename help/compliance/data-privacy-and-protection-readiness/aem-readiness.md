---
title: 資料保護和資料隱私權法規 - Adobe Experience Manager as a Cloud Service 整備
description: 了解對各種資料保護和資料隱私權法規的 Adobe Experience Manager as a Cloud Service 支援；包括歐盟一般資料保護規範 (GDPR)、加州消費者隱私法，以及在實施新的 AEM as a Cloud Service 專案時如何遵守。
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: ht
source-wordcount: '730'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 的資料保護和資料隱私權法規整備 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文件的內容並不構成法律建議，其宗旨並非取代專業的法律建議。
>
>有關資料保護和數據隱私權法規的建議，請諮詢貴公司的法律部門。

>[!NOTE]
>
>如需關於 Adobe 對隱私權問題的回應以及這對於您身為 Adobe 客戶所代表之意義的詳細資訊，請參閱 [Adobe 隱私權中心](https://www.adobe.com/tw/privacy.html)。

Adobe 正為客戶隱私權管理員或 AEM 管理員提供文件和程序 (可用時透過 API) 以處理資料保護和資料隱私權請求，並幫助我們的客戶遵守這些法規。記錄的程序將允許客戶從外部入口網站或服務以手動方式或透過呼叫 API (可用時) 來執行監管請求。

>[!CAUTION]
>
>此處記錄的詳細資料僅限於 Adobe Experience Manager as a Cloud Service。
>
>來自其他 Adobe 隨選服務的資料以及任何相關的隱私權請求將需要對該服務採取動作。
>
>如需更進一步的資訊，請參閱 [Adobe 的隱私權中心](https://www.adobe.com/tw/privacy.html)。

## 簡介 {#introduction}

Adobe Experience Manager as a Cloud Service 執行個體以及在其上執行的應用程式由我們的客戶所擁有和營運。

因此，GDPR、CCPA 等資料保護法規主要是客戶的責任。

簡單介紹，資料隱私權和保護法規包括以下角色要遵循的新規則：

* 商業實體 (CCPA) 和/或資料控制者 (GDPR)

* 服務提供者 (CCPA) 和/或資料處理者 (GDPR)

這些法規的主要規定包括：

1. 擴大個人資料的定義以包括所有唯一 ID；如直接和間接可識別的資料。

2. 加強同意要求。

3. 更加關注刪除權 (資料清除)。

4. 選擇退出資料銷售。

對於 Adobe Experience Manager as a Cloud Service：

* 執行個體，以及在其上執行的應用程式由客戶所擁有和營運。

   * 這實際上意味著客戶管理監管角色，包括商業實體和服務提供者、資料控制者和資料處理者等。

   * Adobe Experience Platform Privacy Service 不會成為 AEM 工作流程的一部分，如下圖所示。

* AEM 包含相關文件和程序，供客戶隱私權管理員和/或 AEM 管理員執行隱私權法規請求；無論是以手動方式或透過 API (可用時)。

* 沒有新增新的服務或 UI。

   * 反而是記錄各個程序和 API，以供處理隱私權監管請求的客戶 UI/入口網站使用。

* AEM 將不包括任何現成工具來支援隱私權請求工作流程。

   * Adobe 將為客戶隱私權管理員和/或 AEM 管理員提供文件和程序；讓他們以手動方式執行與隱私權法規相關的請求。

Adobe 正提供各項程序，用於處理與 Access、刪除和選擇退出 Adobe Experience Manager as a Cloud Service 相關的隱私權請求。在某些情況下，可以從客戶開發的入口網站或指令碼中呼叫可用的 API，以幫助實現自動化。

下圖說明了隱私權請求工作流程的模樣 (使用 Adobe Experience Manager 6.5 進行說明)：

![資料保護和隱私權](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as a Cloud Service 和法規整備 {#aem-as-a-cloud-service-and-regulatory-readiness}

請參閱以下各節，了解 AEM as a Cloud Service 產品領域的監管文件。

## Adobe Experience Manager as a Cloud Service 基礎 {#aem-foundation}

請參閱[AEM Foundation 的資料保護與資料隱私權法規整備](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)

## Adobe Experience Manager as a Cloud Service Sites {#aem-sites}

請參閱 [AEM Sites 的資料保護與資料隱私權法規整備。](/help/compliance/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager as a Cloud Service 與 Adobe Target 和 Adobe Analytics 整合 {#aem-integration-with-adobe-target-adobe-analytics}

這些 Adobe Experience Manager as a Cloud Service 整合具有資料保護和隱私權 (例如 GDPR) 整備服務。來自 Adobe Target 或 Adobe Analytics 與整合相關的個人資料不會儲存在 AEM 中。
如需進一步詳細資訊，請參閱：

* [Adobe Target - 隱私權概觀](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics 資料隱私權工作流程](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)

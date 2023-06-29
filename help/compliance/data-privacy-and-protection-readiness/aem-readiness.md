---
title: 資料保護和資料隱私權法規 - Adobe Experience Manager as a Cloud Service 整備
description: 瞭解Adobe Experience Manager as a Cloud Service對各種資料保護和資料隱私權法規的支援。 這些法規包括歐盟一般資料保護規範(GDPR)、加州消費者隱私法，以及在實施新的AEMas a Cloud Service專案時如何遵守。
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 44%

---

# Adobe Experience Manager as a Cloud Service 的資料保護和資料隱私權法規整備 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文件的內容並不構成法律建議，其宗旨並非取代專業的法律建議。
>
>如需資料保護與資料隱私權法規的相關建議，請洽詢貴公司的法律部門。

>[!NOTE]
>
>如需有關Adobe對隱私權問題的回應，以及此隱私權對您身為Adobe客戶所代表之意義的詳細資訊，請參閱 [Adobe隱私權中心](https://www.adobe.com/tw/privacy.html).

Adobe正為客戶隱私權管理員或AEM管理員提供檔案和程式（可用時透過API）。 本檔案可協助管理員處理資料保護和資料隱私權請求，並協助Adobe客戶遵守這些法規。 記錄的程式可讓客戶從外部入口網站或服務，手動執行法規要求或呼叫API （若有）。

>[!CAUTION]
>
>此處記錄的詳細資料僅限於 Adobe Experience Manager as a Cloud Service。
>
>來自其他Adobe隨選服務的資料以及任何相關的隱私權請求需要對該服務採取動作。
>
>如需詳細資訊，請參閱 [Adobe隱私權中心](https://www.adobe.com/tw/privacy.html).

## 簡介 {#introduction}

Adobe Experience Manager as a Cloud Service執行個體以及在其上執行的應用程式是由Adobe客戶所擁有和營運。

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

   * 這種所有權實際上意味著客戶管理監管角色，包括商業實體和服務提供者、資料控制者和資料處理者等。

   * Adobe Experience Platform Privacy Service不是AEM工作流程的一部分，如下圖所示。

* AEM 包含相關文件和程序，供客戶隱私權管理員和/或 AEM 管理員執行隱私權法規請求；無論是以手動方式或透過 API (可用時)。

* 沒有新增新的服務或 UI。

   * 反而是記錄各個程序和 API，以供處理隱私權監管請求的客戶 UI/入口網站使用。

* AEM不包含任何現成工具來支援隱私權請求工作流程。

   * Adobe會為客戶的隱私權管理員或AEM管理員（或兩者）提供檔案和程式，讓他們以手動方式執行與隱私權法規相關的請求。

Adobe提供處理隱私權請求的程式，這些請求與Adobe Experience Manager as a Cloud Service的存取、刪除和選擇退出相關。 有時候，可以從客戶開發的入口網站或指令碼中呼叫可用的API，以協助實現自動化。

下圖說明了隱私權請求工作流程的模樣 (使用 Adobe Experience Manager 6.5 進行說明)：

![資料保護和隱私權](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as a Cloud Service 和法規整備 {#aem-as-a-cloud-service-and-regulatory-readiness}

如需有關AEMas a Cloud Service產品領域的監管檔案，請參閱以下各節。

## Adobe Experience Manager as a Cloud Service 基礎 {#aem-foundation}

請參閱[AEM Foundation 的資料保護與資料隱私權法規整備](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)

## Adobe Experience Manager as a Cloud Service Sites {#aem-sites}

另請參閱 [AEM Sites的資料保護與資料隱私權法規整備](/help/compliance/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager as a Cloud Service 與 Adobe Target 和 Adobe Analytics 整合 {#aem-integration-with-adobe-target-adobe-analytics}

Adobe Experience Manager as a Cloud Service上的這些整合具有資料保護和隱私權（例如GDPR）整備服務。 來自 Adobe Target 或 Adobe Analytics 與整合相關的個人資料不會儲存在 AEM 中。
如需詳細資訊，請參閱：

* [Adobe Target - 隱私權概觀](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation.html)

* [Adobe Analytics 資料隱私權工作流程](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

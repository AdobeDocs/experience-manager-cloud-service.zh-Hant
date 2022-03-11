---
title: 資料保護和資料隱私法規 — Adobe Experience Manager as a Cloud Service就緒性
description: 瞭解Adobe Experience Manager as a Cloud Service對各種資料保護和資料隱私法規的支援；包括歐盟一般資料保護條例(GDPR)、加利福尼亞消費者隱私法以及實施新as a Cloud Service項目時如AEM何遵守。
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud Service為資料保護和資料隱私法規做好準備 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本檔案的內容不構成法律咨詢，也不是作為法律咨詢的替代。
>
>有關資料保護和資料隱私法規的建議，請咨詢您公司的法律部門。

>[!NOTE]
>
>有關Adobe對隱私問題的響應以及這對您作為Adobe客戶意味著什麼的詳細資訊，請參閱 [Adobe隱私中心](https://www.adobe.com/privacy.html)。

Adobe正在提供文檔和過程（如果有API），讓客戶隱私管理員或管理員處理資料保護和資料隱私請求AEM，並幫助我們的客戶遵守這些法規。 所記錄的過程將允許客戶手動或通過從外部門戶或服務調用API（如果可用）來執行管理要求。

>[!CAUTION]
>
>此處記錄的細節僅限於Adobe Experience Manager as a Cloud Service。
>
>來自其他Adobe按需服務的資料以及任何相關的隱私請求將要求對該服務採取操作。
>
>有關詳細資訊，請參閱 [Adobe隱私中心](https://www.adobe.com/privacy.html)。

## 簡介 {#introduction}

Adobe Experience Manager as a Cloud Service的實例以及運行在它們上的應用程式由我們的客戶擁有和操作。

因此，資料保護法規（如GDPR 、 CCPA和其他法規）在很大程度上是客戶的責任。

作為一個非常簡要的介紹，資料隱私和保護法規包括了新的規則，應遵循以下角色：

* 業務實體(CCPA)和/或資料控制器(GDPR)

* 服務提供商(CCPA)和/或資料處理器(GDPR)

這些條例的主要規定是：

1. 擴展了個人資料定義，包括所有唯一ID;直接和間接可識別的資料。

2. 加強同意要求。

3. 更多地關注刪除權限（資料擦除）。

4. 退出資料銷售。

Adobe Experience Manager as a Cloud Service:

* 這些實例和在它們上運行的應用程式由客戶擁有和操作。

   * 這有效地意味著客戶管理法規角色，包括業務實體和服務提供商、資料控制器和資料處理器等。

   * 如下圖所示，Adobe Experience Platform Privacy Service將不AEM是工作流的一部分。

* 包AEM括客戶隱私管理員和/或管理員執AEM行隱私法規請求的文檔和過程；手動或通過API（如果可用）。

* 未添加新服務或UI。

   * 相反，將記錄過程和API，供處理隱私管理請求的客戶UI/門戶使用。

* 不AEM會包括任何現成工具來支援隱私請求工作流。

   * Adobe將為客戶的隱私管理員和/或管理員提供文檔和過程AEM，使他們能夠手動執行與隱私法規相關的請求。

Adobe正在提供處理與Adobe Experience Manager as a Cloud Service訪問、刪除和退出相關的隱私請求的程式。 在某些情況下，可以從客戶開發的門戶或指令碼中調用可用的API，以幫助實現自動化。

下圖說明隱私請求工作流可能的樣子(使用Adobe Experience Manager6.5說明):

![資料保護和隱私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as a Cloud Service和法規就緒性 {#aem-as-a-cloud-service-and-regulatory-readiness}

有關as a Cloud Service產品區的法規文檔，請參閱以下AEM各節。

## Adobe Experience Manager as a Cloud Service 基礎 {#aem-foundation}

請參閱 [資料AEM保護和資料隱私法規的基礎準備](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)。

## Adobe Experience Manager as a Cloud Service Sites {#aem-sites}

請參閱 [AEM Sites準備好實施資料保護和資料隱私法規。](/help/compliance/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager as a Cloud Service與Adobe Target和Adobe Analytics的整合 {#aem-integration-with-adobe-target-adobe-analytics}

Adobe Experience Manager as a Cloud Service的這些整合與資料保護和隱私（如GDPR）就緒服務相結合。 與整合相關的Adobe Target或Adobe AnalyticsAEM的個人資料未儲存。
有關詳細資訊，請參閱：

* [Adobe Target — 隱私概述](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics資料隱私工作流](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)

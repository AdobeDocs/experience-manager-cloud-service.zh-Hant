---
title: Adobe Experience Manager as a Cloud Service的HIPAA整備
description: 瞭解對HIPAA法規的Experience Manager as a Cloud Service支援，以及實作新的AEM as a Cloud Service專案時如何遵守。
feature: Compliance
role: Admin, Architect, Developer, Leader
source-git-commit: 49721ac71bc2bde10eb5f25db58ee1b07c8a82e5
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 6%

---

# Adobe Experience Manager as a Cloud Service的HIPAA整備 {#hipaa-readiness-for-adobe-experience-manager-as-a-cloud-service}

>[!WARNING]
>
>本文件的內容並不構成法律建議，其宗旨並非取代專業的法律建議。
>
>請諮詢貴公司的法律部門，以獲取有關HIPAA法規的建議。

>[!NOTE]
>
>如需有關Adobe對隱私權問題的回應以及這對於您身為Adobe客戶所代表之意義的詳細資訊，請參閱：
>
>* Adobe信任中心中的[HIPAA與Adobe產品和服務](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html)
>* [Adobe隱私中心](https://www.adobe.com/tw/privacy.html)

針對Adobe Experience Manager (AEM) as a Cloud Service，Adobe提供檔案協助您瞭解HIPAA整備程度。 它可以協助您符合這些法規。

## 健康保險便利與責任法案(HIPAA) {#health-insurance-portability-and-accountability-act-hipaa}

### 健康保險便利與責任法案(HIPAA) {#the-health-insurance-portability-and-accountability-act-hipaa}

HIPAA隱私權、安全性及違反通知規則為個人可識別的健康資訊(稱為受保護的健康資訊(PHI))建立重要保護。

根據HIPAA，受保實體是醫療保健提供者、健康計畫或醫療保健資訊中心。 商業夥伴是為涉及存取PHI之涵蓋實體提供服務的實體。 HIPAA隱私權與安全規則要求受保實體以商業夥伴協定(BAA)的形式向商業夥伴取得書面保證，該協定要求商業夥伴保障受保實體PHI的隱私權與安全性。

### 提供PHI給Adobe {#providing-phi-to-adobe}

Adobe充當其HIPAA就緒服務的Business Associate，列於AEM as a Cloud Service中的[HIPAA就緒服務](#hipaa-readiness-of-services-in-aem-as-a-cloud-service)下。

授權任何Adobe HIPAA就緒服務以處理PHI **的客戶必須**&#x200B;擁有正確的授權和與Adobe簽署的授權BAA。

>[!IMPORTANT]
>
>客戶不得透過Adobe產品和服務建立、接收、維護或傳輸PHI，這些產品和服務未指定為HIPAA就緒服務，或沒有適當的授權可使用HIPAA就緒服務。

### HIPAA共用責任 {#hipaa-shared-responsibilities}

Adobe HIPAA就緒服務仰賴共擔責任安全模式，要求客戶和Adobe各自承擔維護PHI安全性的不同責任。 在此共用安全性模式下，Adobe依賴客戶使用和設定符合HIPAA的HIPAA就緒服務。

如需針對符合HIPAA要求的服務執行Adobe BAA的詳細資訊，請聯絡您的Adobe銷售代表或客戶成功經理。

>[!IMPORTANT]
>
>**免責宣告**：
>
>客戶有責任使用Adobe HIPAA就緒服務，以及確保Adobe HIPAA就緒服務符合其合規性要求。

如需詳細資訊，請參閱Adobe信任中心中的[HIPAA與Adobe產品和服務](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html)。

## HIPAA術語 {#hipaa-terminology}

下表說明如何分類AEM服務以符合HIPAA使用情形。

| HIPAA整備程度 | 說明 |
| --- | --- |
| HIPAA就緒 | 設計可在適當設定並搭配BAA使用時處理PHI。 |
| 不符合HIPAA標準 | 並非為處理PHI而設計，且不得用於HIPAA相關使用案例。 |

>[!NOTE]
>
>HIPAA整備程度分類是以每項服務的預期功能為基礎，並可能會隨著時間而改變。
>
>客戶在規劃HIPAA相關部署時，應參考最新的檔案和適用的合約條款。

## AEM as a Cloud Service中的HIPAA服務整備 {#hipaa-readiness-of-services-in-aem-as-a-cloud-service}

下表說明哪些AEM服務可使用HIPAA，以及哪些服務可與其搭配使用。 符合HIPAA要求的服務需要購買醫療保健延伸保全，如[其他需求](#additional-requirements)中所述。

| 產品/功能 | 服務 | HIPAA整備程度 |
| --- | --- | --- |
| AEM Sites | AEM Sites， AEM Publish， Edge Delivery Services | HIPAA就緒 |
| AEM Sites | 通用編輯器 | 未匯入PHI時，無法將HIPAA就緒<br>[1]新增至延伸安全性程式。 |
| AEM Sites Optimizer | Sites Optimizer | 未匯入PHI時，無法將HIPAA就緒<br>[1]新增至延伸安全性程式。 |
| AEM Assets | AEM Assets | HIPAA就緒 |
| AEM Assets | Content Hub | 未匯入PHI時，無法將HIPAA就緒<br>[1]新增至延伸安全性程式。 |
| AEM Assets | Brand Portal | 不符合HIPAA標準 |
| AEM Assets | 動態媒體OpenAPI | 未匯入PHI時，無法將HIPAA就緒<br>[1]新增至延伸安全性程式。 |
| AEM Assets | Dynamic Media Scene 7 | 不符合HIPAA標準 |
| AEM Forms | AEM Forms、Authentication Facade服務、PDF公用程式服務 | HIPAA就緒 |
| AEM CIF | Commerce Integration Framework | 不符合HIPAA標準 |
| AEM Cloud Manager | AEM Cloud Manager，發行協調器，發行切換，發行驗證器 | HIPAA就緒 |
| AEM Cloud Manager | 軟體散發 | 未匯入PHI時，無法將HIPAA就緒<br>[1]新增至延伸安全性程式。 |
|   |   |   |
| AEM Guides  | AEM Guides  | 不符合HIPAA標準 |
|   |   |   |
| LLM Optimizer | LLM Optimizer | 未匯入PHI時，無法將HIPAA就緒<br>[1]新增至延伸安全性程式。 |

>[!NOTE]
>
>[1]
>
>對於標示為可以新增至延伸安全性計畫的不符合HIPAA要求的服務，客戶必須確保PHI不會路由至這些服務或儲存在這些服務中。
>
>將PHI引進不符合HIPAA的服務中可能會導致不合規的情況。

### 其他需求 {#additional-requirements}

[列為HIPAA就緒的服務](#hipaa-readiness-of-services-in-aem-as-a-cloud-service)需要購買醫療保健延伸安全性。

購買Healthcare專用的Extended Security時，需要：

* 為該計畫選取的產品已可使用HIPAA （如表格中所列），
* 已針對&#x200B;*每個*&#x200B;產品購買醫療保健專用延伸安全性；這可確保足夠的Cloud Manager積分、
* 適用於醫療保健的延伸安全性在方案建立時套用。

如果符合需求，Extended Security for Healthcare可在建立AEM程式時套用；如需詳細資訊，請參閱[設定](#setup)。

>[!NOTE]
>
>如需布建和定價的詳細資訊，請洽詢您的銷售代表。

## 環境 {#environments}

*HIPAA就緒*&#x200B;不適用於RDE （快速開發環境）、開發或中繼環境，因為這些環境不允許使用PHI。

這表示您必須：

* 將虛擬資料用於開發和測試目的
* 僅處理來自生產環境的PHI

下表顯示環境型別可在何處支援為HIPAA就緒。

| | RDE | 開發 | 階段  | Prod |
| --- | --- | --- | --- | --- |
| 環境型別  | 否  | 否  | 否  | 是  |

## 設定 {#setup}

當您[建立生產程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)時，[安全性索引標籤會提供啟用HIPAA保護](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)的選項。
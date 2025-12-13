---
title: 如何將資料庫連線至 [!DNL AEM Forms] as a Cloud Service？
description: 從調適型表單或AEM工作流程擷取資料並儲存至RESTful Web服務、SOAP型Web服務及OData服務。
feature: Adaptive Forms, Form Data Model
role: Admin, User
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---

# 將AEM Forms連線至資料庫 {#aem-forms-data-integration}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/data-integration.html) |
| AEM as a Cloud Service  | 本文章 |



![資料整合](do-not-localize/data-integeration.png)

企業基礎架構包括不同的後端系統或資料來源，例如資料庫、網站服務、REST服務、OData服務和CRM解決方案。 他們共同組成資訊系統，為企業應用程式提供資料，以執行日常業務。 另一方面，應用程式會擷取資料，並將資料傳回更新資料來源。

將Adaptive Form連線至資料庫時，需要與資料來源整合，才能在呈現表單時擷取客戶資料。 在某些情況下，系統會根據最適化Forms中的使用者輸入從資料來源擷取資料。 此外，當您傳送最適化表單至資料庫時，提交的最適化表單資料可以寫回以更新各自的資料來源。

雖然分散式的模組化系統有其優點，但難題在於跨資料來源整合及建立資料關聯。 資料整合是功能強大且有效率的企業基礎建設的關鍵所在，因為不同的資料來源會連線至應用程式，以交換商務資料。

## 資料整合概述 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms]資料整合允許設定不同的資料來源並與[!DNL AEM Forms]連線。 它提供直覺式使用者介面，可跨連線的資料來源建立商業實體和服務的統一資料呈現結構描述。 此統一表示法稱為表單資料模型(FDM)，是JSON結構描述的延伸。 表單資料模型(FDM)中的實體稱為資料模型物件。 表單資料模型(FDM)可讓您：

* 從連線的資料來源存取資料模型物件、屬性和服務。
* 建立自訂資料模型物件和屬性
* 在資料來源內和跨資料來源建立資料模型物件之間的關聯。
* 啟動資料模型物件服務，以查詢或寫入資料來源中的資料，以及從資料來源寫入資料。

建立表單資料模型(FDM)後，您就可以用它來：

* 根據表單資料模型(FDM)建立最適化Forms
* 從已設定的資料來源預先填入最適化Forms
* 使用最適化表單規則叫用資料來源服務/作業
* 將提交的最適化表單資料寫入資料來源

## 適用性和使用案例

### 保險

## AEM Forms是否可用於保單應用程式？

可以。AEM Forms可用來建立數位保險申請表單，以收集申請人資訊、驗證輸入內容，並與後端承保系統整合。

## AEM Forms是否支援包銷工作流程？

是，且具有工作流程與整合。 AEM Forms支援工作流程導向的流程和後端整合，好讓應用程式資料可流入承保和決策系統。

## AEM Forms可以與保險核心系統整合嗎？

可以。AEM Forms支援使用REST和SOAP API進行整合，使其能夠與原則管理系統、宣告管理系統和CRM連線。

## AEM Forms可以將表單資料寫回保險系統嗎？

可以。AEM Forms支援將資料回寫至後端系統，做為表單提交和工作流程執行的一部分。

## 開始使用資料整合 {#get-started-with-data-integration}

實施資料整合以將最適化表單傳送到資料庫的第一個步驟是，識別並設定資料來源，該資料來源儲存您要用於最適化Forms中的資訊。 接下來，您會建立表單資料模型(FDM)，此模型會使用一或多個資料來源的資料模型物件、屬性及服務。 您可以根據表單資料模型(FDM)建立最適化Forms，其中最適化表單欄位會繫結至各自的資料來源屬性。

[!DNL AEM Forms]也可讓您建立與資料來源無關的表單資料模型(FDM)，並在稍後將表單資料模型(FDM)中的資料模型物件和屬性與資料來源建立關聯或繫結。 它可消除您在處理表單資料模型(FDM)時對資料來源的任何依賴性。

檢閱下列內容以開始、瞭解並實作資料整合：

* [設定資料來源](configure-data-sources.md)
* [建立表單資料模型(FDM)](create-form-data-models.md)
* [使用表單資料模型(FDM)](work-with-form-data-model.md)
* [使用表單資料模型(FDM)](using-form-data-model.md)

<!--

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] does not support relational database.

-->
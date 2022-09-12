---
title: 如何將資料庫連接到 [!DNL AEM Forms] as a Cloud Service?
seo-title: AEM Forms Data Integration
description: 您可以從中檢索資料並保存到RESTful Web服務、基於SOAP的Web服務和OData服務 [!DNL AEM Forms] as a Cloud Service。 此服務提供專用工具，可擷取、測試、驗證資料，以及將資料傳送至各種類型的資料來源。
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# 將資料來源連線到 Cloud Service {#aem-forms-data-integration}

![資料整合](do-not-localize/data-integeration.png)

企業基礎架構包括不同的後端系統或資料源，如資料庫、Web服務、REST服務、 OData服務和CRM解決方案。 綜上所述，他們建立了一個資訊系統，該系統將資料提供給企業應用程式，以執行日常業務。 另一方面，應用程式會擷取資料，並傳回以更新資料來源。

[!DNL AEM Forms] 適用性Forms和互動式通訊等應用程式需要與資料來源整合，以便在演算表單和建立互動式通訊時擷取客戶資料。 根據適用性Forms中的使用者輸入，從資料來源擷取資料時，有時會使用案例。 此外，可將提交的最適化表單資料回寫，以更新個別資料來源。

雖然分散的模組化系統有其自身的優點，但挑戰在於整合和建立資料源之間的資料關聯。 資料整合是功能高效的企業基礎架構的關鍵，該基礎架構具有與應用程式連接的不同資料源，用於交換業務資料。

## 資料整合概觀 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] 資料整合可讓您透過 [!DNL AEM Forms]. 它提供直觀的用戶介面，以建立跨連接資料源的業務實體和服務的統一資料表示架構。 統一的表示法稱為表單資料模型，此為JSON結構描述的擴充功能。 「表單資料模型」中的圖元稱為資料模型對象。 表單資料模型可讓您：

* 從連接的資料源訪問資料模型對象、屬性和服務。
* 建立自訂資料模型物件和屬性
* 在資料來源內和跨資料來源建立資料模型物件之間的關聯。
* 調用資料模型對象服務，以查詢資料源或從資料源中寫入資料。

建立表單資料模型後，您就可以在各種最適化表單和互動式通訊工作流程中使用該模型，例如：

* 根據表單資料模型建立最適化Forms和互動式通訊
* 預填適用性Forms和來自已設定資料來源的互動式通訊
* 使用適用性表單規則叫用資料來源服務/操作
* 將提交的適用性表單資料寫入資料來源

## 開始使用資料整合 {#get-started-with-data-integration}

實作資料整合的第一步，是識別並設定資料來源，以儲存您要在適用性Forms和互動式通訊使用案例中運用的資訊。 接下來，您將建立一個表單資料模型，該模型使用來自一個或多個資料源的資料模型對象、屬性和服務。 您可以根據表單資料模型建立最適化Forms和互動式通訊，互動式通訊中的最適化表單欄位或預留位置會系結至個別的資料來源屬性。

[!DNL AEM Forms] 也可讓您建立與資料來源無關的表單資料模型，並稍後將表單資料模型中的資料模型物件和屬性與資料來源關聯或系結。 在處理表單資料模型時，可消除對資料來源的任何相依性。

請檢閱下列項目，以開始、了解及實作資料整合。

* [設定資料來源](configure-data-sources.md)
* [建立表單資料模型](create-form-data-models.md)
* [使用表單資料模型](work-with-form-data-model.md)
* [使用表單資料模型](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] 不支援關係資料庫。

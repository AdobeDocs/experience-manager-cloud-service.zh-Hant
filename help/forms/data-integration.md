---
title: '如何將資料庫連接到 [!DNL AEM Forms] as a Cloud Service? '
seo-title: AEM Forms Data Integration
description: 可以從中檢索資料並將資料保存到REST風格的Web服務、基於SOAP的Web服務和OData服務 [!DNL AEM Forms] as a Cloud Service。 該服務提供了專用工具，用於檢索、test、驗證和將資料發送到各種類型的資料源。
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# 將資料來源連線到 Cloud Service {#aem-forms-data-integration}

![資料整合](do-not-localize/data-integeration.png)

企業基礎架構包括不同的後端系統或資料源，如資料庫、 Web服務、 REST服務、 OData服務和CRM解決方案。 綜上所述，他們建立了一個為企業應用程式提供資料以執行日常業務的資訊系統。 另一方面，應用程式會捕獲資料並將其發送回更新資料源。

[!DNL AEM Forms] 像自適應Forms和互動式通信這樣的應用程式需要與資料源整合以在呈現表單和建立互動式通信的同時獲取客戶資料。 在自適應Forms中，當根據用戶輸入從資料源獲取資料時，有使用情形。 此外，可以回寫已提交的Adaptive Form資料以更新各自的資料源。

雖然分佈式模組化系統有其自身的優點，但挑戰在於跨資料源整合和建立資料關聯。 資料整合是功能強大、高效的企業基礎架構的關鍵，該基礎架構的不同資料源連接到用於交換業務資料的應用程式。

## 資料整合概述 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] 資料整合允許配置和連接不同的資料源 [!DNL AEM Forms]。 它提供了直觀的用戶介面，以建立跨連接資料源的業務實體和服務的統一資料表示模式。 統一表示稱為表單資料模型，是JSON架構的擴展。 表單資料模型中的圖元稱為資料模型對象。 表單資料模型允許您：

* 從連接的資料源訪問資料模型對象、屬性和服務。
* 建立自定義資料模型對象和屬性
* 在資料源內和資料源之間建立資料模型對象之間的關聯。
* 調用資料模型對象服務以查詢資料源或將資料從資料源寫入資料。

建立表單資料模型後，可以在各種自適應表單和互動式通信工作流中使用它，例如：

* 基於表單資料模型建立自適應Forms和互動式通信
* 預填充自適應Forms和配置資料源的互動式通信
* 使用自適應表單規則調用資料源服務/操作
* 將提交的Adaptive Form資料寫入資料源

## 資料整合入門 {#get-started-with-data-integration}

實施資料整合的第一步是確定和配置資料源，這些資料源儲存您要在自適應Forms和互動式通信使用情形中利用的資訊。 接下來，您將建立一個使用一個或多個資料源中的資料模型對象、屬性和服務的表單資料模型。 您可以基於表單資料模型建立自適應Forms和互動式通信，其中互動式通信中的自適應表單欄位或佔位符綁定到各自的資料源屬性。

[!DNL AEM Forms] 還允許您建立與資料源無關的表單資料模型，並稍後將表單資料模型中的資料模型對象和屬性與資料源關聯或綁定。 它消除了在處理表單資料模型時對資料源的任何依賴。

查看以下內容以開始、瞭解和實施資料整合。

* [設定資料來源](configure-data-sources.md)
* [建立表單資料模型](create-form-data-models.md)
* [使用表單資料模型](work-with-form-data-model.md)
* [使用表單資料模型](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] 不支援關係資料庫。

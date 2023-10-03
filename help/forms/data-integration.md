---
title: 如何將資料庫連線至 [!DNL AEM Forms] as a Cloud Service？
description: 從調適型表單或AEM工作流程擷取資料並儲存至RESTful Web服務、以SOAP為基礎的Web服務和OData服務。
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: defeee2fee42c6274c71438d6f9fde6e49a05081
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---

# 將AEM Forms連線至資料庫 {#aem-forms-data-integration}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/data-integration.html) |
| AEM as a Cloud Service  | 本文章 |


![資料整合](do-not-localize/data-integeration.png)

企業基礎架構包括不同的後端系統或資料來源，例如資料庫、網站服務、REST服務、OData服務和CRM解決方案。 他們共同組成資訊系統，為企業應用程式提供資料，以執行日常業務。 另一方面，應用程式會擷取資料，並將資料傳回更新資料來源。

[!DNL AEM Forms] 最適化Forms和互動式通訊等應用程式需要與資料來源整合，以便在呈現表單和建立互動式通訊時擷取客戶資料。 在某些情況下，系統會根據最適化Forms中的使用者輸入從資料來源擷取資料。 此外，提交的最適化表單資料可以寫回以更新各自的資料來源。

雖然分散式的模組化系統有其優點，但難題在於跨資料來源整合及建立資料關聯。 資料整合是功能強大且有效率的企業基礎建設的關鍵所在，因為不同的資料來源會連線至應用程式，以交換商務資料。

## 資料整合概述 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] 資料整合可讓您設定並連線不同的資料來源，使用 [!DNL AEM Forms]. 它提供直覺式使用者介面，可跨連線的資料來源建立商業實體和服務的統一資料呈現結構描述。 統一表示法稱為表單資料模型，是JSON結構描述的延伸。 表單資料模型中的圖元稱為資料模型物件。 表單資料模型可讓您：

* 從連線的資料來源存取資料模型物件、屬性和服務。
* 建立自訂資料模型物件和屬性
* 在資料來源內和跨資料來源建立資料模型物件之間的關聯。
* 啟動資料模型物件服務，以查詢或寫入資料來源中的資料，以及從資料來源寫入資料。

建立表單資料模型後，您就可以在各種最適化表單和互動式通訊工作流程中加以使用，例如：

* 根據表單資料模型建立最適化Forms和互動式通訊
* 從已設定的資料來源預先填入最適化Forms和互動式通訊
* 使用最適化表單規則叫用資料來源服務/作業
* 將提交的最適化表單資料寫入資料來源

## 開始使用資料整合 {#get-started-with-data-integration}

實作資料整合的第一步是識別並設定資料來源，以儲存您要在最適化Forms和互動式通訊使用案例中使用的資訊。 接著，您建立表單資料模型，此模型會使用一或多個資料來源的資料模型物件、屬性和服務。 您可以根據表單資料模型建立最適化Forms和互動式通訊，其中互動式通訊中的最適化表單欄位或預留位置會繫結至各自的資料來源屬性。

[!DNL AEM Forms] 也可讓您建立與資料來源無關的表單資料模型，並在稍後將表單資料模型中的資料模型物件和屬性與資料來源建立關聯或繫結。 當您處理表單資料模型時，它可消除對資料來源的任何相依性。

檢閱下列內容以開始、瞭解並實作資料整合。

* [設定資料來源](configure-data-sources.md)
* [建立表單資料模型](create-form-data-models.md)
* [使用表單資料模型](work-with-form-data-model.md)
* [使用表單資料模型](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] 不支援關聯式資料庫。

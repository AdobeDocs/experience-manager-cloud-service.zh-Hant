---
title: 將可重複區段新增到表單
description: 新增可重複區段至 EDS Form
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 100%

---

# 將可重複區段新增到表單

最適化表單區塊提供新增表單區段或元件的功能，或是使表單區段或元件成為可重複的功能。這允許使用者針對同一類型的數據多次輸入訊息，從而更容易收集工作經驗或教育背景等資訊。

例如，考慮一個用來收集有關個人工作經驗資訊的表單。您可能有一個可重複區段，用來擷取每項先前工作的詳細資訊。可重複區段通常包含公司名稱、職位、就業日期和工作職責等欄位。使用者可以新增可重複區段的多個實例，以輸入有關他們所做每項工作的資訊。

閱讀完本文章後，您將學會：

- [在表單中建立可重複區段](#add-repeatable-sections-to-a-form)
- [設定表單中的最小或最大重複次數](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## 新增可重複區段
        

在表單中建立可重複區段，可讓使用者輸入同一資料集的多個實例，進而有效收集重複資訊。若要在表單中建立可重複區段：

1. 前往 Microsoft SharePoint 或 Google Workspace 的 Edge Deliver 專案資料夾，並開啟您的試算表。

1. 新增一個表單欄位，且`type`屬性設定為`fieldset`
1. 指定欄位的`Name`。名稱屬性是用來建立可重複區段。
1. 透過將`repeatable`設為 `true` 來啟用重複性。
1. 指定欄位的描述性`label`，用作可重複區段的標題。

   請參考以下影像，以了解工作申請表中工作經驗區段的實例。

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. 關於您想要含在該區段中的每個欄位，請將其`Fieldset`屬性設為與您在步驟 3 中所選的相同名稱。

   例如，在所有相關欄位的欄位集屬性內，指定將`experience`列入`employment history`區段中。

   ![可重複區段欄位及其屬性的範例](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。將可重複區段新增至表單。

   在可重複區段下方，使用者可以找到直覺式的「**新增**」按鈕，可方便使用者輕鬆新增多個區段。

   ![可重複區段、新增按鈕，用來新增多個區段 ](/help/edge/assets/repeatable-section-example.png)


## 設定最小和最大重複次數

在表單設計中，為可重複區段設定最小和最大重複次數很有用。這樣做可以在有效引導使用者的同時建立控制和一致性。若要設定最小或最大重複次數：

1. 前往 Microsoft SharePoint 或 Google Workspace 的 Edge Deliver 專案資料夾，並開啟您的試算表。

1. 關於`type` `fieldset`的一個欄位，以及將`repeatable`屬性設定為 `true`：

   - 設定`min`屬性來指定該區段可以重複的最小次數。

   - 設定`max`屬性來指定該區段可以重複的最大次數。

   ![設定最小和最大屬性來指定該區段可以重複的次數](/help/edge/assets/repeatable-section-set-min-max.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

   在新增可重複區段時，使用者可以找到直覺式「**刪除**」圖示，讓使用者更容易刪除可重複區段。新增以後，這些區段就不能減少至少於`min`屬性指定的實例。這可確保遵守為填寫表單而設定的最低要求。



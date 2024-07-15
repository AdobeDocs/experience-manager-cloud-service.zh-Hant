---
title: 將可重複區段新增到表單
description: 新增可重複區段至 EDS Form
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 100%

---

# 將可重複區段新增到表單

最適化表單區塊提供新增表單區段或元件的功能，或是使表單區段或元件成為可重複的功能。這允許使用者針對同一類型的數據多次輸入訊息，從而更容易收集工作經驗或教育背景等資訊。

例如，考慮一個用來收集有關個人工作經驗資訊的表單。您可能有一個可重複區段，用來擷取每項先前工作的詳細資訊。可重複區段通常包含公司名稱、職位、就業日期和工作職責等欄位。使用者可以新增可重複區段的多個實例，以輸入有關他們所做每項工作的資訊。

閱讀完本文章後，您將學會：

* [在表單中建立可重複區段](#add-repeatable-sections-to-a-form)
* [設定表單中的最小或最大重複次數](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

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

   * 設定`min`屬性來指定該區段可以重複的最小次數。

   * 設定`max`屬性來指定該區段可以重複的最大次數。

   ![設定最小和最大屬性來指定該區段可以重複的次數](/help/edge/assets/repeatable-section-set-min-max.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

   在新增可重複區段時，使用者可以找到直覺式「**刪除**」圖示，讓使用者更容易刪除可重複區段。新增以後，這些區段就不能減少至少於`min`屬性指定的實例。這可確保遵守為填寫表單而設定的最低要求。

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Forms Block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Services project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-SharePoint)._" 


To add repeatable sections in Edge Delivery:

1. [Author a form using Microsoft Excel](#author-form)
2. [Preview and publish the form](#preview-form)

### Author a form using Microsoft Excel {#author-form}

1. Go to your Edge Deliver project folder on Microsoft SharePoint or Google Workspace and open your spreadsheet. For example, open an a spreadsheet named `loan-application.xlsx`.

1. Add a new columns labeled `Repeatable` to the sheet contaning your form fields. By default, the `shared-default` sheet contains the form fields.  

1. Add new columns labeled as `Repeatable`, `Min`, and `Max` in your Microsoft Excel file.
1. Specify the value for the `Repeatable` column as `True` for the fieldset that you want to make repeatable.
1. Specify the values for the `Min` and `Max` columns. The `Min` value represents the minimum number of occurrences for which the panel repeats, while the `Max` value represents the maximum number of occurrences for which the panel repeats.
1. Save your Microsoft Excel file.
     
>[!NOTE]
>
> Here is the [Loan application](/help/forms/assets/loan-application.xlsx) excel sheet for your reference. 

### Preview/Publish the form using your Edge Delivery Service

1. Open or create new document file in a Microsft SharePoint Site to embed the Excel sheet  in it using a `Form Block`. For example, open the `index` file and add a `Form Block`.
2. Open the command prompt, navigate to your AEM Edge Delivery project directory on your local machine, and execute the command as `aem up`.

The form is accessible at `https://localhost:3000`, where clicking the `Add` button adds new repeatable section for entering co-applicant details. You can also delete the the repeatable section by clicking the `Delete` button. 

>[!NOTE]
>
> If you encounter a "Page Not Found" error while accessing your form at localhost, add the directory name of the Microsoft SharePoint Site in front of the URL where your form is located. For example, `http://localhost:3000/<dir-name>/`

-->


## 另請參閱

{{see-more-forms-eds}}

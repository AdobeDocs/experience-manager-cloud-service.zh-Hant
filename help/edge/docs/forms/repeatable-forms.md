---
title: 將可重複區段新增至表單
description: 新增可重複區段至 EDS Form
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 8%

---

# 將可重複區段新增至表單

最適化表單區塊提供新增或讓表單的區段或元件可重複的功能。 這可讓使用者為相同型別的資料輸入多次資訊，更輕鬆地收集工作經驗或教育背景等資訊。

例如，考慮用來收集個人工作體驗相關資訊的表單。 您可以有可重複的區段來擷取先前各工作的詳細資訊。 重複區段通常包含公司名稱、職稱、僱用日期和工作責任等欄位。 使用者可以新增多個可重複區段的執行個體，以輸入有關他們從事的每一個工作的資訊。



到本文結束時，您將瞭解：

* [在表單中建立可重複的區段](#add-repeatable-sections-to-a-form)
* [設定表單中最小或最大重複次數](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## 建立可重複的區段

在表單中建立可重複的區段，讓使用者能夠輸入同一組資料的多個例項，進而有效率地收集重複資訊。 若要在表單中建立可重複的區段：

1. 前往Microsoft SharePoint或Google Workspace上的Edge Deliver專案資料夾，並開啟試算表。

1. 使用新增表單欄位 `type` 屬性設定為 `fieldset`
1. 指定 `Name` 欄位的。 name屬性用於建立可重複的區段。
1. 透過設定啟用重複性 `repeatable` 至 `true`.
1. 指定描述性 `label` 欄位的。 它用作可重複區段的標題。

   請參閱下圖，以取得工作申請表單中僱用歷史記錄區段的圖例。

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. 針對您想納入區段中的每個欄位，設定其 `Fieldset` 屬性的名稱與您在步驟3中選擇的名稱相同。

   例如，指定 `experience` Fieldset屬性中納入的所有相關欄位 `employment history` 區段。

   ![重複區段欄位及其屬性的範例](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 以預覽和發佈工作表。 可重複區段會新增至表單。

   在可重複區段底下，使用者會找到直覺式的 **新增** 按鈕，方便您輕鬆新增多個區段。

   ![重複區段，「新增」按鈕，可新增多個區段 ](/help/edge/assets/repeatable-section-example.png)


## 設定最小重複次數和最大重複次數

在表單設計中，為可重複區段設定最小和最大重複次數會很有幫助。 如此一來，您就能夠建立控制並維持一致性，同時有效地引導使用者。 若要設定最小或最大重複次數：

1. 前往Microsoft SharePoint或Google Workspace上的Edge Deliver專案資料夾，並開啟試算表。

1. 針對欄位 `type` `fieldset` 和 `repeatable` 屬性設定為 `true`：

   * 設定 `min` 屬性來指定可重複該區段的最小次數。

   * 設定 `max` 屬性來指定可重複該區段的最大次數。

   ![設定min和max屬性，指定可重複區段的次數](/help/edge/assets/repeatable-section-set-min-max.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 預覽和發佈試算表。

   新增可重複區段時，使用者會發現 **刪除** 圖示，可讓您更輕鬆地移除重複區段。 新增後，這些區段無法減少到比指定的執行個體更少。 `min` 屬性。 這可確保遵守為表單完成設定的最低要求。

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Form block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Services project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-sharepoint)._" 


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


## 了解更多

* [建立並預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單來傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈到網站頁面](/help/edge/docs/forms/publish-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [改變主題和樣式風格](/help/edge/docs/forms/style-theme-forms.md)
* [表單元件及其屬性](/help/edge/docs/forms/form-components.md)

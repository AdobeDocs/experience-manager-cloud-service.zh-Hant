---
title: 針對AEM Formsas a Cloud Service使用reCAPTCHA與Edge Delivery Services
description: 使用 EDS Form 中的 Google reCAPTCHA
feature: Edge Delivery Services
exl-id: ac104e23-f175-435f-8414-19847efa5825
source-git-commit: 8730383d26c6f4fbe31a25a43d33bf314251d267
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 87%

---


# 針對AEM Formsas a Cloud Service使用reCAPTCHA與Edge Delivery Services

reCAPTCHA 是一種受歡迎的工具，用來保護網站免遭詐騙活動、垃圾郵件和濫用。在 Edge Delivery Services 中，最適化表單區塊有新增 Google reCAPTCHA 的功能，可區分人類和機器人。此功能可讓使用者保護其網站免遭垃圾郵件和濫用。
例如，考慮一個收集資料的查詢表單，例如開始和結束旅行日期、房間預算、預估旅行成本和旅行者資訊。在這種情況下，惡意使用者可能會利用該表單來發送網路釣魚電子郵件，或使用垃圾郵件機器人將不相關或有害內容填滿表單。整合 reCAPTCHA 可驗證提交內容是否來自真實使用者，以此提供更高的安全性並有效地減少垃圾郵件。

Edge Delivery Services 僅支援最適化表單區塊的&#x200B;**分數型 (v3)-reCAPTCHA** 。

![Recaptcha V2](/help/forms/assets/recaptcha-v2-invisible.png)

**reCAPTCHA** 功能屬於預先發佈計畫。若要求存取 AEM Forms Edge Delivery Services 的  **reCAPTCHA**  功能，請從您的工作地址發送電子郵件至 mailto:aem-forms-ea@adobe.com。

<!--
By the end of this article, you learn to:
  * [Enable Google reCAPTCHA's for a single form](#enable-google-recaptchas-for-a-single-form)
  * [Enable reCAPTCHA for all the forms on your Site](#enable-recaptcha-for-all-the-forms)

## Pre-requisite

Register your domain with [Google reCAPTCHA and obtain credentials](https://www.google.com/recaptcha/admin/create).

## Enable Google reCAPTCHA's for a single form {#enable-google-recaptchas-for-a-single-form}

Enabling Google reCAPTCHA for a single form involves integrating Google's reCAPTCHA service into a specific web form to prevent automated abuse or spam submissions.

To enable Google reCAPTCHA's for a single form:
1. [Configure the reCAPTCHA secret key in project configuration file](#configure-secret-key)
1. [Add reCAPTCHA site key to your form](#add-site-key)


### Configure the reCAPTCHA secret key in project configuration file {#configure-secret-key}

The Site Secret for domain registered with Google reCAPTCHA is added to project the configuration file (`.helix/config`) in your AEM Project folder at Microsoft SharePoint or Google Drive. To add the Site Secret to the config file:

1. Go to your AEM Project folder on Microsoft® SharePoint or Google Drive. 
1. Create the `.helix/config.xlsx` file in your AEM Project folder in Microsoft SharePoint Site or the `.helix/config` file in AEM Project folder within your Google Drive. 

    >[!NOTE]
    >
    > The [project configuration file](https://www.aem.live/docs/configuration) is a spreadsheet located at `/.helix/config`. If the file does not exist, create it.

1. Open the `config` file and add the following key and value pairs:

    * **captcha.secret**: Google reCAPTCHA secret key value
    * **captcha.type**: reCAPTCHA v2
  
   Refer to the image for an illustration of a project configuration file:

    ![Project configuration file](/help/forms/assets/recaptcha-config-file.png)

    >[!NOTE]
    >
    >  You can retrieve the reCAPTCHA keys from the [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1.  Preview and publish the `config` file using [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content). 

### Add reCAPTCHA site key to your form {#add-site-key}

The Site Key for domain registered with Google reCAPTCHA is added to the spreadsheet of the form that is to be protected. To add the Site key to a form:

1. Go to your AEM Project folder on Microsoft® SharePoint or Google Drive and open your spreadsheet. You can also create new spreadsheet for a form.
1. Insert a row into the spreadsheet to add new field as CAPTCHA, including the following details:
    * **type**: captcha
    * **value**: Google reCAPTCHA site key value
  
    Refer to the illustration below, depicting the spreadsheet with the new row type as CAPTCHA:
  
   ![Recaptcha spreadsheet](/help/forms/assets/recaptcha-spreadsheet.png)

    >[!NOTE]
    >
    >  You can retrieve the reCAPTCHA keys from the [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) to preview and publish the sheet. 
You can refer to the [spreadsheet](/help/forms/assets/recaptcha-enquiry.xlsx) that includes the form definition for an enquiry form.

After adding new row in the form definition, a reCAPTCHA badge appears at the bottom-right corner of the form. This ensures that the form is now protected from fraudulent activities, spam, and misuse.

![recaptcha-form](/help/forms/assets/recaptcha-form.png)

Refer to the URL below, which showcases the live form with the reCAPTCHA badge:
https://main--wefinance--wkndforms.hlx.live/enquiry

## Enable reCAPTCHA for all the forms on your Site{#enable-recaptcha-for-all-the-forms}

To apply Google reCAPTCHA to all the forms on your Site that use Adaptive Forms Block, skip the previous steps and directly embed the `sitekey` value into the `recaptcha.js` file. To include site key value in the `recaptcha.js` file:

1. Open the corresponding GitHub repository on your local machine. 
1. Navigate to `../blocks/form/integrations/recaptcha.js` file.
1. Replace the `siteKey` with Google reCAPTCHA site key value.

    ![Recaptcha apply to all forms](/help/forms/assets/recaptcha-apply-to-all-forms.png)

    >[!NOTE]
    >
    >  You can retrieve the reCAPTCHA keys from the [Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin).

1. Use [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) to preview and publish the site. 

The reCAPTCHA badge starts appearing for all the forms on your Site. 
-->

## 另請參閱

{{see-more-forms-eds}}


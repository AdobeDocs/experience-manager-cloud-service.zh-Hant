---
title: 如何在AEM Forms中透過電子郵件傳送表單提交通知？
description: AEM Forms可讓您設定電子郵件提交動作，以在表單提交時傳送確認給使用者。
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# 透過電子郵件傳送表單提交通知 {#sending-a-form-submission-acknowledgement-via-email}

## 最適化表單資料提交 {#adaptive-form-data-submission}

最適化Forms提供數種現成的[提交動作](configuring-submit-actions.md)工作流程，用於將表單資料提交至不同的端點。

例如，**[!UICONTROL 傳送電子郵件]**&#x200B;提交動作會在成功提交最適化表單時傳送電子郵件。 您也可以將其設定為在電子郵件中傳送表單資料和PDF。

本文詳細說明在最適化表單及其提供的不同設定上啟用電子郵件動作的步驟。

>[!NOTE]
>
>您也可以使用&#x200B;**[!UICONTROL 透過電子郵件傳送PDF]**&#x200B;選項，以電子郵件傳送完成的表單作為PDF附件。 此動作可用的組態選項與&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;動作可用的選項相同。 電子郵件PDF動作僅適用於XFA型最適化Forms

## 傳送電子郵件動作 {#email-action}

「傳送電子郵件」動作可讓作者在成功提交最適化表單時，自動傳送電子郵件給一或多個收件者。

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, select **[!UICONTROL Form Container]** and select ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### 使用最適化表單欄位名稱來動態建立電子郵件內容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

調適型表單中的欄位名稱稱為預留位置，在使用者提交表單後會以該欄位的值取代。

在&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;動作中，您可以使用執行動作時所處理的預留位置。 這表示使用者提交表單時會產生電子郵件的標頭（例如&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL Subject]**）。

若要定義預留位置，請在選取&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;做為提交動作之後，在欄位中指定`${<field name>}`。

例如，如果表單包含名為`email_addr`的&#x200B;**[!UICONTROL 電子郵件地址]**&#x200B;欄位，用於擷取使用者的電子郵件識別碼，您可以在&#x200B;**[!UICONTROL 收件者]**、**[!UICONTROL 副本]**&#x200B;或&#x200B;**[!UICONTROL 密件副本]**&#x200B;欄位中指定下列專案。

`${email_addr}`

當使用者提交表單時，會傳送電子郵件給在表單的`email_addr`欄位中輸入的電子郵件識別碼。

>[!NOTE]
>
>您可以在欄位的&#x200B;**[!UICONTROL 編輯]**&#x200B;對話方塊中找到欄位名稱。

變數預留位置也可以在&#x200B;**[!UICONTROL 主旨]**&#x200B;和&#x200B;**[!UICONTROL 電子郵件範本]**&#x200B;欄位中使用。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重複面板中的欄位無法當作變數預留位置使用。


---
title: 通過電子郵件發送表單提交確認
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms允許您配置電子郵件提交操作，在提交表單時向用戶發送確認。
seo-description: AEM Forms allows you to configure the email Submit Action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# 通過電子郵件發送表單提交確認 {#sending-a-form-submission-acknowledgement-via-email}

## 自適應表單資料提交 {#adaptive-form-data-submission}

自適應Forms提供了幾種 [提交操作](configuring-submit-actions.md) 將表單資料提交到不同終結點的工作流。

例如， **[!UICONTROL 發送電子郵件]** 提交操作在成功提交自適應表單時發送電子郵件。 還可以配置它以發送電子郵件中的表單資料和PDF。

本文詳細介紹了在自適應表單上啟用電子郵件操作的步驟及其提供的不同配置。

>[!NOTE]
>
>您還可以使用 **[!UICONTROL 通過電子郵件發送PDF]** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。 此操作可用的配置選項與 **[!UICONTROL 發送電子郵件]** 操作。 「電子郵件PDF」操作僅適用於基於XFA的自適應Forms

## 發送電子郵件操作 {#email-action}

通過「發送電子郵件」操作，作者可以在成功提交自適應表單時自動向一個或多個收件人發送電子郵件。

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, tap **[!UICONTROL Form Container]** and tap ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an end user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### 使用「自適應表單」欄位名稱動態建立電子郵件內容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

自適應表單中的欄位名稱稱為佔位符，用戶提交表單後，這些佔位符將替換為該欄位的值。

在 **[!UICONTROL 發送電子郵件]** 操作中，可以使用執行操作時處理的佔位符。 它意味著電子郵件的標題(如 **[!UICONTROL 至]**。 **[!UICONTROL 抄送]**。 **[!UICONTROL 密件抄送]**。 **[!UICONTROL 主題]**)。

要定義佔位符，請指定 `${<field name>}` 在 **[!UICONTROL 發送電子郵件]** 作為「提交操作」。

例如，如果窗體包含 **[!UICONTROL 電子郵件地址]** 欄位，命名 `email_addr`，要捕獲用戶的電子郵件ID，可以在 **[!UICONTROL 至]**。 **[!UICONTROL 抄送]**&#x200B;或 **[!UICONTROL 密件抄送]** 的子菜單。

`${email_addr}`

當用戶提交表單時，會向在 `email_addr` 的子菜單。

>[!NOTE]
>
>您可以在 **[!UICONTROL 編輯]** 對話框。

變數佔位符也可用於 **[!UICONTROL 主題]** 和 **[!UICONTROL 電子郵件模板]** 的子菜單。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重複面板中的欄位不能用作變數佔位符。


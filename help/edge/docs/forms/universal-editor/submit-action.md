---
title: 提交動作
description: 設定最適化表單的提交動作。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: da2f673319dd5cec764408b4517698a9d39031bb
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 13%

---

# 最適化表單提交動作

提交動作會指定透過最適化表單收集之資料的目的地。 當使用者按一下表單上的&#x200B;**[!UICONTROL 提交]**&#x200B;按鈕時，提交程式就會開始。 AEM Forms提供下列兩種型別的提交動作，可讓您建立並使用自訂提交動作來符合您的特定需求。 現成可用的提交動作如下：

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

* [提交到 REST 端點](#rest-endpoint-submission-ue)
* [寄送電子郵件](#email-submission-ue)


### 提交到 REST 端點 {#rest-endpoint-submission-ue}

「提交至REST端點」動作用於將提交的表單資料傳送至指定的REST端點。 端點可以屬於託管表單的內部伺服器，也可以使用相對路徑或絕對路徑屬於外部伺服器。 若要將資料提交到託管表單的 AEM 伺服器，請使用對應至 AEM 伺服器根路徑的相對路徑。例如 `/content/forms/af/SampleForm.html`。若要將資料提交至任何其他伺服器，請使用絕對路徑。

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
* It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
* Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
* Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



若要設定REST端點：

1. 在&#x200B;**[!UICONTROL 編輯器]**&#x200B;中開啟最適化表單。
1. 選取&#x200B;**[!UICONTROL 最適化表單區塊]**。
1. 按一下屬性![屬性](/help/forms/assets/Smock_Properties_18_N.svg)圖示。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 提交至REST端點]**。
1. 指定REST端點URL
1. 您也可以&#x200B;**啟用POST要求**，並提供URL以張貼要求。

![啟用最適化表單的POST要求](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> * 若要將資料發佈到內部伺服器，請提供資源的路徑。 資料會張貼到資源的路徑。 例如 `/content/restEndPoint`。對於此類發佈要求，會使用提交要求的驗證資訊。
> * 若要將資料發佈到外部伺服器，請提供 URL。URL 的格式是：`https://host:port/path_to_rest_end_point`。請確保設定以匿名方式處理 POST 要求的路徑。

### 寄送電子郵件 {#email-submission-ue}

傳送電子郵件提交動作可讓您在成功提交表單時，傳送電子郵件給一或多個收件者。 「傳送電子郵件」設定可協助您建立電子郵件，以預先定義的格式包含表單資料。 例如，考慮下列範本，其中客戶名稱、送貨地址、州名和郵遞區號會從提交的表單資料中擷取。 [進一步瞭解最適化Forms中的電子郵件範本](/help/forms/html-email-templates-in-adaptive-forms.md)。 使用「傳送電子郵件」提交動作設定最適化表單的一些優點包括：

1. 它可讓快速通訊，因為表單資料會直接傳送給指定的電子郵件收件者。
1. 它有助於透過直接將表單提交整合到電子郵件通知中來簡化工作流程。
1. 它可協助組織自訂電子郵件內容，使其適合特定通訊需求。

通用編輯器中的![最適化表單屬性](/help/forms/assets/submit-actions-ue.png)


若要將提交動作設定為表單提交的電子郵件：

1. 在&#x200B;**編輯器**&#x200B;中開啟最適化表單。
1. 選取您的&#x200B;**[!UICONTROL 最適化表單區塊]**。
1. 按一下屬性![屬性](/help/forms/assets/Smock_Properties_18_N.svg)圖示。
1. 從&#x200B;**[!UICONTROL 送出動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;選項。
1. 選取傳送電子郵件選項後，您可以設定下列屬性，如下圖所示。

<table>
  <thead>
    <tr>
      <th>影像</th>
      <th>屬性</th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
    <td rowspan="7"><img src="/help/forms/assets/email-config-ue.png" alt="電子郵件設定"></td> 
    <td><b>來自</td>
    <td>指定寄件者的電子郵件地址。</td>
    </tr>
    <tr>
      <td><b>至</td>
      <td>指定電子郵件的主要收件者，則可新增多個電子郵件地址（以逗號分隔）。</td>
    </tr>
    <tr>
      <td><b>CC</td>
      <td>指定應接收電子郵件副本的收件者。</td>
    </tr>
    <tr>
      <td><b>BCC</td>
      <td>指定應接收電子郵件密件副本(BCC)的收件者。</td>
    </tr>
    <tr>
      <td><b>主旨</td>
      <td>指定電子郵件的主旨行。</td>
    </tr>
    <tr>
      <td><b>使用外部範本</td>
      <td>允許使用外部電子郵件範本來格式化電子郵件內容。 提供外部範本的URL或路徑，以整合在AEM Assets資料夾中託管的預先設計電子郵件範本。</td>
    </tr>
    <tr>
      <td><b>包含附件</td>
      <td>指定提交的表單資料是否應該包含透過電子郵件中的表單提交的附件。 支援的附件格式為PDF、XML和JSON。</td>
    </tr>
  </tbody>
</table>






<!--
        
        * **From**: The email address of the sender.
        * **To**: Specify the primary recipients of the email, multiple email addresses can be added, separated by commas.
        * **CC**: Specify the recipients who should receive a carbon copy (CC) of the email.
        * **BCC**: Specify the recipients who should receive a blind carbon copy (BCC) of the email.
        * **Subject**: Specify the subject line of the email.
        * **Use External Template**: Enables the use of an external email template for formatting the email content. Provide the URL or path to the External template path to integrate a pre-designed email template hosted in your AEM Assets folder.
        * **Include Attachment**: Specifies whether the submitted form data should include an attachment submitted through the form in the email.

    {width=50%,height=50%}![Enable post request for adaptive forms](/help/forms/assets/email-config-ue.png)

-->

## 在最適化表單提交上顯示自訂感謝訊息 {#submit-action-message-ue}

「在提交時」選項可協助您在最適化表單提交時設定「提交動作」訊息。若要設定表單的「提交動作」訊息：

1. 在&#x200B;**編輯器**&#x200B;中開啟最適化表單。
1. 選取您的&#x200B;**[!UICONTROL 最適化表單區塊]**。
1. 按一下屬性![屬性](/help/forms/assets/Smock_Properties_18_N.svg)圖示。
1. 按一下後，您會看到下列選項：
   * **[!UICONTROL 提交時]**：提交時可協助您自訂要在提交表單時顯示的訊息。 依預設，成功提交表單時，會向使用者顯示「感謝您提交表單」自訂訊息。
您也可以選取**[!UICONTROL 顯示訊息]**&#x200B;的選項，並在RTF **編輯器**&#x200B;中新增/編輯您的訊息，自訂表格提交時的感謝訊息。


## 另請參閱

{{see-more-forms-eds}}

---
title: 提交動作
description: 為最適化表單設定提交動作。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
hide: true
hidefromToC: true
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 100%

---

# 最適化表單提交動作

## 概觀

表單提交是使用者歷程中關鍵的最後步驟，就是在這時候處理所收集的資料並採取行動。此文件提供在通用編輯器中設定和管理自適應表單提交動作的綜合指南。

### 學習內容

本文件閱讀完畢後，您將了解如何進行以下事項：

- 為表單設定不同類型的提交動作
- 設定 REST 端點提交以便與外部系統整合
- 設定電子郵件提交以獲得表單回覆
- 實施自訂提交動作以滿足特定業務需求
- 處理提交期間的表單驗證和錯誤情況

### 目標讀者

本指南適用於以下人員：

- 實施提交邏輯的&#x200B;**表單開發人員**
- 將表單連接到後端系統的&#x200B;**系統整合商**
- 定義表單工作流程的&#x200B;**業務分析人員**
- 設計表單提交流程的&#x200B;**技術架構者**

### 可用的提交動作

通用編輯器提供兩種主要的提交動作類型：

1. **提交至 REST 端點** * 將表單資料傳送至 API 端點
2. **傳送電子郵件** * 透過電子郵件發送表單回覆

### 先決條件

在設定提交動作前，請確保您符合以下條件：

- 擁有通用編輯器的存取權
- 擁有表單設定的適當權限
- 了解目標提交端點或電子郵件設定

提交動作會指定透過最適化表單所收集的資料的目的地。使用者按一下表單上的「**[!UICONTROL 提交]**」按鈕時，提交流程隨即開始。AEM Forms 可提供以下所述的兩種提交動作類型，並讓您建立和使用自訂提交動作來滿足您的特定需求。現成可用的提交動作包括：

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

- [提交到 REST 端點](#rest-endpoint-submission-ue)
- [寄送電子郵件](#email-submission-ue)


### 提交到 REST 端點 {#rest-endpoint-submission-ue}

提交到 REST 端點動作會用於將已提交的表單資料傳送到指定的 REST 端點。該端點可能屬於代管表單的內部伺服器，也可能透過使用相對路徑或絕對路徑屬於外部伺服器。若要將資料提交到託管表單的 AEM 伺服器，請使用對應至 AEM 伺服器根路徑的相對路徑。例如 `/content/forms/af/SampleForm.html`。若要將資料提交到任何其他伺服器，可使用絕對路徑。

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
- It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
- Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
- Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



若要設定 REST 端點：

1. 在&#x200B;**[!UICONTROL 編輯器]**&#x200B;中開啟最適化表單。
1. 選取&#x200B;**[!UICONTROL 最適化表單區塊]**。
1. 按一下屬性「![properties](/help/forms/assets/Smock_Properties_18_N.svg)」圖示。
1. 從「**[!UICONTROL 提交動作]**」下拉式清單選取「**[!UICONTROL 提交到 REST 端點]**」。
1. 指定 REST 端點 URL。
1. 您也可以「**啟用 POST 要求**」並提供用於發佈要求的 URL。

![通用編輯器屬性面板的螢幕擷圖顯示 REST 端點設定欄位，包括表單提交所需的 URL 輸入以及「啟用 POST 要求」切換按鈕](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> - 若要將資料發佈到內部伺服器，請提供資源的路徑。資料會張貼到資源的路徑。例如 `/content/restEndPoint`。對於此類發佈要求，會使用提交要求的驗證資訊。
> - 若要將資料發佈到外部伺服器，請提供 URL。URL 的格式是：`https://host:port/path_to_rest_end_point`。請確保設定以匿名方式處理 POST 要求的路徑。

### 寄送電子郵件 {#email-submission-ue}

「寄送電子郵件」提交動作可讓您在成功提交表單後寄送電子郵件給一或多個收件者。寄送電子郵件組態有助於您建立可能包括預先定義格式的表單資料的電子郵件。例如，可考慮下列範本，這些範本會從已提交的表單資料中擷取客戶名稱、送貨地址、州名稱和郵遞區號。[深入了解最適化表單中的電子郵件範本](/help/forms/html-email-templates-in-adaptive-forms.md)。設定具有「寄送電子郵件」提交動作的最適化表單的一些優點包括：

1. 由於表單資料會直接傳送給指定的電子郵件收件者，因此可以實現快速通訊。
1. 其可將表單提交直接整合到電子郵件通知中，因此有助於簡化工作流程。
1. 其可協助組織自訂電子郵件內容，從而使其適合特定的通訊需求。

![通用編輯器中的最適化表單屬性](/help/forms/assets/submit-actions-ue.png)


若要將表單提交的提交動作設定為電子郵件：

1. 在&#x200B;**編輯器**&#x200B;中開啟最適化表單。
1. 選取您的&#x200B;**[!UICONTROL 最適化表單區塊]**。
1. 按一下屬性「![properties](/help/forms/assets/Smock_Properties_18_N.svg)」圖示。
1. 從「**[!UICONTROL 提交動作]**」下拉式清單選取「**[!UICONTROL 寄送電子郵件]**」選項。
1. 選取寄送電子郵件選項後，您即可設定下列屬性，如下圖所示。

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
    <td rowspan="7"><img src="/help/forms/assets/email-config-ue.png" alt="電子郵件組態"></td> 
    <td><b>寄件者</td>
    <td>指定寄件者的電子郵件地址。</td>
    </tr>
    <tr>
      <td><b>收件者</td>
      <td>指定電子郵件的主要收件者，可以新增多個電子郵件地址，並以逗號分隔。</td>
    </tr>
    <tr>
      <td><b>副本</td>
      <td>指定應接收電子郵件副本 (CC) 的收件者。</td>
    </tr>
    <tr>
      <td><b>密件副本</td>
      <td>指定應接收電子郵件密件副本 (BCC) 的收件者。</td>
    </tr>
    <tr>
      <td><b>主旨</td>
      <td>指定電子郵件的主旨行。</td>
    </tr>
    <tr>
      <td><b>使用外部範本</td>
      <td>允許使用外部電子郵件範本來格式化電子郵件內容。提供外部範本的 URL 或路徑，以整合在 AEM Assets 資料夾中代管的預先設計的電子郵件範本。</td>
    </tr>
    <tr>
      <td><b>包括附件</td>
      <td>指定提交的表單資料是否應包括透過電子郵件中的表單提交的附件。支援的附件格式為 PDF、XML 和 JSON。</td>
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

    ![Screenshot of the Universal Editor email configuration panel showing fields for From, To, CC, BCC, Subject, and options for external templates and attachments](/help/forms/assets/email-config-ue.png)

-->

## 提交最適化表單後顯示自訂感謝訊息 {#submit-action-message-ue}

「提交時」選項可協助您在提交最適化表單時設定「提交動作」訊息，若要為表單設定「提交動作」訊息：

1. 在&#x200B;**編輯器**&#x200B;中開啟最適化表單。
1. 選取您的&#x200B;**[!UICONTROL 最適化表單區塊]**。
1. 按一下屬性「![properties](/help/forms/assets/Smock_Properties_18_N.svg)」圖示。
1. 點擊後，您即會看到下列選項：
   - **[!UICONTROL 提交時]**：「提交時」可協助您自訂提交表單時顯示的訊息。預設情況下，成功提交表單時，會向使用者顯示自訂訊息「感謝您提交表單」。
您也可以在提交表單時自訂感謝訊息，透過選取「**[!UICONTROL 顯示訊息]**」選項，然後以 RTF 文字&#x200B;**編輯器**&#x200B;新增/編輯您的訊息。




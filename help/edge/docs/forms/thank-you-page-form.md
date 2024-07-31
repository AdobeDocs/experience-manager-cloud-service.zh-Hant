---
title: 提交表單後顯示自訂感謝訊息
description: 了解如何設定 Forms 區塊的感謝頁面和重新導向，以最佳化使用者體驗並簡化使用者歷程。
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 51%

---

# 提交表單後顯示自訂感謝訊息

使用者提交表單後，透過感謝訊息提供順暢的體驗至關重要。 它不僅可確認提交成功，也可提升使用者滿意度，並指引他們進一步完成歷程。

* **感謝訊息**：感謝訊息是使用者體驗的基石，可在強化品牌識別的同時，提供保證及傳達重要資訊。 此頁面是對使用者行為的直接認可，讓他們產生一種完成後的滿足感。

* **重新導向**：重新導向可發揮關鍵作用，旨在引導使用者前往相關目的地、提高最佳參與度且最後達到更高轉換率。重新導向可無縫引導使用者進入下一步歷程，確保使用者得到流暢的導覽體驗。例如，在收集初始明細後，將使用者重新導向至付款頁面。

最適化表單區塊的預設行為是在提交時顯示以下的感謝訊息。成功提交表單時，訊息會顯示在表單頂端。

![預設感謝訊息](/help/edge/assets/thank-you-message.png)

但是，您可以靈活地自訂這項體驗，以滿足您的特定需求。選項包括：    

* 提交表單後顯示自訂感謝訊息
* 將使用者重新導向至提交後的另一個頁面，以供進一步動作

>[!NOTE]
>
> 您可以參考下列[查詢試算表](/help/edge/docs/forms/assets/enquiry.xlsx)，根據您的要求自訂感謝訊息。

## 設定自訂感謝訊息

如果您希望在成功提交表單時顯示個人化的感謝訊息，可以設定試算表以顯示該訊息。

請依照以下步驟為您的最適化表單區塊設定自訂感謝訊息：

1. 前往 Microsoft SharePoint 或 Google Workspace 的 Edge Deliver 專案資料夾，並開啟您的試算表。
1. 在`value`欄中為試算表中的`submit`欄位型別新增自訂的感謝訊息。

   ![自訂感謝訊息](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   例如，在`submit`欄位型別的`value`欄中新增`Submission Successful!`訊息。

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

   ![自訂感謝訊息](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## 提交後將使用者重新導向至另一個頁面

提交表單後將使用者重新導向至另一個頁面，可提供相關資訊、確認動作並引導使用者前往期望的結果頁面，藉此加強使用者體驗。例如，

* 使用者填寫購買表單後，他們將被重新導向至付款頁面，以安全方式完成交易。
* 提交活動或網路研討會的註冊表單後，使用者將被重新導向至顯示活動詳細資訊 (例如日期、時間和地點) 的確認頁面。

請依照下列步驟，將使用者重新導向至其他頁面：

1. 前往 Microsoft SharePoint 或 Google Workspace 的 Edge Deliver 專案資料夾，並開啟您的試算表。
1. 在試算表中針對`submit`欄位型別貼上`value`欄中的URL，以便在成功提交表單時重新導向使用者。
若要將頁面重新導向至其他頁面，請使用[Edge Delivery檔案](https://www.aem.live/docs/)頁面URL。

   ![感謝您重新導向URL](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 來預覽和發佈試算表。

   ![重新導向感謝訊息](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

您也可以為`submit`欄位型別建立新檔案檔案，並將其預覽URL新增至`value`欄。

使用者提交表單後，請務必提供清楚的感謝訊息。 如此可確認提交成功，並提升使用者滿意度。

## 另請參閱

{{see-more-forms-eds}}

<!--
## Configuring a custom thank you message

The default behavior of Adaptive Forms Block is to display the following thank you message on submission. The message is displayed on the top of the form. 

![default thank you message](/help/edge/assets/thank-you-message.png)


Follow the below steps to configure a custom thank you message for your Adaptive Forms Block:

1. Access your AEM Project on your local machine or GitHub repository.

2. Navigate to [AEM Project Folder]\blocks\form\submit.js file for editing.

3. Locate the following code 

    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Thanks for your submission';

    ```

4. Replace the default message with your custom message. For example, 


    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Your submission has been received and noted.';

    ```


1. Save the file. Commit the updated file to your GitHub Repository. Now, when you submit a form, the custom thank you message is displayed. For example,

![Custom thank you message](/help/edge/assets/custom-thank-you-message.png)

* **Thank you message**: A thank you message is a cornerstone of user experience, offering reassurance and conveying important information while reinforcing brand identity. It serves as a direct acknowledgment of the user's action, fostering a sense of completion and satisfaction.

* **Redirect**: A redirect plays a pivotal role in steering users towards relevant destinations, optimizing engagement, and ultimately boosting conversion rates. By seamlessly guiding users to the next step in their journey, a redirect ensures a smooth navigation experience. For example, redirecting user to payments page after collecting initial details. 

In the Adaptive Forms Block, the default behavior is to display a thank you message. However, you have the flexibility to tailor this experience to meet your specific needs. Options include:

* [Configuring a custom thank you message to align with your brand and communication goals](#configuring-the-thank-you-page-and-message) 
* [Redirecting users to another page post-submission for further action](#redirect-users-to-another-page-post-submission)

## Redirect users to another page post-submission

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 





1. Access your AEM Edge Delivery project folder on Microsoft SharePoint or Google Workspace.
1. Create a Microsoft Word or Google Docs file named "thankyou" within your project directory.
1. Add your thank you message to the "thankyou" file. </br>
   
    ![Example thank you page](/help/edge/assets/sample-thankyou-page.png) 

1. Use AEM Sidekick to preview and publish the "thankyou" file.

 Your Adaptive Forms Block displays the "thankyou" page on form submission. 

## Redirect users to another page post-submission

By default, the Adaptive Forms Block redirects the users to the "thankyou" page. To redirect users to a page other than the default "thankyou" page, you have two options: 

* [Replace the "thankyou" page with a different page](#replace-the-existing-thankyou-page) 
* [Use website redirects for "thankyou" page redirection](#use-website-redirects-for-thankyou-page-redirection) 

### Replace the "thankyou" page

1. Open the "[EDS Project]/blocks/form/form.js" file for editing.
1. Change the `thankyou` page in the following line to page of your choice:

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'thankyou';

    ```

    For example,

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'payment';
        
    ```
    
    >[!NOTE]
    >
    > Ensure that a page with the same name exists in your Edge Delivery Services project folder on either Microsoft SharePoint or Google Workspace. If the page does not exist, proceed to create and publish it.  

1. Proceed to check in the updated 'form.js' folder and its underlying files to your Edge Delivery Services project on GitHub. This update ensures that the form now redirects to the updated page as specified.

1. Ensure that the page exists in your EDS project folder and publish it.


### Use website redirects for "thankyou" page redirection

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 



## See also

{{see-more-forms-eds}}
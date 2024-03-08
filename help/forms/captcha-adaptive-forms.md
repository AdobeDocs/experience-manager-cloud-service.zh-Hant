---
title: 如何在最適化Forms中使用驗證碼？
description: 瞭解如何為最適化表單設定或Google reCAPTCHA服務。
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
feature: Adaptive Forms, Foundation Components
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 6%

---


# 在最適化Forms中使用reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/creating-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html) |
| AEM as a Cloud Service  | 本文章 |
| 套用至 | 根據Foundation元件的最適化表單。 <br> 針對以核心元件為基礎的最適化表單， [按一下這裡](/help/forms/captcha-adaptive-forms-core-components.md). |


CAPTCHA （完全自動化公用圖靈測試來區分電腦和人之間的差異）是一種常用於線上交易的程式，以區分人和自動化程式或機器人。 這會帶來挑戰，並評估使用者的回應，以判斷其是否為人類或機器人與網站互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意目的來確保線上交易的安全。

[!DNL AEM Forms] 在最適化Forms中支援reCAPTCHA。 您可以使用Google的reCAPTCHA服務來實作CAPTCHA。

>[!NOTE]
>
>* [!DNL AEM Forms] 支援reCaptcha v2和reCaptcha Enterprise。 不支援任何其他版本。
>* 上離線模式不支援最適化Forms中的reCAPTCHA [!DNL AEM Forms] 應用程式。
>

## 透過Google設定reCAPTCHA服務 {#google-reCAPTCHA}

表單作者可使用Google的reCAPTCHA服務，在最適化Forms中實作reCAPTCHA。 它提供進階驗證碼功能以保護您的網站。 如需reCAPTCHA運作方式的詳細資訊，請參閱 [Google reCAPTCHA](https://developers.google.com/recaptcha/). reCAPTCHA服務包括 [!DNL reCAPTCHA v2] 和 [!DNL reCAPTCHA Enterprise] 您可以將其中整合至 [!DNL AEM Forms]. 您可以根據自己的需求，設定reCAPTCHA服務以啟用：

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [AEM Forms中的reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [AEM Forms中的reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)


### 設定reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. 建立或選取 [Google雲端專案](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) 並啟用 [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. 取得 [專案ID](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) 並建立 [API金鑰](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) 和 [網站的網站金鑰](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. 建立雲端服務的設定容器。

   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 選取資料夾或建立資料夾，然後使用下列步驟啟用雲端設定的資料夾：
      1. 在組態瀏覽器中，選取資料夾並選取 **[!UICONTROL 屬性]**.
      1. 在組態內容對話方塊中，啟用 **[!UICONTROL 雲端設定]**.
      1. 選取 **[!UICONTROL 儲存並關閉]** 以儲存組態並結束對話方塊。

1. 設定雲端服務 [!DNL reCAPTCHA Enterprise].

   1. 在您的Experience Manager編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**.
   1. 選取 **[!UICONTROL reCAPTCHA]**. 「組態」頁面隨即開啟。 選取您建立的設定容器，然後選取 **[!UICONTROL 建立]**.
   1. 選擇版本為 [!DNL reCAPTCHA Enterprise] 並指定reCAPTCHA Enterprise服務的名稱、專案ID、網站金鑰和API金鑰（在步驟2中取得）。
   1. 選取金鑰型別，金鑰型別應與您在下列位置設定的網站金鑰相同： [Google雲端專案](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin)例如， **核取方塊網站索引鍵** 或 **以分數為基礎的網站金鑰**.
   1. 指定 [臨界值分數在0到1的範圍內](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores). 分數大於或等於臨界值分數會識別人類互動，否則會被視為機器人互動。
   1. 選取 **[!UICONTROL 建立]** 以建立雲端服務設定。

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Select **[!UICONTROL Save Settings]** and then select **[!UICONTROL OK]** to complete the configuration.
-->

reCAPTCHA Enterprise服務啟用後，就可在調適型表單中使用。 另請參閱 [在最適化表單中使用驗證碼](#using-reCAPTCHA).

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### 設定Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. 取得 [reCAPTCHA API金鑰組](https://www.google.com/recaptcha/admin) 來自Google。 它包含 **網站金鑰** 和 **秘密金鑰**.
1. 建立雲端服務的設定容器。
   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 選取資料夾或建立資料夾，然後使用下列步驟啟用雲端設定的資料夾：
      1. 在組態瀏覽器中，選取資料夾並選取 **[!UICONTROL 屬性]**.
      1. 在組態內容對話方塊中，啟用 **[!UICONTROL 雲端設定]**.
      1. 選取 **[!UICONTROL 儲存並關閉]** 以儲存組態並結束對話方塊。

1. 設定reCAPTCHA v2的雲端服務。

   1. 在您的AEM編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **Cloud Service**.
   1. 選取 **[!UICONTROL reCAPTCHA]**. 「組態」頁面隨即開啟。 選取您建立的設定容器，然後選取 **[!UICONTROL 建立]**.
   1. 選擇版本為 [!DNL reCAPTCHA v2] ，指定reCAPTCHA服務的名稱、網站金鑰和秘密金鑰（在步驟1取得），然後選取 **[!UICONTROL 建立]** 以建立雲端服務設定。
   1. 在「編輯元件」對話方塊中，指定在步驟1中取得的網站和秘密金鑰。 選取 **[!UICONTROL 儲存設定]** 然後選取 **確定** 以完成設定。

   在設定reCAPTCHA服務後，就可用於調適型表單。 如需詳細資訊，請參閱 [在最適化表單中使用驗證碼](#using-reCAPTCHA).

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## 在最適化表單中使用reCAPTCHA {#using-reCAPTCHA}

若要在最適化表單中使用reCAPTCHA：

1. 在編輯模式中開啟最適化表單。

   >[!NOTE]
   >
   >確定建立最適化表單時選取的設定容器包含reCAPTCHA雲端服務。 您也可以編輯最適化表單屬性，以變更與表單相關聯的設定容器。

1. 在元件瀏覽器中，拖放 **驗證碼** 元件至最適化表單。

   >[!NOTE]
   >
   >* 不支援在最適化表單中使用多個驗證碼元件。 此外，不建議在標示為延遲載入的面板或片段中使用驗證碼。
   >* reCaptcha有時效性，大約會在幾分鐘後過期。 因此，建議將驗證碼元件放在最適化表單中的提交按鈕之前。

1. 選取您新增的驗證碼元件，然後選取 ![cmppr](assets/cmppr.png) 以編輯其屬性。
1. 指定驗證碼介面工具集的標題。 預設值為 **驗證碼**. 選取 **隱藏標題** 如果您不想顯示標題。
1. 從 **驗證碼服務** 下拉式清單，選取 **reCAPTCHA** 以啟用reCAPTCHA服務（若您已依照中的說明進行設定） [Google的reCAPTCHA服務](#google-reCAPTCHA).
1. 從「設定」下拉式清單中選取設定 **reCAPTCHA Enterprise** 或 **reCAPTCHA v2**
   1. 如果您選取 **reCAPTCHA Enterprise** 版本，金鑰型別可以是 **核取方塊** 或 **以分數為基礎**，此量度會根據您設定時的選擇 [網站的網站金鑰](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key)：

   >[!NOTE]
   >
   >* 在雲端設定中，具有 **金鑰型別** 作為 **核取方塊**，如果驗證碼驗證失敗，自訂的錯誤訊息會顯示為內嵌訊息。
   >* 在雲端設定中，具有 **金鑰型別** 作為 **以分數為基礎**，則當驗證碼驗證失敗時，自訂的錯誤訊息會顯示為快顯訊息。

   1. 您可以選取大小為 **[!UICONTROL 一般]** 和 **[!UICONTROL 精簡]**.
   1. 您可以選取 **[!UICONTROL 繫結參考]**，在 **[!UICONTROL 繫結參考]** 提交的資料為已繫結資料，否則為未繫結資料。 以下是提交表單時，未繫結資料和已繫結資料（以SSN為繫結參考）的XML範例。

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data>
                   <captcha16820607953761>
                       <captchaType>reCaptchaEnterprise</captchaType>
                       <captchaScore>0.9</captchaScore>
                   </captcha16820607953761>
               </data>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>371237912</SSN>
                       <FirstName>Sarah </FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608034928</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   ```xml
           <?xml version="1.0" encoding="UTF-8" standalone="no"?>
           <afData>
           <afUnboundData>
               <data/>
           </afUnboundData>
           <afBoundData>
               <Root
                   xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                   <PersonalDetails>
                       <SSN>
                           <captchaType>reCaptchaEnterprise</captchaType>
                           <captchaScore>0.9</captchaScore>
                       </SSN>
                       <FirstName>Sarah</FirstName>
                       <LastName>Smith</LastName>
                   </PersonalDetails>
                   <OtherInfo>
                       <City>California</City>
                       <Address>54 Residency</Address>
                       <State>USA</State>
                       <Zip>123112</Zip>
                   </OtherInfo>
               </Root>
           </afBoundData>
           <afSubmissionInfo>
               <stateOverrides/>
               <signers/>
               <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
               <afSubmissionTime>20230608035111</afSubmissionTime>
           </afSubmissionInfo>
           </afData>
   ```

   如果您選取 **reCAPTCHA v2** 版本：
   1. 您可以選取大小為 **[!UICONTROL 一般]** 或 **[!UICONTROL 精簡]** 用於reCAPTCHA Widget。
   1. 您可以選取 **[!UICONTROL 隱形]** 僅在可疑活動的情況下顯示驗證碼質詢的選項。

   已針對最適化表單啟用reCAPTCHA服務。 您可以預覽表單，並檢視驗證碼是否正常運作。 此 **受reCAPTCHA保護** 徽章（如下所示）會顯示在受保護的表單上。
   ![Google受reCAPTCHA徽章保護](/help/forms/assets/google-recaptcha-v2.png)

1. 儲存屬性。

>[!NOTE]
> 
> 不要選取 **[!UICONTROL 預設]** 驗證碼服務下拉式清單中，預設的AEM驗證碼服務已過時。

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### 根據規則顯示或隱藏驗證碼元件 {#show-hide-captcha}

您可以根據在最適化表單中元件套用的規則，選擇顯示或隱藏驗證碼元件。 選取元件，選取 ![編輯規則](assets/edit-rules-icon.svg)，並選取 **[!UICONTROL 建立]** 以建立規則。 如需建立規則的詳細資訊，請參閱 [規則編輯器](rule-editor.md).

例如，只有在表單中的「貨幣值」欄位的值超過25000時，CAPTCHA元件才會顯示在調適型表單中。

選取 **[!UICONTROL 貨幣值]** 欄位建立下列規則：

![顯示或隱藏規則](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> 當您選取reCAPTCHA v2設定時，大小會設為 [!UICONTROL 隱形]，顯示/隱藏選項仍會維持停用。

### 進行驗證碼驗證 {#validate-captcha}

您可以在提交表單時或在使用者動作和條件的基礎上進行最適化表單中的驗證碼驗證。

#### 在表單提交時進行驗證碼驗證 {#validation-form-submission}

若要在提交最適化表單時自動驗證碼：

1. 選取驗證碼元件並選取 ![cmppr](assets/configure-icon.svg) 以檢視元件屬性。
1. 在 **[!UICONTROL 驗證碼驗證]** 區段，選取 **[!UICONTROL 在表單提交時進行驗證碼驗證]**.
1. 選取 ![完成](assets/save_icon.svg) 以儲存元件屬性。

#### 驗證使用者動作和條件的驗證碼 {#validate-captcha-user-action}

若要根據條件和使用者動作來驗證驗證碼：

1. 選取驗證碼元件並選取 ![cmppr](assets/configure-icon.svg) 以檢視元件屬性。
1. 在 **[!UICONTROL 驗證碼驗證]** 區段，選取 **[!UICONTROL 使用者動作時進行驗證碼驗證]**.
1. 選取 ![完成](assets/save_icon.svg) 以儲存元件屬性。

[!DNL Experience Manager Forms] 提供 `ValidateCAPTCHA` 使用預先定義條件進行驗證碼驗證的API。 您可以使用自訂提交動作或在調適型表單中定義元件規則來叫用API。

以下範例為 `ValidateCAPTCHA` 使用預先定義條件進行驗證碼驗證的API：

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
     GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus (400);
            return;
        }
    }
```

此範例表示 `ValidateCAPTCHA` 只有在使用者在填寫表單時指定的數字方塊位數大於5時，API才會驗證表單中的驗證碼。

**選項1：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API使用自訂提交動作來驗證CAPTCHA**

執行以下步驟以使用 `ValidateCAPTCHA` 使用自訂提交動作來驗證驗證碼的API：

1. 新增指令碼，其中包括 `ValidateCAPTCHA` 自訂提交動作的API。 如需自訂提交動作的詳細資訊，請參閱 [建立最適化Forms的自訂提交動作](custom-submit-action-form.md).
1. 從中選擇自訂提交動作的名稱 **[!UICONTROL 提交動作]** 中的下拉式清單 **[!UICONTROL 提交]** 最適化表單的屬性。
1. 選取 **[!UICONTROL 提交]**. 系統會根據中定義的條件來驗證驗證碼 `ValidateCAPTCHA` 自訂提交動作的API。

**選項2：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API可在提交表單前，在使用者動作時驗證驗證碼**

您也可以叫用 `ValidateCAPTCHA` API，方法是在最適化表單的元件上套用規則。

例如，您新增 **[!UICONTROL 驗證碼驗證]** 最適化表單中的按鈕，並建立規則以在按一下按鈕時叫用服務。

下圖說明如何在 **[!UICONTROL 驗證碼驗證]** 按鈕：

![驗證碼驗證](assets/captcha-validation1.gif)

您可以叫用包含的自訂servlet `ValidateCAPTCHA` API使用規則編輯器，並根據驗證結果啟用或停用最適化表單的提交按鈕。

同樣地，您可以使用規則編輯器在適用性表單中包含驗證碼的自訂方法。

<!--

### Add custom CAPTCHA services {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. However, you can add a custom service to display in the **[!UICONTROL CAPTCHA Service]** drop-down list.  

The following is a sample implementation of the interface to add additional CAPTCHA service to your Adaptive Form:

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` refers to the resource path of the CAPTCHA component in the Sling repository. Use this property to include details specific to the CAPTCHA component. For example, `captchaPropertyNodePath` includes information for the reCAPTCHA cloud configuration configured on the CAPTCHA component. The cloud configuration information provides **[!UICONTROL Site Key]** and **[!UICONTROL Secret Key]** settings for implementing the reCAPTCHA service.

`userResponseToken` refers to the `g_recaptcha_response` that gets generated after solving a CAPTCHA in a form. -->

### 編輯reCAPTCHA服務網域 {#reCAPTCHA-service-domain}

reCAPTCHA服務使用 `https://www.recaptcha.net/` 作為預設網域。 您可以修改設定以進行設定 `https://www.google.com/` 或任何自訂網域名稱，用於載入、呈現和驗證reCAPTCHA服務。

設定 **[!UICONTROL af.cloudservices.recaptcha.domain]** 的屬性 **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]** 要指定的設定 `https://www.google.com/` 或任何其他自訂網域名稱。 下列JSON檔案顯示範例：

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

若要設定值，請[使用 AEM SDK 產生 OSGi 設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hant#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並[將設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant#deployment-process)您的 Cloud Service 執行個體。

## 另請參閱 {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Reference Themes, Templates, and Form Data models for Adaptive Forms](/help/forms/reference-themes-templates-data-models.md)

-->

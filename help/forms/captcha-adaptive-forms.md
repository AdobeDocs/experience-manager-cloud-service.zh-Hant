---
title: 如何在最適化Forms中使用驗證碼？
description: 瞭解如何為最適化表單設定或Google reCAPTCHA服務。
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
feature: Adaptive Forms, Foundation Components
role: User, Developer
source-git-commit: e6f986e014e45fad461721d84f18cc49a7bb434e
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 6%

---


# 在最適化Forms中使用reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/creating-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/captcha-adaptive-forms.html) |
| AEM as a Cloud Service  | 本文章 |
| 套用至 | 根據Foundation元件的最適化表單。 針對以核心元件為基礎的最適化表單<br>，[按一下這裡](/help/forms/captcha-adaptive-forms-core-components.md)。 |


CAPTCHA （完全自動化公用圖靈測試來區分電腦和人之間的差異）是一種常用於線上交易的程式，以區分人和自動化程式或機器人。 這會帶來挑戰，並評估使用者的回應，以判斷其是否為人類或機器人與網站互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意目的來確保線上交易的安全。

AEM Formsas a Cloud Service支援下列CAPTCHA解決方案：

* [Google reCAPTCHA](#configure-recaptcha-service-by-google)
* [Cloudflare Turnstile](/help/forms/integrate-adaptive-forms-turnstile.md)
* [驗證碼](/help/forms/integrate-adaptive-forms-hcaptcha.md)

## 透過Google設定reCAPTCHA服務 {#google-reCAPTCHA}

表單作者可使用Google的reCAPTCHA服務，在最適化Forms中實作reCAPTCHA。 它提供進階驗證碼功能以保護您的網站。 如需reCAPTCHA運作方式的詳細資訊，請參閱[Google reCAPTCHA](https://developers.google.com/recaptcha/)。 AEM Forms支援[!DNL reCAPTCHA v2]和[!DNL reCAPTCHA Enterprise]。 不支援任何其他版本。 另請注意，[!DNL AEM Forms]應用程式上的離線模式不支援最適化Forms中的reCAPTCHA。 您可以根據自己的需求，設定reCAPTCHA服務以啟用：

![reCAPTCHA](/help/forms/assets/recaptcha_new.png)

* [AEM Forms中的reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [AEM Forms中的reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)


### 設定reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. 建立或選取[Google Cloud專案](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin)並啟用[reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api)。
1. 取得[專案識別碼](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed)並建立網站的[API金鑰](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key)和[網站金鑰](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key)。
1. 建立雲端服務的設定容器。

   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 選取資料夾或建立資料夾，然後使用下列步驟啟用雲端設定的資料夾：
      1. 在組態瀏覽器中，選取資料夾並選取&#x200B;**[!UICONTROL 屬性]**。
      1. 在[組態內容]對話方塊中，啟用&#x200B;**[!UICONTROL 雲端組態]**。
      1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並結束對話方塊。

1. 設定[!DNL reCAPTCHA Enterprise]的雲端服務。

   1. 在您的Experience Manager作者執行個體上，移至![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**。
   1. 選取&#x200B;**[!UICONTROL reCAPTCHA]**。 「組態」頁面隨即開啟。 選取您建立的組態容器，並選取&#x200B;**[!UICONTROL 建立]**。
   1. 選取版本為[!DNL reCAPTCHA Enterprise]，並指定reCAPTCHA Enterprise服務的名稱、專案ID、網站金鑰和API金鑰（在步驟2中取得）。
   1. 選取金鑰型別，金鑰型別應與您在[Google Cloud專案](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin)中設定的網站金鑰相同，例如，**核取方塊網站金鑰**&#x200B;或&#x200B;**以分數為基礎的網站金鑰**。
   1. 指定0到1](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores)範圍內的[臨界值分數。 分數大於或等於臨界值分數會識別人類互動，否則會被視為機器人互動。
   1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立雲端服務組態。

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Select **[!UICONTROL Save Settings]** and then select **[!UICONTROL OK]** to complete the configuration.
-->

reCAPTCHA Enterprise服務啟用後，就可在調適型表單中使用。 請參閱在最適化表單](#using-reCAPTCHA)中使用驗證碼[。

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->

### 設定Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. 從Google取得[reCAPTCHA API金鑰組](https://www.google.com/recaptcha/admin)。 它包含&#x200B;**網站金鑰**&#x200B;和&#x200B;**秘密金鑰**。
1. 建立雲端服務的設定容器。
   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 選取資料夾或建立資料夾，然後使用下列步驟啟用雲端設定的資料夾：
      1. 在組態瀏覽器中，選取資料夾並選取&#x200B;**[!UICONTROL 屬性]**。
      1. 在[組態內容]對話方塊中，啟用&#x200B;**[!UICONTROL 雲端組態]**。
      1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並結束對話方塊。

1. 設定reCAPTCHA v2的雲端服務。

   1. 在您的AEM作者執行個體上，移至![tools-1](assets/tools-1.png) > **Cloud Service**。
   1. 選取&#x200B;**[!UICONTROL reCAPTCHA]**。 「組態」頁面隨即開啟。 選取您建立的組態容器，並選取&#x200B;**[!UICONTROL 建立]**。
   1. 將版本選取為[!DNL reCAPTCHA v2]，指定reCAPTCHA服務的名稱、網站金鑰和秘密金鑰（在步驟1中取得），並選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立雲端服務組態。
   1. 在「編輯元件」對話方塊中，指定在步驟1中取得的網站和秘密金鑰。 選取&#x200B;**[!UICONTROL 儲存設定]**，然後選取&#x200B;**確定**&#x200B;以完成設定。

   在設定reCAPTCHA服務後，就可用於調適型表單。 如需詳細資訊，請參閱[在最適化表單中使用驗證碼](#using-reCAPTCHA)。

<!--![reCAPTCHA v2](/help/forms/assets/recaptcha-v2.png)-->


## 在最適化表單中使用Google reCAPTCHA {#using-reCAPTCHA}

在最適化表單中使用Google reCAPTCHA：

1. 在編輯模式中開啟最適化表單。

   >[!NOTE]
   >
   >確定建立最適化表單時選取的設定容器包含reCAPTCHA雲端服務。 您也可以編輯最適化表單屬性，以變更與表單相關聯的設定容器。

1. 從元件瀏覽器中，將&#x200B;**驗證碼**&#x200B;元件拖放至最適化表單上。

   >[!NOTE]
   >
   >* 不支援在最適化表單中使用多個驗證碼元件。 此外，不建議在標示為延遲載入的面板或片段中使用驗證碼。
   >* reCaptcha有時效性，大約會在幾分鐘後過期。 因此，建議將驗證碼元件放在最適化表單中的提交按鈕之前。

1. 選取您新增的Captcha元件，並選取![cmppr](assets/cmppr.png)以編輯其屬性。
1. 指定驗證碼介面工具集的標題。 預設值為&#x200B;**驗證碼**。 如果您不想顯示標題，請選取&#x200B;**隱藏標題**。
1. 從&#x200B;**Captcha服務**&#x200B;下拉式清單中，選取&#x200B;**reCAPTCHA**&#x200B;以啟用reCAPTCHA服務(若您已依照Google](#google-reCAPTCHA)的[reCAPTCHA服務說明進行設定)。
1. 從「設定」下拉式清單中選取&#x200B;**reCAPTCHA Enterprise**&#x200B;或&#x200B;**reCAPTCHA v2**&#x200B;的組態
   1. 若您選取&#x200B;**reCAPTCHA Enterprise**&#x200B;版本，金鑰型別可以是&#x200B;**核取方塊**&#x200B;或&#x200B;**以分數為基礎**，其依據是您在設定網站的[網站金鑰時的選擇](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key)：

   >[!NOTE]
   >
   >* 在&#x200B;**金鑰型別**&#x200B;為&#x200B;**核取方塊**&#x200B;的雲端設定中，如果驗證碼驗證失敗，自訂的錯誤訊息會顯示為內嵌訊息。
   >* 在&#x200B;**金鑰型別**&#x200B;為&#x200B;**以分數為**&#x200B;的雲端設定中，如果驗證碼驗證失敗，自訂的錯誤訊息會顯示為快顯訊息。

   1. 您可以選取&#x200B;**[!UICONTROL Normal]**&#x200B;和&#x200B;**[!UICONTROL Compact]**&#x200B;的大小。
   1. 您可以選取&#x200B;**[!UICONTROL 繫結參考]**，在&#x200B;**[!UICONTROL 繫結參考]**&#x200B;中，提交的資料為繫結資料，否則為未繫結資料。 以下是提交表單時，未繫結資料和已繫結資料（以SSN為繫結參考）的XML範例。

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

   如果您選取&#x200B;**reCAPTCHA v2**&#x200B;版本：
   1. 您可以為reCAPTCHA Widget選取大小為&#x200B;**[!UICONTROL Normal]**&#x200B;或&#x200B;**[!UICONTROL Compact]**。
   1. 您可以選取&#x200B;**[!UICONTROL 隱藏]**&#x200B;選項，只在可疑活動時才顯示驗證碼質詢。

   已針對最適化表單啟用reCAPTCHA服務。 您可以預覽表單，並檢視驗證碼是否正常運作。 受reCAPTCHA **保護的**徽章（如下所示）會顯示在受保護的表單上。
   ![受reCAPTCHA徽章保護的Google](/help/forms/assets/google-recaptcha-v2.png)

1. 儲存屬性。

>[!NOTE]
> 
> 請勿從Captcha服務下拉式清單中選取&#x200B;**[!UICONTROL 預設]**，因為預設的AEM CAPTCHA服務已過時。

>[!VIDEO](https://video.tv.adobe.com/v/3422641/recaptcha-google-adaptive-forms/?quality=12&learn=on)

### 根據規則顯示或隱藏驗證碼元件 {#show-hide-captcha}

您可以根據在最適化表單中元件套用的規則，選擇顯示或隱藏驗證碼元件。 選取元件，選取![編輯規則](assets/edit-rules-icon.svg)，然後選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立規則。 如需建立規則的詳細資訊，請參閱[規則編輯器](rule-editor.md)。

例如，只有在表單中的「貨幣值」欄位的值超過25000時，CAPTCHA元件才會顯示在調適型表單中。

選取表單中的&#x200B;**[!UICONTROL 貨幣值]**&#x200B;欄位，並建立下列規則：

![顯示或隱藏規則](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> 當您選取reCAPTCHA v2組態且大小設定為[!UICONTROL 隱藏]時，顯示/隱藏選項仍會停用。

### 進行驗證碼驗證 {#validate-captcha}

您可以在提交表單時或在使用者動作和條件的基礎上進行最適化表單中的驗證碼驗證。

#### 在表單提交時進行驗證碼驗證 {#validation-form-submission}

若要在提交最適化表單時自動驗證碼：

1. 選取CAPTCHA元件並選取![cmppr](assets/configure-icon.svg)以檢視元件屬性。
1. 在&#x200B;**[!UICONTROL 驗證碼驗證]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 表單提交時驗證碼驗證]**。
1. 選取![完成](assets/save_icon.svg)以儲存元件屬性。

#### 驗證使用者動作和條件的驗證碼 {#validate-captcha-user-action}

若要根據條件和使用者動作來驗證驗證碼：

1. 選取CAPTCHA元件並選取![cmppr](assets/configure-icon.svg)以檢視元件屬性。
1. 在&#x200B;**[!UICONTROL 驗證碼]**&#x200B;區段中，選取使用者動作上的&#x200B;**[!UICONTROL 驗證碼]**。
1. 選取![完成](assets/save_icon.svg)以儲存元件屬性。

[!DNL Experience Manager Forms]提供`ValidateCAPTCHA` API以使用預先定義的條件來驗證驗證碼。 您可以使用自訂提交動作或在調適型表單中定義元件規則來叫用API。

以下是`ValidateCAPTCHA` API的範例，使用預先定義的條件來驗證驗證碼：

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
     GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

此範例表示`ValidateCAPTCHA` API只有在使用者在填寫表單時指定的數字方塊位數大於5時，才會驗證表單中的驗證碼。

**選項1：使用[!DNL Experience Manager Forms] ValidateCAPTCHA API，使用自訂提交動作來驗證CAPTCHA**

執行以下步驟來使用`ValidateCAPTCHA` API，使用自訂提交動作來驗證驗證碼：

1. 將包含`ValidateCAPTCHA` API的指令碼新增至自訂提交動作。 如需自訂提交動作的詳細資訊，請參閱[為最適化Forms建立自訂提交動作](custom-submit-action-form.md)。
1. 從最適化表單的&#x200B;**[!UICONTROL 提交]**&#x200B;屬性中的&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取自訂提交動作的名稱。
1. 選取&#x200B;**[!UICONTROL 提交]**。 系統會根據自訂提交動作的`ValidateCAPTCHA` API中定義的條件，來驗證驗證碼。

**選項2：使用[!DNL Experience Manager Forms] ValidateCAPTCHA API在提交表單前，針對使用者動作驗證驗證碼**

您也可以在最適化表單的元件上套用規則，以叫用`ValidateCAPTCHA` API。

例如，您在最適化表單中新增&#x200B;**[!UICONTROL 驗證碼]**&#x200B;按鈕，並建立規則以在按一下按鈕時叫用服務。

下圖說明如何在按一下&#x200B;**[!UICONTROL 驗證碼]**&#x200B;按鈕時叫用服務：

![驗證碼驗證](assets/captcha-validation1.gif)

您可以使用規則編輯器叫用包含`ValidateCAPTCHA` API的自訂servlet，並根據驗證結果啟用或停用最適化表單的提交按鈕。

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

reCAPTCHA服務使用`https://www.recaptcha.net/`做為預設網域。 您可以修改設定以設定`https://www.google.com/`或任何自訂網域名稱，以載入、演算及驗證reCAPTCHA服務。

設定&#x200B;**[!UICONTROL 最適化表單和互動式通訊Web通道設定]**&#x200B;的&#x200B;**[!UICONTROL af.cloudservices.recaptcha.domain]**&#x200B;屬性，以指定`https://www.google.com/`或任何其他自訂網域名稱。 下列JSON檔案顯示範例：

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

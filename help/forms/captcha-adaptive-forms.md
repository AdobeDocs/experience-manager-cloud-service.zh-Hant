---
title: 驗證碼在自適應Forms中的應用
seo-title: Using CAPTCHA in Adaptive Forms
description: 瞭解如何在Adaptive AEM Forms中配置CAPTCHA或GooglereCAPTCHA服務。
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in Adaptive Forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: 580ab2731bc277bcd53c4863b3b22f5e44dc8406
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 3%

---

# 在自適應Forms中使用驗證碼{#using-captcha-in-adaptive-forms}

CAPTCHA(完全自動化公共圖靈test，將電腦和人區分開)是線上交易中常用的程式，用於區分人類和自動程式或機器人。 它提出了一個挑戰，並評估用戶響應，以確定它是人還是機器人與站點交互。 它防止用戶在test失敗時繼續操作，並通過防止bot發佈垃圾郵件或惡意目的，幫助確保線上交易的安全。

[!DNL AEM Forms] 支援自適應Forms驗證碼。 您可以使用Google的reCAPTCHA服務來實施CAPTCHA。

>[!NOTE]
>
>* [!DNL AEM Forms] 僅支援reCaptcha v2。 不支援任何其他版本。
>* 在離線模式下，不支援自適應Forms中的驗證碼 [!DNL AEM Forms] 的子菜單。
>


## 配置由Google提供的ReCAPTCHA服務 {#google-recaptcha}

表單作者可以使用Google的reCAPTCHA服務在自適應Forms中實現CAPTCHA。 它提供高級驗證碼功能以保護您的站點。 有關reCAPTCHA工作原理的詳細資訊，請參見 [GoogleRE CAPTCHA](https://developers.google.com/recaptcha/)。

![重新捕獲](assets/recaptcha_new.png)

在 [!DNL AEM Forms]:

1. 獲取 [reCAPTCHA API密鑰對](https://www.google.com/recaptcha/admin) Google。 它包括一個站點密鑰和一個秘密。
1. 為雲服務建立配置容器。

   1. Go to **[!UICONTROL Tools > General > Configuration Browser]**.
      * See the [Configuration Browser](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#introduction) documentation for more information.
   1. 執行以下操作以啟用雲配置的全局資料夾，或跳過此步驟為雲服務配置建立和配置另一個資料夾。

      1. 在配置瀏覽器中，選擇 **[!UICONTROL 全球]** 資料夾和點擊 **[!UICONTROL 屬性]**。

      1. In the Configuration Properties dialog, enable **[!UICONTROL Cloud Configurations]**.
      1. Tap **[!UICONTROL Save &amp; Close]** to save the configuration and exit the dialog.
   1. 在配置瀏覽器中，按一下 **[!UICONTROL 建立]**。
   1. 在「建立配置」對話框中，指定資料夾的標題並啟用 **[!UICONTROL 雲配置]**。
   1. 點擊 **[!UICONTROL 建立]** 建立為雲服務配置啟用的資料夾。


1. 為reCAPTCHA配置雲服務。

   1. 在您的Experience Manager作者實例上，轉到 ![工具–1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**。
   1. 點擊 **[!UICONTROL reCAPTCHA]**。 將開啟「配置」頁。 Select the configuration container created in the previous step and tap **[!UICONTROL Create]**.
   1. 為reCAPTCHA服務指定名稱、站點密鑰和密鑰並點擊 **[!UICONTROL 建立]** 建立雲服務配置。
   1. 在「編輯元件」對話框中，指定在步驟1中獲取的站點和密鑰。 點擊 **[!UICONTROL 保存設定]** 然後點擊 **[!UICONTROL 確定]** 完成配置。

   配置reCAPTCHA服務後，它可在AdaptiveForms中使用。 有關詳細資訊，請參見 [驗證碼在自適應Forms中的應用](#using-captcha)。

## 在自適應Forms中使用驗證碼 {#using-captcha}

To use CAPTCHA in Adaptive Forms:

1. 在編輯模式下開啟自適應表單。

   >[!NOTE]
   >
   >確保在建立自適應表單時選擇的配置容器包含reCAPTCHA雲服務。 也可以編輯「自適應表單」屬性以更改與表單關聯的配置容器。

1. 在元件瀏覽器中，拖放 **[!UICONTROL 驗證碼]** 到「自適應」窗體。

   >[!NOTE]
   >
   >不支援在自適應表單中使用多個驗證碼元件。 此外，建議不要在標籤為延遲載入的面板或片段中使用驗證碼。

   >[!NOTE]
   >
   >驗證碼是時間敏感型的，大約一分鐘後過期。 因此，建議將驗證碼元件放在自適應表單中「提交」按鈕之前。

1. 選擇您添加的驗證碼元件並點擊 ![招商](assets/configure-icon.svg) 編輯其屬性。
1. 指定驗證碼構件的標題。 預設值為 **[!UICONTROL 驗證碼]**。 選擇 **[!UICONTROL 隱藏標題]** 的子菜單。
1. 從 **[!UICONTROL 驗證碼服務]** 下拉，選擇 **[!UICONTROL 雷卡普查]** 啟用reCAPTCHA服務（如所述） [ReCAPTCHA服務，Google](#google-recaptcha)。 Select a configuration from the Settings drop-down.
1. Select the type as **[!UICONTROL Normal]** or **[!UICONTROL Compact]** for the reCAPTCHA widget. 也可以選擇 **[!UICONTROL 不可見]** 選項，僅在可疑活動時顯示驗證碼挑戰。 受reCAPTCHA標籤保護的標籤顯示在受保護的表單上。

   ![Google用reCAPTCHA徽章處理](assets/google-recaptcha-v2.png)

   >[!NOTE]
   >
   >Do not select **[!UICONTROL Default]** from the Captcha service drop-down as the default Experience Manager CAPTCHA service is deprecated.

1. Save the properties.

reCAPTCHA服務在自適應表單上啟用。 您可以預覽表單並查看驗證碼正在工作。

### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. 按一下元件，選擇 ![編輯規則](assets/edit-rules-icon.svg)，然後點擊 **[!UICONTROL 建立]** 的子菜單。 有關建立規則的詳細資訊，請參閱 [規則編輯器](rule-editor.md)。

例如，僅當表單中的「貨幣值」欄位的值大於25000時，CAPTCHA元件才必須顯示在自適應表單中。

點擊 **[!UICONTROL 貨幣值]** 的子例行程式，並建立以下規則：

![顯示或隱藏規則](assets/rules-show-hide-captcha.png)

### 進行驗證碼驗證 {#validate-captcha}

在提交表單或根據用戶操作和條件對驗證碼驗證進行基礎時，您都可以在自適應表單中驗證驗證碼。

#### 在提交表單時驗證驗證碼 {#validation-form-submission}

要在提交自適應表單時自動驗證驗證驗證碼，請執行以下操作：

1. 點擊驗證碼元件並選擇 ![招商](assets/configure-icon.svg) 的子菜單。
1. 在 **[!UICONTROL 驗證驗證驗證碼]** 選擇 **[!UICONTROL 在提交表單時驗證驗證碼]**。
1. 點擊 ![完成](assets/save_icon.svg) 的子菜單。

#### 驗證用戶操作和條件驗證驗證碼 {#validate-captcha-user-action}

要基於條件和用戶操作驗證驗證碼，請執行以下操作：

1. 點擊驗證碼元件並選擇 ![招商](assets/configure-icon.svg) 的子菜單。
1. 在 **[!UICONTROL 驗證驗證驗證碼]** 選擇 **[!UICONTROL 對用戶操作驗證驗證碼]**。
1. 點擊 ![完成](assets/save_icon.svg) 的子菜單。

[!DNL Experience Manager Forms] 提供 `ValidateCAPTCHA` 使用預定義條件驗證CAPTCHA的API。 您可以使用自定義提交操作或在自適應表單中定義元件規則來調用API。

以下是 `ValidateCAPTCHA` 使用預定義條件驗證CAPTCHA的API:

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

該示例表示 `ValidateCAPTCHA` API僅在填寫表單時用戶指定的數字框中的位數大於5時驗證表單中的驗證碼。

**選項1:使用 [!DNL Experience Manager Forms] 使用自定義提交操作驗證驗證查詢API**

執行以下步驟以使用 `ValidateCAPTCHA` 使用自定義提交操作驗證驗證碼的API:

1. 添加包含 `ValidateCAPTCHA` 自定義提交操作的API。 For more on custom Submit Actions, see [Create a custom Submit Action for Adaptive Forms](custom-submit-action-form.md).
1. 從中選擇自定義提交操作的名稱 **[!UICONTROL 提交操作]** 下拉清單 **[!UICONTROL 提交]** 自適應窗體的屬性。
1. Tap **[!UICONTROL Submit]**. The CAPTCHA gets validated based on the conditions defined in `ValidateCAPTCHA` API of the custom Submit Action.

**選項2:使用 [!DNL Experience Manager Forms] 在提交表單之前驗證CAPTCHA API以驗證用戶操作上的CAPTCHA**

您還可以調用 `ValidateCAPTCHA` API，方法是對自適應表單中的元件應用規則。

例如，添加 **[!UICONTROL 驗證驗證驗證碼]** 的子菜單。

The following figure illustrates how you can invoke a service on the click of a **[!UICONTROL Validate CAPTCHA]** button:

![進行驗證碼驗證](assets/captcha-validation1.gif)

可以調用包含的自定義Servlet `ValidateCAPTCHA` 使用規則編輯器的API，並根據驗證結果啟用或禁用自適應表單的提交按鈕。

Similarly, you can use rule editor to include a custom method to validate CAPTCHA in an Adaptive Form.

### 添加自定義驗證碼服務 {#add-custom-captcha-service}

[!DNL Experience Manager Forms] provides reCAPTCHA as the CAPTCHA service. 但是，您可以添加要在 **[!UICONTROL 驗證碼服務]** 的子菜單。

下面是向自適應表單添加附加CAPTCHA服務的介面的示例實現：

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

`captchaPropertyNodePath` 引用Sling儲存庫中CAPTCHA元件的資源路徑。 使用此屬性可包括特定於驗證碼元件的詳細資訊。 比如說， `captchaPropertyNodePath` 包括在CAPTCHA元件上配置的reCAPTCHA雲配置的資訊。 雲配置資訊提供 **[!UICONTROL 站點密鑰]** 和 **[!UICONTROL 密鑰]** 用於實施reCAPTCHA服務的設定。

`userResponseToken` 指 `g_recaptcha_response` 在解決一個形式的驗證碼後產生的。

### Edit reCAPTCHA service domain {#recaptcha-service-domain}

reCAPTCHA服務使用 `https://www.recaptcha.net/` 作為預設域。 You can modify the settings to set `https://www.google.com/` or any custom domain name for loading, rendering, and validating the reCAPTCHA service.

設定 **[!UICONTROL af.cloudservices.recaptcha.domain]** 屬性 **[!UICONTROL 自適應形式與交互通信Web通道配置]** 指定配置 `https://www.google.com/` 或任何其他自定義域名。 以下JSON檔案顯示示例：

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。

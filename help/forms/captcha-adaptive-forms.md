---
title: 在最適化Forms中使用驗證碼
seo-title: Using CAPTCHA in Adaptive Forms
description: 瞭解如何在Adaptive Forms中設定AEM驗證碼或Google reCAPTCHA服務。
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in Adaptive Forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
exl-id: 3fdbe5a3-5c3c-474d-b701-e0182da4191a
source-git-commit: 1633e02fc6b79a45582b919863662bc1d1b49b42
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 3%

---

# 在最適化Forms中使用驗證碼{#using-captcha-in-adaptive-forms}

CAPTCHA （完全自動化的公用圖靈測試，用於區分電腦和人類）是一種常用於線上交易的程式，用來區分人類和自動化程式或機器人。 這會帶來挑戰，並評估使用者回應，以判斷它是人類還是機器人與網站互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意目的來確保線上交易的安全。

[!DNL AEM Forms] 支援最適化Forms中的驗證碼。 您可以使用Google的reCAPTCHA服務來實作CAPTCHA。

>[!NOTE]
>
>* [!DNL AEM Forms] 僅支援reCaptcha v2。 不支援任何其他版本。
>* 上離線模式不支援最適化Forms中的驗證碼 [!DNL AEM Forms] 應用程式。
>

## 透過Google設定reCAPTCHA服務 {#google-reCAPTCHA}

表單作者可使用Google的reCAPTCHA服務，在最適化Forms中實作CAPTCHA。 它提供進階的驗證碼功能，以保護您的網站。 如需reCAPTCHA運作方式的詳細資訊，請參閱 [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![reCAPTCHA](assets/recaptcha_new.png)

若要在中實作reCAPTCHA服務 [!DNL AEM Forms]：

1. 取得 [recaptcha API金鑰組](https://www.google.com/recaptcha/admin) 來自Google。 它包含網站金鑰和密碼。
1. 建立雲端服務的設定容器。

   1. 前往 **[!UICONTROL 「工具」>「一般」>「設定瀏覽器」]**.
      * 請參閱 [設定瀏覽器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#introduction) 說明檔案以取得詳細資訊。
   1. 請執行以下操作來啟用雲端設定的全域資料夾，或跳過此步驟來建立和設定雲端服務設定的另一個資料夾。

      1. 在設定瀏覽器中，選取 **[!UICONTROL 全域]** 資料夾並點選 **[!UICONTROL 屬性]**.

      1. 在「組態屬性」對話方塊中，啟用 **[!UICONTROL 雲端設定]**.
      1. 點選 **[!UICONTROL 儲存並關閉]** 以儲存設定並結束對話方塊。

   1. 在設定瀏覽器中，點選 **[!UICONTROL 建立]**.
   1. 在建立設定對話方塊中，指定資料夾的標題並啟用 **[!UICONTROL 雲端設定]**.
   1. 點選 **[!UICONTROL 建立]** 以建立為雲端服務設定啟用的資料夾。

1. 設定reCAPTCHA的雲端服務。

   1. 在您的Experience Manager編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. 點選 **[!UICONTROL reCAPTCHA]**. 「組態」頁面隨即開啟。 選取在上一步建立的設定容器並點選 **[!UICONTROL 建立]**.
   1. 指定reCAPTCHA服務的名稱、網站金鑰和秘密金鑰，然後點選 **[!UICONTROL 建立]** 以建立雲端服務設定。
   1. 在「編輯元件」對話方塊中，指定在步驟1中取得的場地和秘密金鑰。 點選 **[!UICONTROL 儲存設定]** 然後點選 **[!UICONTROL 確定]** 以完成設定。

   設定reCAPTCHA服務後，就可在最適化Forms中使用。 如需詳細資訊，請參閱 [在最適化Forms中使用驗證碼](#using-captcha).

## 在最適化Forms中使用驗證碼 {#using-captcha}

若要在最適化Forms中使用驗證碼：

1. 在編輯模式下開啟最適化表單。

   >[!NOTE]
   >
   >確定建立最適化表單時選取的設定容器包含reCAPTCHA雲端服務。 您也可以編輯最適化表單屬性，以變更與表單相關聯的設定容器。

1. 在元件瀏覽器中，拖放 **[!UICONTROL 驗證碼]** 元件至最適化表單。

   >[!NOTE]
   >
   >不支援在最適化表單中使用多個Captcha元件。 此外，不建議在標示為延遲載入的面板或片段中使用驗證碼。

   >[!NOTE]
   >
   >驗證碼會區分大小寫，且約一分鐘後過期。 因此，建議將驗證碼元件放在最適化表單中提交按鈕之前。

1. 選取您新增的Captcha元件並點選 ![cmppr](assets/configure-icon.svg) 以編輯其屬性。
1. 指定驗證碼介面工具集的標題。 預設值為 **[!UICONTROL 驗證碼]**. 選取 **[!UICONTROL 隱藏標題]** 如果您不想顯示標題。
1. 從 **[!UICONTROL 驗證碼服務]** 下拉式清單，選取 **[!UICONTROL reCAPTCHA]** 啟用reCAPTCHA服務（若您已依照中的說明進行設定） [Google的reCAPTCHA服務](#google-reCAPTCHA). 從「設定」下拉式清單中選取設定。
1. 選取型別為 **[!UICONTROL 一般]** 或 **[!UICONTROL 壓縮]** 用於reCAPTCHA小工具。 您也可以選取 **[!UICONTROL 隱藏]** 選項，僅在可疑活動的情況下顯示CAPTCHA質詢。 受保護的reCAPTCHA徽章（如下所示）會顯示在受保護的表單上。

   ![受reCAPTCHA徽章保護的Google](assets/google-recaptcha-v2.png)

   >[!NOTE]
   >
   >* 不要選取 **[!UICONTROL 預設]** 已棄用Captcha服務下拉式清單中的預設Experience ManagerCAPTCHA服務。

1. 儲存屬性。

已在最適化表單上啟用reCAPTCHA服務。 您可以預覽表單並檢視驗證碼運作中。

### 根據規則顯示或隱藏驗證碼元件 {#show-hide-captcha}

您可以根據在最適化表單中套用至元件的規則，選擇顯示或隱藏驗證碼元件。 點選元件，選取 ![編輯規則](assets/edit-rules-icon.svg)，然後點選 **[!UICONTROL 建立]** 以建立規則。 如需建立規則的詳細資訊，請參閱 [規則編輯器](rule-editor.md).

例如，只有在表單中的「貨幣值」欄位的值超過25000時，CAPTCHA元件才會顯示在調適型表單中。

點選 **[!UICONTROL 貨幣值]** 欄位並建立以下規則：

![顯示或隱藏規則](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
>* 如果您選取reCAPTCHA v2設定，大小為 [!UICONTROL 隱藏] 則顯示/隱藏選項不適用。

### 進行驗證碼驗證 {#validate-captcha}

您可以在提交表單時驗證最適化表單中的驗證碼，或依據使用者動作和條件進行驗證碼驗證。

#### 在表單提交時驗證驗證碼 {#validation-form-submission}

若要在提交最適化表單時自動驗證碼：

1. 點選CAPTCHA元件並選取 ![cmppr](assets/configure-icon.svg) 以檢視元件屬性。
1. 在 **[!UICONTROL 驗證碼驗證]** 區段，選取 **[!UICONTROL 在表單提交時驗證驗證碼]**.
1. 點選 ![完成](assets/save_icon.svg) 以儲存元件屬性。

#### 驗證使用者動作和條件的驗證碼 {#validate-captcha-user-action}

若要根據條件和使用者動作來驗證驗證碼：

1. 點選CAPTCHA元件並選取 ![cmppr](assets/configure-icon.svg) 以檢視元件屬性。
1. 在 **[!UICONTROL 驗證碼驗證]** 區段，選取 **[!UICONTROL 使用者動作時驗證驗證碼]**.
1. 點選 ![完成](assets/save_icon.svg) 以儲存元件屬性。

[!DNL Experience Manager Forms] 提供 `ValidateCAPTCHA` 使用預先定義的條件來驗證驗證碼的API。 您可以使用自訂提交動作或透過在調適型表單中定義元件規則來叫用API。

以下範例為 `ValidateCAPTCHA` 使用預先定義條件來驗證驗證碼的API：

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

此範例表示 `ValidateCAPTCHA` 只有在使用者在填寫表單時指定的數字方塊位數大於5時，API才會驗證表單中的驗證碼。

**選項1：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API可使用自訂提交動作來驗證CAPTCHA**

執行以下步驟以使用 `ValidateCAPTCHA` 使用自訂提交動作驗證驗證碼的API：

1. 新增包含 `ValidateCAPTCHA` 自訂提交動作的API。 如需自訂提交動作的詳細資訊，請參閱 [建立最適化Forms的自訂提交動作](custom-submit-action-form.md).
1. 從中選擇自訂提交動作的名稱 **[!UICONTROL 提交動作]** 中的下拉式清單 **[!UICONTROL 提交]** 最適化表單的屬性。
1. 點選 **[!UICONTROL 提交]**. 系統會根據中定義的條件來驗證驗證碼 `ValidateCAPTCHA` 自訂提交動作的API。

**選項2：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API可在提交表單前，依使用者動作驗證驗證碼**

您也可以叫用 `ValidateCAPTCHA` API的方式是對調適型表單中的元件套用規則。

例如，您新增 **[!UICONTROL 驗證碼驗證]** 最適化表單中的按鈕，並建立規則以在按一下按鈕時叫用服務。

下圖說明如何在 **[!UICONTROL 驗證碼驗證]** 按鈕：

![進行驗證碼驗證](assets/captcha-validation1.gif)

您可以叫用包含的自訂servlet `ValidateCAPTCHA` API使用規則編輯器，並根據驗證結果啟用或停用最適化表單的提交按鈕。

同樣地，您可以使用規則編輯器在適用性表單中包含驗證CAPTCHA的自訂方法。

### 新增自訂驗證碼服務 {#add-custom-captcha-service}

[!DNL Experience Manager Forms] 提供reCAPTCHA作為CAPTCHA服務。 不過，您可以新增自訂服務，以顯示於 **[!UICONTROL 驗證碼服務]** 下拉式清單。

以下是將其他CAPTCHA服務新增至最適化表單的介面實作範例：

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

`captchaPropertyNodePath` 指的是Sling存放庫中驗證碼元件的資源路徑。 此屬性用於包含驗證碼元件的特定詳細資料。 例如， `captchaPropertyNodePath` 包含在CAPTCHA元件上設定的reCAPTCHA雲端設定資訊。 雲端設定資訊提供 **[!UICONTROL 網站金鑰]** 和 **[!UICONTROL 秘密金鑰]** 實作reCAPTCHA服務的設定。

`userResponseToken` 是指 `g_recaptcha_response` 在表單中解決驗證碼後產生的驗證碼。

### 編輯reCAPTCHA服務領域 {#reCAPTCHA-service-domain}

reCAPTCHA服務使用 `https://www.recaptcha.net/` 作為預設網域。 您可以修改設定以進行設定 `https://www.google.com/` 或任何自訂網域名稱，用於載入、呈現和驗證reCAPTCHA服務。

設定 **[!UICONTROL af.cloudservices.recaptcha.domain]** 的屬性 **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]** 要指定的設定 `https://www.google.com/` 或任何其他自訂網域名稱。 下列JSON檔案會顯示範例：

```json
{
  "af.cloudservices.recaptcha.domain": "https://www.google.com/"
}
```

若要設定值，[請使用 AEM SDK 產生 OSGi Configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並將[設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)您的 Cloud Service 執行個體。

---
title: 如何在AEM最適化表單中使用Google reCAPTCHA？
description: 使用Google reCAPTCHA服務輕鬆增強表單安全性。 內的逐步指南！
topic-tags: Adaptive Forms, author
keywords: Google reCAPTCHA服務，最適化Forms， CAPTCHA挑戰，機器人預防，核心元件，表單提交安全性，表單垃圾郵件預防
feature: Adaptive Forms, Core Components
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
role: User, Developer
source-git-commit: bba5e5d283da616baa57b788181af73d59d86ee3
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 3%

---

# 根據核心元件在AEM最適化表單中使用Google reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

| 套用至 | 文章連結 |
| -------- | ---------------------------- |
| 根據核心元件的最適化表單 | 本文章 |
| Adaptive Form based on Foundation Components | [按一下這裡](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) is a program commonly used in online transactions to distinguish between humans and automated programs or bots. It poses a challenge and evaluates user response to determine if it&#39;s a human or a bot interacting with the site. It prevents the user to proceed if the test fails and helps make online transactions secure by keeping bots from posting spam or malicious purposes.

AEM Forms as a Cloud Service supports the following CAPTCHA solutions:

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [驗證碼](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## 透過Google的reCAPTCHA服務連線您的AEM Forms環境 {#connect-your-forms-environment-with-recaptcha-service-by-google}

表單作者可使用Google的reCAPTCHA服務，在最適化Forms中實作reCAPTCHA。 It offers advance CAPTCHA capabilities to protect your site. [](https://developers.google.com/recaptcha/)[!DNL AEM Forms][!DNL Cloud Service]You can use it to present a CAPTCHA challenge on form submission. 若要使用Google的reCAPTCHA服務連線您的AEM Forms環境

1. 從Google取得[reCAPTCHA API金鑰組](https://www.google.com/recaptcha/admin)。 它包含&#x200B;**網站金鑰**&#x200B;和&#x200B;**秘密金鑰**。

   ![建立Google網站的Google reCAPTCHA組態以取得reCAPTCHA金鑰](/help/forms/assets/google-captcha.gif)
1. 在您的AEM Formsas a Cloud Service環境中建立設定容器。 設定容器內含用來將AEM連線至外部服務的雲端設定。 若要建立並設定設定設定容器，以透過Google將您的AEM Forms環境與reCAPTCHA服務連線：
   1. 開啟您的AEM Formsas a Cloud Service執行個體。
   1. 移至&#x200B;**[!UICONTROL 工具>一般>設定瀏覽器]**。 在設定瀏覽器中，您可以：
   1. 選取現有資料夾或建立資料夾。 您可以建立檔案夾並為其啟用Cloud Configurations選項，或為現有檔案夾啟用Cloud Configurations選項：

      * 若要建立資料夾並為其啟用雲端設定選項：
         1. 在組態瀏覽器中，按一下&#x200B;**[!UICONTROL 建立]**。
         1. ****
         1. 按一下「**[!UICONTROL 建立]**」。
      * To enable the Cloud Configurations option for an existing folder:
         1. ****
         1. ****
         1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並結束對話方塊。

1. 設定Cloud Service：
   1. ![](assets/tools-1.png)********
   1. Select a Configuration Container, created or updated in previous section. 選取「**[!UICONTROL 建立]**」。
   1. ****************&#x200B;選取「**[!UICONTROL 建立]**」。

   ![設定Cloud Service以透過Google將您的AEM Forms環境與reCAPTCHA服務連線](/help/forms/assets/captcha-configuration.gif)

   在設定reCAPTCHA服務後，就可在調適型表單中使用。 如需詳細資訊，請參閱[在最適化表單中使用Google reCAPTCHA](#using-reCAPTCHA)。

## 在最適化表單中使用 Google reCAPTCHA {#using-reCAPTCHA}

若要在最適化Forms中使用reCAPTCHA：

1. 開啟您的AEM Formsas a Cloud Service執行個體。
1. ********
1. ************

   [](#connect-your-forms-environment-with-recaptcha-service-by-google)

   ![](/help/forms/assets/captcha-properties.png)

1. ****&#x200B;最適化表單會在最適化Forms編輯器中開啟。
1. 從元件瀏覽器中，將&#x200B;**[!UICONTROL 最適化表單reCAPTCHA]**&#x200B;元件拖放至最適化表單。

   Google reCAPTCHA驗證常有時效性，約幾分鐘後就會過期。 因此，Adobe建議將&#x200B;**[!UICONTROL 最適化表單reCAPTCHA]**&#x200B;元件放在&#x200B;**[!UICONTROL 提交]**&#x200B;按鈕之前。

1. 選取&#x200B;**[!UICONTROL 最適化表單reCAPTCHA]**&#x200B;元件，並選取屬性![屬性圖示](assets/configure-icon.svg)圖示。 它會開啟屬性對話方塊。 指定下列強制屬性：
   * **[!UICONTROL 名稱]：**&#x200B;您可以在表單和規則編輯器中輕鬆識別具有唯一名稱的表單元件，但名稱不得包含空格或特殊字元。
   * **[!UICONTROL CAPTCHA組態]：**&#x200B;選取已設定為顯示表單之Google reCAPTCHA對話方塊的雲端組態。 基於類似目的，您的環境中可以有多個雲端設定。 因此，請謹慎選擇服務。 如果未列出任何服務，請參閱[透過Google將您的AEM Forms環境與reCAPTCHA服務連線](#connect-your-forms-environment-with-recaptcha-service-by-google)，以瞭解如何建立將您的AEM Forms環境與Google的reCAPTCHA服務連線的Cloud Service。
   * **驗證碼大小：**&#x200B;您可以選取Google reCAPTCHA挑戰對話方塊的顯示大小。 使用&#x200B;**[!UICONTROL Compact]**&#x200B;選項可顯示小尺寸，使用&#x200B;**[!UICONTROL Normal]**&#x200B;選項可顯示相對大尺寸的Google reCAPTCHA挑戰對話方塊。

1. 選取「**[!UICONTROL 完成]**」。

   現在，您的最適化表單上會顯示受reCAPTCHA保護的&#x200B;****。 它會顯示在所有設定為可使用Google reCAPTCHA服務的最適化Forms上。

   現在，僅允許提交合法表單，其中表單填寫者成功清除Google reCAPTCHA服務帶來的挑戰。
   ![受reCAPTCHA徽章保護的Google](/help/forms/assets/google-recaptcha-v2.png)

<!--
### Show or hide CAPTCHA component based on rules {#show-hide-captcha}

You can select to show or hide the CAPTCHA component based on rules that you apply on a component in an Adaptive Form. Select the component, select ![edit rules](assets/edit-rules-icon.svg), and select **[!UICONTROL Create]** to create a rule. For more information on creating rules, see [Rule Editor](rule-editor.md).

For example, the CAPTCHA component must display in an Adaptive Form only if the Currency Value field in the form has a value of more than 25000.

Select the **[!UICONTROL Currency Value]** field in the form and create the following rules:

![Show or hide rules](assets/rules-show-hide-captcha.png)

   >[!NOTE]
   >
   > When you select a reCAPTCHA v2 configuration and the size is set to [!UICONTROL Invisible], the show/hide option remains disabled.

   -->

## 常見問題

**問：我可以在最適化表單中使用多個驗證碼元件嗎？****** Also, it is not recommended to use Captcha component in a fragment or a panel marked for lazy loading.

## 另請參閱 {#see-also}

{{see-also}}
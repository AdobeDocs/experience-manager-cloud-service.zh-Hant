---
title: 如何在AEM最適化表單核心元件中使用驗證碼&amp； reg；？
description: Enhance form security with hCaptcha&reg; service effortlessly. Step-by-step guide inside!
topic-tags: Adaptive Forms, author
keywords: hCaptcha&reg; service, Adaptive Forms, CAPTCHA challenge, Bot prevention, Core Components, Form submission security, Form spam prevention
feature: Adaptive Forms, Core Components
hide: true
hidefromtoc: true
exl-id: 6c559df2-7b6a-42fe-b44c-29a782570a0c
role: User, Developer
source-git-commit: bba5e5d283da616baa57b788181af73d59d86ee3
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 2%

---

# Connect your AEM Forms environment with hCaptcha® {#connect-your-forms-environment-with-hcaptcha-service}

<span class="preview"></span>

CAPTCHA (Completely Automated Public Turing test to tell Computers and Humans Apart) is a program commonly used in online transactions to distinguish between humans and automated programs or bots. It poses a challenge and evaluates user response to determine if it&#39;s a human or a bot interacting with the site. It prevents the user to proceed if the test fails and helps make online transactions secure by keeping bots from posting spam or malicious purposes.

AEM Forms as a Cloud Service supports the following CAPTCHA solutions:

* [Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
* [](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)

## Integrate AEM Forms environment with hCaptcha Captcha

hCaptcha®服務可保護您的表單免受機器人、垃圾郵件和自動濫用的侵擾。 這會提出核取方塊Widget質詢，並評估使用者回應，以判斷它是人類還是機器人與表單互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意活動來確保線上交易的安全。

AEM Forms as a Cloud Service支援Adaptive Forms核心元件中的hCaptcha®。 您可以用它來在表單提交時顯示核取方塊Widget挑戰。

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### 將AEM Forms環境與hCaptcha整合的必要條件® {#prerequisite}

[](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key)

### Configure hCaptcha® {#steps-to-configure-hcaptcha}

To integrate AEM Forms with hCaptcha® service, perform the following steps:

1. Create a Configuration Container on your AEM Forms as a Cloud Service environment. 設定容器內含用來將AEM連線至外部服務的雲端設定。 若要建立並設定設定設定容器以使用hCaptcha連線您的AEM Forms環境®：
   1. 開啟您的AEM Formsas a Cloud Service執行個體。
   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. In the Configuration Browser, you can select an existing folder or create a folder. You can create a folder and enable the Cloud Configurations option for it or Enable the Cloud Configurations option for an existing folder:

      * To create a folder and enable the Cloud Configurations option for it:
         1. ****
         1. ****
         1. 按一下&#x200B;**[!UICONTROL 建立]**。
      * To enable the Cloud Configurations option for an existing folder:
         1. ****
         1. ****
         1. ****

1. Configure the Cloud Service:
   1. 在您的AEM作者執行個體上，移至![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**&#x200B;並選取&#x200B;**[!UICONTROL hCaptcha®]**。
      ui中的![hCaptcha®](assets/hcaptcha-in-ui.png)
   1. 選取已建立或已更新的設定容器，如上一節所述。 選取「**[!UICONTROL 建立]**」。
      ![組態hCaptcha®](assets/config-hcaptcha.png)
   1. ****************[](#prerequisite)選取「**[!UICONTROL 建立]**」。

      ![](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > 使用者不需要修改[使用者端JavaScript驗證URL](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage)和[伺服器端驗證URL](https://docs.hcaptcha.com/#verify-the-user-response-server-side)，因為它們已預先填入hCaptcha®驗證。

   設定hCAPTCHA服務後，即可用於根據核心元件的[最適化表單](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction)。

## 在最適化Forms核心元件®0}中使用hCaptcha}{#using-hCaptcha®-core-components}

1. 開啟您的AEM Formsas a Cloud Service執行個體。
1. ********
1. ************

   [](#connect-your-forms-environment-with-hcaptcha-service)

   ![](/help/forms/assets/captcha-properties.png)

1. ****&#x200B;最適化表單會在最適化Forms編輯器中開啟。
1. 從元件瀏覽器中，拖放或新增&#x200B;**[!UICONTROL 最適化表單hCaptcha®]**&#x200B;元件至最適化表單。
1. 選取&#x200B;**[!UICONTROL 最適化表單hCaptcha®]**&#x200B;元件，然後按一下屬性![屬性圖示](assets/configure-icon.svg)圖示。 它會開啟屬性對話方塊。 指定下列屬性：

   ![hCaptcha® v2](assets/config-hcaptcha-v2.png)

   * ****
   * ****
   * ****
   * ************<!-- or **[!UICONTROL Invisible]** to validate hCaptcha&reg; without explicitly rendering the checkbox widget on the user interface. -->
   * ****
   * **[!UICONTROL 指令碼驗證訊息]** — 此選項可讓您輸入指令碼驗證失敗時顯示的訊息。
     >[!NOTE]
     >You can have multiple Cloud Configurations in your environment for a similar purpose. So, choose the service carefully. [](#connect-your-forms-environment-with-hcaptcha-service)
     <!--* **Error Message:** Provide the error message to display to the user when the Captcha submission fails.-->

1. 選取「**[!UICONTROL 完成]**」。


Now, only legitimate forms, in which the form filler successfully clears the challenge posed by the hCaptcha® service are allowed for the form submission. hCaptcha®

****


## 常見問題

* ****
* **** Also, it is not recommended to use a Captcha component in a fragment or a panel marked for lazy loading.

## 另請參閱 {#see-also}

{{see-also}}

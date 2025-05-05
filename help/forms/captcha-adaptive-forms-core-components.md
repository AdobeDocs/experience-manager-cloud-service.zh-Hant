---
title: 如何在AEM最適化表單中使用Google reCAPTCHA？
description: 使用Google reCAPTCHA服務輕鬆增強表單安全性。 內的逐步指南！
topic-tags: Adaptive Forms, author
keywords: Google reCAPTCHA服務，最適化Forms， CAPTCHA挑戰，機器人預防，核心元件，表單提交安全性，表單垃圾郵件預防
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: d116f979-efb6-4fac-8202-89afd1037b2c
source-git-commit: 76301ca614ae2256f5f8b00c41399298c761ee33
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 2%

---

# 在AEM最適化表單中，根據核心元件使用Google reCAPTCHA {#using-reCAPTCHA-in-adaptive-forms}

| 套用至 | 文章連結 |
| -------- | ---------------------------- |
| 根據核心元件的最適化表單 | 本文章 |
| 根據Foundation元件的最適化表單 | [按一下這裡](/help/forms/captcha-adaptive-forms.md) |

CAPTCHA （完全自動化公用圖靈測試來區分電腦和人之間的差異）是一種常用於線上交易的程式，以區分人和自動化程式或機器人。 這會帶來挑戰，並評估使用者的回應，以判斷其是否為人類或機器人與網站互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意目的來確保線上交易的安全。

AEM Forms as a Cloud Service支援下列驗證碼解決方案：

* [Google reCAPTCHA](#connect-your-aem-forms-environment-with-recaptcha-service-by-google)
* [驗證碼](/help/forms/integrate-adaptive-forms-hcaptcha-core-components.md)


## 透過Google將您的AEM Forms核心元件與reCAPTCHA服務連線 {#connect-your-forms-environment-with-recaptcha-service-by-google}

表單作者可使用Google的reCAPTCHA服務，在最適化Forms中實作reCAPTCHA。 它提供進階驗證碼功能以保護您的網站。 如需reCAPTCHA運作方式的詳細資訊，請參閱[Google reCAPTCHA](https://developers.google.com/recaptcha/)。 您用它來提交表單時提出驗證碼質詢。[!DNL AEM Forms] as a [!DNL Cloud Service]支援Google reCAPTCHA v2和reCAPTCHA Enterprise。 不支援任何其他版本。 另請注意，在AEM Forms應用程式的離線模式中不支援最適化Forms中的reCAPTCHA。

您可以根據自己的需求，設定reCAPTCHA服務以啟用：

* [reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms-core-components)
* [reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)

### 設定reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms-core-components}

1. 建立或選取[Google Cloud專案](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin)並啟用[reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api)。
1. 取得[專案識別碼](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed)並建立網站的[API金鑰](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key)和[網站金鑰](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key)。
1. 建立雲端服務的設定容器。

   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 選取資料夾或建立資料夾，然後使用下列步驟啟用雲端設定的資料夾：
      1. 在組態瀏覽器中，選取資料夾並選取&#x200B;**[!UICONTROL 屬性]**。
      1. 在[組態內容]對話方塊中，啟用&#x200B;**[!UICONTROL 雲端組態]**。
      1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並結束對話方塊。

1. 設定[!DNL reCAPTCHA Enterprise]的雲端服務。

   1. 在您的Experience Manager作者執行個體上，前往![tools-1](assets/tools-1.png) > **[!UICONTROL 雲端服務]**。
   1. 選取&#x200B;**[!UICONTROL reCAPTCHA]**。 「組態」頁面隨即開啟。 選取您建立的組態容器，並選取&#x200B;**[!UICONTROL 建立]**。
   1. 選取版本為[!DNL reCAPTCHA Enterprise]，並指定reCAPTCHA Enterprise服務的名稱、專案ID、網站金鑰和API金鑰（在步驟2中取得）。
   1. 選取金鑰型別，金鑰型別應與您在[Google Cloud專案](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin)中設定的網站金鑰相同，例如，**核取方塊網站金鑰**&#x200B;或&#x200B;**以分數為基礎的網站金鑰**。
   1. 指定0到1[&#128279;](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores)範圍內的臨界值分數。 分數大於或等於臨界值分數會識別人類互動，否則會被視為機器人互動。
   1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立雲端服務組態。

<!--
    1. In the Edit Component dialog, specify the name, project ID, site key, API key (obtained in steps 2 and 3), select the key type, and enter the threshold score. Select **[!UICONTROL Save Settings]** and then select **[!UICONTROL OK]** to complete the configuration.
-->

reCAPTCHA Enterprise服務啟用後，就可在調適型表單中使用。 請參閱在最適化表單[&#128279;](#using-reCAPTCHA)中使用驗證碼。

<!--
![reCAPTCHA Enterprise](/help/forms/assets/recaptcha1-enterprise.png)
-->


### 設定Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. 從Google取得[reCAPTCHA API金鑰組](https://www.google.com/recaptcha/admin)。 它包含&#x200B;**網站金鑰**&#x200B;和&#x200B;**秘密金鑰**。

   ![建立Google網站的Google reCAPTCHA組態以取得reCAPTCHA金鑰](/help/forms/assets/google-captcha.gif)
1. 在您的AEM Forms as a Cloud Service環境中建立設定容器。 設定容器內含用來將AEM連線至外部服務的雲端設定。 若要建立並設定設定設定容器，以透過Google將您的AEM Forms環境與reCAPTCHA服務連線：
   1. 開啟您的AEM Forms as a Cloud Service執行個體。
   1. 移至&#x200B;**[!UICONTROL 工具>一般>設定瀏覽器]**。 在設定瀏覽器中，您可以：
   1. 選取現有資料夾或建立資料夾。 您可以建立檔案夾並為其啟用Cloud Configurations選項，或為現有檔案夾啟用Cloud Configurations選項：

      * 若要建立資料夾並為其啟用雲端設定選項：
         1. 在組態瀏覽器中，按一下&#x200B;**[!UICONTROL 建立]**。
         1. 在[建立組態]對話方塊中，指定名稱、標題，並選取&#x200B;**[!UICONTROL 雲端組態]**&#x200B;選項。
         1. 按一下「**[!UICONTROL 建立]**」。
      * 若要啟用現有資料夾的「雲端設定」選項：
         1. 在組態瀏覽器中，選取資料夾並選取&#x200B;**[!UICONTROL 屬性]**。
         1. 在[組態內容]對話方塊中，啟用&#x200B;**[!UICONTROL 雲端組態]**。
         1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並結束對話方塊。

1. 設定Cloud Service：
   1. 在您的AEM作者執行個體上，前往![tools-1](assets/tools-1.png) > **[!UICONTROL 雲端服務]**&#x200B;並選取&#x200B;**[!UICONTROL reCAPTCHA]**。
   1. 選取在前一節中建立或更新的「設定容器」。 選取「**[!UICONTROL 建立]**」。
   1. 指定reCAPTCHA服務的&#x200B;**[!UICONTROL Title]**、**[!UICONTROL Name]**、**[!UICONTROL 網站金鑰]**&#x200B;和&#x200B;**[!UICONTROL 秘密金鑰]** （在步驟1中取得）。 選取「**[!UICONTROL 建立]**」。

   ![設定Cloud Service以透過Google使用reCAPTCHA服務連線您的AEM Forms環境](/help/forms/assets/captcha-configuration.gif)

   在設定reCAPTCHA服務後，就可在調適型表單中使用。 如需詳細資訊，請參閱[在最適化表單中使用Google reCAPTCHA](#using-reCAPTCHA)。


在最適化表單中使用Google reCAPTCHA

## 在最適化表單中使用 Google reCAPTCHA {#using-reCAPTCHA}

若要在最適化Forms中使用reCAPTCHA：

1. 開啟您的AEM Forms as a Cloud Service執行個體。
1. 移至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
1. 選取最適化Forms並選取&#x200B;**[!UICONTROL 屬性]**。 針對&#x200B;**[!UICONTROL 組態容器]**&#x200B;選項，選取包含連線AEM Forms與Google的reCAPTCHA服務的雲端組態的組態容器，並選取&#x200B;**[!UICONTROL 儲存並關閉]**。

   如果您沒有這類設定容器，請參閱區段[透過Google將您的AEM Forms環境與reCAPTCHA服務連線](#connect-your-forms-environment-with-recaptcha-service-by-google)，以瞭解如何建立這類設定容器。

   ![選取設定容器](/help/forms/assets/captcha-properties.png)

1. 選取最適化Forms並選取&#x200B;**[!UICONTROL 編輯]**。 最適化表單會在最適化Forms編輯器中開啟。
1. 從元件瀏覽器中，將&#x200B;**[!UICONTROL 最適化表單reCAPTCHA]**&#x200B;元件拖放至最適化表單。

   >[!NOTE]
   > * Google reCAPTCHA驗證常有時效性，約幾分鐘後就會過期。 因此，Adobe建議將&#x200B;**[!UICONTROL 最適化表單reCAPTCHA]**&#x200B;元件放置在&#x200B;**[!UICONTROL 提交]**&#x200B;按鈕之前。

1. 選取&#x200B;**[!UICONTROL 最適化表單reCAPTCHA]**&#x200B;元件，並選取屬性![屬性圖示](assets/configure-icon.svg)圖示。 它會開啟屬性對話方塊。 指定下列強制屬性：
   * **[!UICONTROL 名稱]：**&#x200B;您可以在表單和規則編輯器中輕鬆識別具有唯一名稱的表單元件，但名稱不得包含空格或特殊字元。
   * **[!UICONTROL 標題]：**&#x200B;指定驗證碼介面工具集的標題。 預設值為&#x200B;**驗證碼**。 如果您不想顯示標題，請選取&#x200B;**隱藏標題**。 選取&#x200B;**允許標題為RTF格式**，以RTF格式編輯您的標題。 您也可以將標題標示為&#x200B;**未繫結的表單元素**。
   * **[!UICONTROL 驗證碼組態]：**&#x200B;從[設定]下拉式清單中選取&#x200B;**reCAPTCHA Enterprise**&#x200B;或&#x200B;**reCAPTCHA v2**&#x200B;的組態，以呈現表單的Google reCAPTCHA對話方塊：
      1. 若您選取&#x200B;**reCAPTCHA Enterprise**&#x200B;版本，金鑰型別可以是&#x200B;**核取方塊**&#x200B;或&#x200B;**以分數為基礎**，其依據是您在設定網站的[網站金鑰時的選擇](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key)：

         >[!NOTE]
         >
         >* 在&#x200B;**金鑰型別**&#x200B;為&#x200B;**核取方塊**&#x200B;的雲端設定中，如果驗證碼驗證失敗，自訂的錯誤訊息會顯示為內嵌訊息。
         >* 在&#x200B;**金鑰型別**&#x200B;為&#x200B;**以分數為**&#x200B;的雲端設定中，如果驗證碼驗證失敗，自訂的錯誤訊息會顯示為快顯訊息。

      1. 您可以選取&#x200B;**[!UICONTROL Normal]**&#x200B;和&#x200B;**[!UICONTROL Compact]**&#x200B;的大小。

     >[!NOTE]
     >* 基於類似目的，您的環境中可以有多個雲端設定。 因此，請謹慎選擇服務。 如果未列出任何服務，請參閱[透過Google將您的AEM Forms環境與reCAPTCHA服務連線](#connect-your-forms-environment-with-recaptcha-service-by-google)，以瞭解如何建立將您的AEM Forms環境與Google的reCAPTCHA服務連線的Cloud Service。

   * **驗證碼大小：**&#x200B;您可以選取Google reCAPTCHA挑戰對話方塊的顯示大小。 使用&#x200B;**[!UICONTROL Compact]**&#x200B;選項可顯示小尺寸，使用&#x200B;**[!UICONTROL Normal]**&#x200B;選項可顯示相對大尺寸的Google reCAPTCHA挑戰對話方塊。
如果您選取&#x200B;**reCAPTCHA v2**&#x200B;版本：
      1. 您可以為reCAPTCHA Widget選取大小為&#x200B;**[!UICONTROL Normal]**&#x200B;或&#x200B;**[!UICONTROL Compact]**。
      1. 您可以選取&#x200B;**[!UICONTROL 隱藏]**&#x200B;選項，只在可疑活動時才顯示驗證碼質詢。

   已針對最適化表單啟用reCAPTCHA服務。 您可以預覽表單，並檢視驗證碼是否正常運作。 受reCAPTCHA **保護的**&#x200B;徽章（如下所示）會顯示在受保護的表單上。

   ![受reCAPTCHA徽章保護的Google](/help/forms/assets/google-recaptcha-v2.png)

1. 選取「**[!UICONTROL 完成]**」。

   現在，您的最適化表單上會顯示受reCAPTCHA保護的&#x200B;**&#x200B;**。 它會顯示在所有設定為可使用Google reCAPTCHA服務的最適化Forms上。

   現在，僅允許提交合法表單，其中表單填寫者成功清除Google reCAPTCHA服務帶來的挑戰。

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

**問：我可以在最適化表單中使用多個驗證碼元件嗎？**
**Ans：**&#x200B;不支援在最適化表單中使用一個以上的Captcha元件。 此外，不建議在標籤為延遲載入的片段或面板中使用驗證碼元件。

## 另請參閱 {#see-also}

{{see-also}}
